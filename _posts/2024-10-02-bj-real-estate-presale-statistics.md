---
layout: article
title: 北京预售制楼盘售出信息统计
tags: statistics daily python
---

从住建委网站爬了一批预售制楼盘的车位售卖结果.

<!--more-->

# 简介

北京住建委网站会公开商品房的状态, 
可以通过 [url](http://bjjs.zjw.beijing.gov.cn/eportal/ui?pageId=307670) 去搜索各个楼盘的状态. 

这里只统计商品房. 商品房状态分类两种:

期房, 房屋状态可能为:
- 不可售
- 可售
- 已预订
- 已签约
- 已办理预售项目抵押
- 网上联机备案
- 资格核验中

现房, 房屋状态可能为:
- 不可售
- 已预订
- 已签约
- 未签约
- 资格核验中

注意到 房屋状态通过不同颜色表示, 因此很容易统计签约售卖情况.

# 统计结果

TL;DR 签约比例没有超过50%的,大部分在30%左右.

2024-10-02 统计结果, 以下统计的都是车位和仓储相关签约情况:

铭润嘉园 **现房** 
[京 (2024) 海不动产权第 0010064 号](http://bjjs.zjw.beijing.gov.cn/eportal/ui?pageId=424476&projectID=24504969&systemID=3&srcId=1) 
2024-07-01 签约百分比 10.70%

```
建筑面积:37073.1300m2地上:1层地下:2层拟售参考均价(由开发企业提供):丙类库房：27980.00元/平 车位：11717.92元/平
测绘机构:北京大地万川测绘有限公司
------ Result ------
状态 已签约, 套数 46, 百分比 10.70%
状态 未签约, 套数 384, 百分比 89.30%
```

毓润嘉园 **现房** 
[京 (2023) 海不动产权第 0026909 号](http://bjjs.zjw.beijing.gov.cn/eportal/ui?pageId=424476&projectID=24246988&systemID=3&srcId=1) 
2023-11-01 签约百分比 30.69%

```
建筑面积:51623.2800m2地上:1层地下:3层拟售参考均价(由开发企业提供):车位：10814.44元/平 库房：279他商业服务设施(含菜市场)：25000.00元/平
测绘机构:北京中土凯林勘测设计有限公司
------ Result ------
状态 未签约, 套数 454, 百分比 69.31%
状态 已签约, 套数 201, 百分比 30.69%
```

铭润嘉园 **现房** 
[京 (2023) 海不动产权第 0034803 号](http://bjjs.zjw.beijing.gov.cn/eportal/ui?pageId=424476&projectID=24143518&systemID=3&srcId=1) 
2023-11-01 签约百分比 34.96%

```
建筑面积:29238.2500m2地上:1层地下:2层拟售参考均价(由开发企业提供):丙类库房：28005.94元/平 车位： 其他商业服务设施(含菜市场)：25000.00元/平
测绘机构:北京大地万川测绘有限公司
------ Result ------
状态 已签约, 套数 93, 百分比 34.96%
状态 未签约, 套数 173, 百分比 65.04%
```

汇德里 **现房** 
[京房售证字 (2022) 154 号](http://bjjs.zjw.beijing.gov.cn/eportal/ui?pageId=320794&projectID=7438306&systemID=2&srcId=1#) 
2022-09-30 

汇德里比较特殊, 显示 1# 2# 地下车库分别有 426 和 384 套, 
网签套书为250, 官方显示销售状态已售完. 假如按照 网签 / 总套数计算, 比例约为 30.8%


富华里富园 **预售**
[京房售证字 (2023) 47 号](http://bjjs.zjw.beijing.gov.cn/eportal/ui?pageId=320794&projectID=7607383&systemID=2&srcId=1) 
2023-04-28 签约百分比 7.95%

```
建筑面积:32191.1000m2地上:1层地下:2层合同竣工日期:2025-06-30
拟售参考均价(由开发企业提供):车位：12963.55元/平
测绘机构:北京大地万川测绘有限公司资质证号:乙测资字1111409分摊
------ Result ------
状态 可售, 套数 760, 百分比 92.01%
状态 网上联机备案, 套数 59, 百分比 7.14%
状态 已签约, 套数 7, 百分比 0.85%
```

富华里汇园 **预售** 
[京房售证字 (2023) 48 号](http://bjjs.zjw.beijing.gov.cn/eportal/ui?pageId=320794&projectID=7607382&systemID=2&srcId=1) 
2023-04-28 10#地下车库签约百分比 39.25%

```
建筑面积:35596.4500m2地上:1层地下:2层合同竣工日期:2025-08-30
拟售参考均价(由开发企业提供):车位：13310.96元/平
测绘机构:北京金房兴业测绘有限公司资质证号:甲测资字11110262分
------ Result ------
状态 可售, 套数 483, 百分比 60.75%
状态 网上联机备案, 套数 285, 百分比 35.85%
状态 已签约, 套数 27, 百分比 3.40%
```

玉和雅苑 **预售** 
[京房售证字 (2024) 71 号](http://bjjs.zjw.beijing.gov.cn/eportal/ui?pageId=320794&projectID=7901306&systemID=2&srcId=1) 
2024-08-21 
19-1#地下车库签约比例: 3.46% 
19-2#地下车库签约比例: 6.29%

```
19-1# 地下车库
建筑面积:14509.8500m2地上:0层地下:2层合同竣工日期:2025-09-25
拟售参考均价(由开发企业提供):车位：11770.22元/平
测绘机构:沐城测绘（北京）有限公司资质证号
------ Result ------
状态 可售, 套数 363, 百分比 96.54%
状态 已签约, 套数 13, 百分比 3.46%

19-2# 地下车库
建筑面积:27237.0300m2地上:1层地下:2层合同竣工日期:2025-09-25
拟售参考均价(由开发企业提供):车位：11637.89元/平
测绘机构:沐城测绘（北京）有限公司资质证号:
------ Result ------
状态 可售, 套数 432, 百分比 93.71%
状态 已签约, 套数 29, 百分比 6.29%
```

# 脚本

```python
import collections
import os
import re

import click
import requests
from bs4 import BeautifulSoup

kStatusLabels = ['不可售',
                 '可售',
                 '已预订',
                 '已签约',
                 '已办理预售项目抵押',
                 '网上联机备案',
                 '资格核验中',
                 '已预订',
                 '未签约',
                 '资格核验中',
                 ]


def _parse_label_and_bgcolor(parent_tr) -> dict:
    label_to_bgcolor = {}
    prev = None
    for td in parent_tr.find_all('td'):
        current_text = td.get_text()
        for tag in kStatusLabels:
            if tag in current_text:
                # td = prev.find('td')
                label_to_bgcolor[tag] = prev.get('style')
        prev = td
    return label_to_bgcolor


def _parse(soup: BeautifulSoup, debug_mode=False):
    for info in soup.find_all('td', {'bgcolor': '#F9F4E8'}):
        info_str = info.get_text(strip=True)
        if info_str:
            print(info_str)
    label_to_bgcolor = {}
    for status_tag in kStatusLabels:
        span_tags = soup.find_all('span', text=re.compile(status_tag))
        for span in span_tags:
            parent_tr = span.find_parent('tr')
            if parent_tr:
                label_to_bgcolor = _parse_label_and_bgcolor(parent_tr)
                break
        if label_to_bgcolor:
            break
    bgcolor_to_label = {v: k for k, v in label_to_bgcolor.items()}
    if debug_mode:
        print('------ Debug ------')
        for k, v in label_to_bgcolor.items():
            print(f'状态 {k}: {v}')
        print(bgcolor_to_label)
    counter = collections.defaultdict(int)
    status_with_produce_id = collections.defaultdict(list)
    all_produces = soup.find_all('div', id=lambda x: bool(x) and str(x).isdigit(), style=lambda x: bool(x))
    for each_produce in all_produces:
        style = each_produce.get('style')
        find = False
        for k in bgcolor_to_label:
            if k in style:
                find = True
                counter[bgcolor_to_label[k]] += 1
                status_with_produce_id[bgcolor_to_label[k]].append(each_produce.get_text(strip=True))
            if find:
                break
    print('------ Result ------')
    sum = 0
    for k in counter:
        sum += counter[k]
    for k, v in counter.items():
        print(f'状态 {k}, 套数 {v}, 百分比 {v / float(sum) * 100.0:.2f}%')
    for k, v in status_with_produce_id.items():
        if k in ['可售', '未签约']:
            continue
        print(f'状态 {k}: 房间号{v}')


@click.group()
def cli():
    pass


@click.command()
@click.option('--url', default='',
              help='zjw url, e.g. http://bjjs.zjw.beijing.gov.cn/eportal/ui?pageId=320833&systemId=2&categoryId=1&salePermitId=7901306&buildingId=542133')
@click.option('--debug_mode', is_flag=True, default=False, help='enable debug mode.')
def statistic_url(url: str, debug_mode) -> None:
    response = requests.get(url)
    if response.status_code == 200:
        soup = BeautifulSoup(response.text, 'html.parser')
    else:
        raise RuntimeError(f"Failed to retrieve the webpage. Status code: {response.status_code}")
    print(f'开始统计... url: {url}')
    _parse(soup, debug_mode)

cli.add_command(statistic_url)

if __name__ == '__main__':
    cli()
```