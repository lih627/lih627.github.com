---
layout: article
title: Hello world, my blog!
tags: normal
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

配置jekyll的主题, 官方提供两种方式, 一种是fork官方的repo, 另外一种是下载官方给的zip文件, 我选择后者. 在 clone 下来的 `UserName.githu.com` 文件夹中, 把解压后的主题文件全部放进去, 这个时候运行 `bundle exec jekyll serve --livereload` , 就可以运行了静态网页, 对于M1芯片的Mac, 如果报错, 我还需要`bundle add webrick`才能让静态网站跑起来.
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
# LatTex code
$$
\begin{equation}
E = mc^2
\end{equation}
$$
```

解析结果
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


### 20240830 更新

最近想起来还有这个博客,发现在自己的笔记本电脑已经无法通过编译了.当时搭建过程也没有详细记录.
有很多东西还是要想清楚的.

- 这个博客通过jekyll生成. jekyll是一个开源的静态网站生成器,使用ruby编写.
- ruby 是一种变成语言,前面通过homebrew下载后,ruby自己有一套包管理器gem. 这个博客在开始搭建的时候,通过 gem 安装了 jekyll 和 bundler
-  bunder 也是一个ruby包管理工具,不同于gem,他管理的是项目级别的gem依赖,在这个博客的github目录下,可以看高 Gemfile, jekyll-text-theme.gemspec 共同决定了这个项目要安装哪些版本的包. 而 Gemfile.lock 就是 bundler 生成的文件,来安装项目级别的各种ruby库的版本
- 所以博客无法通过编译可能是各种版本有问题, 处理思路如下

```shell
# 安装新版本的 ruby
$ brew install ruby
# 安装结束后
$ ruby -v
ruby 3.3.4 (2024-07-09 revision be1089c8ec) [arm64-darwin23]
# 更新 jekyll 和 bundler
$ gem update jekyll bundler
# 切换到项目目录, 根据 Gemfile 和 *.gemspec 更新项目需要的包
$ bundle update
# 重新尝试本地编译态网站, 也需要在项目目录下
$ bundle exec jekyll server --livereload
```

### 20250619 更新

看起来目前 mac os ruby 版本无法在本地启动博客服务, 通过docker测试

先 cd 到项目目录, 然后运行
```
docker run --rm -it -p 4000:4000 -v "$(pwd):/srv/jekyll" ruby:3-bullseye bash 
cd /srv/jekyll/ &&  bundle update 
bundle exec jekyll server --livereload --host 0.0.0.0 --port 4000 
```


### References

1. [https://yuleii.github.io/](https://yuleii.github.io/)
2. [Markdown syntax](https://markdown.com.cn/basic-syntax/)
3. [Jekyll TeXt-theme doc](https://kitian616.github.io/jekyll-TeXt-theme/docs/en/quick-start)
4. 可以阅读 [jekyll 文档](https://jekyllrb.com/)了解更多内容