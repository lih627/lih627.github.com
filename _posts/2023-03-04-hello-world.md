---
layout: article
title: Hello world, my blog!
tags: Normal
mathjax: true
---

Hellow world ~

<!--more-->

### 搭建个人博客

使用 Jekyll + TeXt 主题搭建, 主题相关配置可参考 [TeXt-theme](https://kitian616.github.io/jekyll-TeXt-theme/test/). 首先需要配置本地环境, 用来测试:

1. 创建一个 `[UserName].github.com` 的 空Repo, 对于我是 `lih627.github.com`
2. 下载 Ruby 和 Jekyll, MacOS 自带 rbuy 但是版本过低, 我使用 homebrew 安装 `brew install ruby`.
3. 安装结束后, 在 `~/.zshrc` 使用新的 ruby binary, `[-d $DIR_PATH]` 用来判断路径是否存在, 然后重启终端
```bash
if [ -d "$(brew --prefix)/opt/ruby/bin" ]; then
  export PATH=$(brew --prefix)/opt/ruby/bin:$PATH
  export PATH=`gem environment gemdir`/bin:$PATH
  echo "Change ruby path to $(brew --prefix)/opt/ruby/bin done."
fi
```
4. 安装 jekyll `gem install jekyll`

配置jekyll的主题, 官方提供两种方式, 一种是fork官方的repo, 另外一种是下载官方给的zip文件, 我选择后者. 在 clone 下来的 `UserName.githu.com` 文件夹中, 把解压后的主题文件全部放进去, 这个时候运行 `bundle exec jekyll serve` , 就可以运行了静态网页, 对于M1芯片的Mac, 如果报错, 我还需要`bundle add webrick`才能让静态网站跑起来.
```
 Auto-regeneration: enabled for '/Users/hao/Code/lih627.github.com'
    Server address: http://127.0.0.1:4000
  Server running... press ctrl-c to stop.
```
成功运行后, 将 repo 中的改动 push 到远程master分支, github 会通过 Actions 自动帮忙生成网页, 即 [lih627.github.io](lih627.github.io)

### 如何写文章

文章放在 `_posts` 文件夹下面, 命名格式是 `YYYY-MM-DD-the-post-name.md`. 在 markdown 文件头, 需要加入 YAML Front Matter:

```yaml
layout: article
title: Document - Writing Posts
mathjax: true # 我在_config.yaml 已经默认设置为True了
```

文章使用markdown语法, 并支持LatTex 例如:
```plain
$$
\begin{equation}
E = mc^2
\end{equation}
$$
```

$$
\begin{equation}
E = mc^2
\end{equation}
$$


可以加载图片(我将图片放到了 repo `/imgs` 下):
```
![My Cannon80D](/imgs/2023-03-05-Canon80D.jpeg){:height="50%" width="50%" .circle}
```
![My Cannon80D](/imgs/2023-03-05-Canon80D.jpeg){:height="50%" width="50%" .circle}


### References

1. [https://yuleii.github.io/](https://yuleii.github.io/)
2. [Markdown syntax](https://markdown.com.cn/basic-syntax/)
3. [Jekyll TeXt-theme doc](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/quick-start)
