---
layout: article
title: JSON vs Porotobuf Formatting
tags: code cpp 
---

最近发现,对于包含 value 为 unicode的 JSON 和 protobuf, toStyledString 和 DebugString 打印结果不相同.
还以为是自己遇到了bug, 实际上两者存储的内容并无区别.

<!--more-->

## JSON vs Protobuf

假设定义 Json

```json
{
    "name": "桃"
}
```

```proto
message Msg {
    optional string name = 1;
}
```

在应用场景需要手动讲json返回值处理后给proto, 例如:
```cpp
Json::Value value;
LoadValueFromBackend(&value);
Msg msg;
if (value.isMembor("name") && !value["name"].asString().empty()) {
    msg->set_name(value["name"].asString());
}
std::cout << value.toStyledString() << std::endl;
std::cout << msg.DebugString() << std::endl;
```

工作中发现打印出来的debug string 的内容不一致:
```
json: '\u6843'
protobuf: '\346\214\203'
```

但是如果:
```cpp
std::cout << value["name"].asString() << std::endl;
std::cout << msg.name() << std::endl;
```

发现打印出来的都是 `桃`

这是由于字符串编码方式的不同以及这些编码在不同的上下文中如何被展示的差异造成的:

1. `value.toStyledString()` 输出 JSON:

    - 当使用 `value.toStyledString()` 来打印 JSON 对象时, JSON 序列化器会将非 ASCII 字符(例如中文字符“桃”)转换为 Unicode 转义序列的形式。这种形式通常是 `\u` 加上四位十六进制数字. 例如，字符“桃”对应的 Unicode 码点是 `0x6843`，所以会显示为 `\u6843`.

2. `msg.DebugString()` 输出 Protobuf:

    - 	Protobuf 的 `DebugString()` 打印的是消息的调试信息, 字符串字段会以八进制的字节序列形式显示. 对于 UTF-8 编码的字符串, `DebugString()` 会将每个字节转换为相应的八进制表示. 字符“桃”在 UTF-8 编码下对应的字节序列是 `E6 94 83`, 而 `DebugString()` 中八进制的表示法是 `\346\241\203`.

3. `value["name"].asString()` 和 `msg.name()` 直接打印字符串:

    - 当直接打印时, 字符串会被直接输出为 UTF-8 编码的文本, 因此你看到的就是原始的“桃”字符.

4. UTF-8 `\u6842` 为 `0x6843`, UTF-8 编码后的结果为 `11100110 10100001 10000011` 即 `(11)(100)(110) (10)(100)(001) (10)(000)(011), 346 241 203` 

总结：

- 编码: `toStyledString()` 和 `DebugString()` 输出中对非 ASCII 字符的处理方式不同.
- 表现形式: `toStyledString()` 使用 Unicode 转义序列，`DebugString()` 使用八进制字节表示.


解决方案:

可对Protobuf进行escaping,确定utf8转义:

```cpp
#include <iostream>
#include <string>
#include "your_proto.pb.h"  // 包含生成的消息类

int main() {
    Msg msg;
    msg.set_name("桃");  // "桃" 的 Unicode 码点是 U+6843

    std::cout << "Default DebugString() output:" << std::endl;
    std::cout << msg.DebugString() << std::endl;

    // 设置 UTF-8 转义
    google::protobuf::TextFormat::Printer printer;
    printer.SetUseUtf8StringEscaping(true);

    std::string output;
    printer.PrintToString(msg, &output);

    std::cout << "With UTF-8 escaping:" << std::endl;
    std::cout << output << std::endl;

    return 0;
}
```


## Unicode 和 UTF-8 关系

可以参考 [字符编码笔记：ASCII，Unicode 和 UTF-8](https://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html). 简单来说 UTF-8 就是在互联网上使用最广的一种 Unicode 的实现方式.