---
layout: post
title:  "Thanks to Jekyll!"
date:   2026-01-29 17:22:20 +0800
categories: basic tutorial
usemathjax: true
---


# Jekyll本地安装和使用

## 1. Ruby+Devkit安装

下载Ruby+Devikit的安装包[rubyinstaller.org](https://rubyinstaller.org/downloads/)，使用默认选项进行安装
<div align="center">
<img src="https://github.com/ZYCheng1002/platypus/blob/main/images/welcome-to-jekyll/ruby_installer.png?raw=true" alt="rubyinstaller.org" width="400">
</div>

最后一步，不要勾选`ridk install`的选项，选择自己安装ridk

检查ruby是否安装成功:`ruby -v`

<div align="center">
<img src="https://github.com/ZYCheng1002/platypus/blob/main/images/welcome-to-jekyll/ruby_v.png?raw=true" alt="ruby -v" width="400">
</div>

更换源:
`gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/`
更换完成后， 使用指令`gem sources -l`确认是否成功。

安装 `MSY32`, 执行 `ridk install`, 执行后需要进行选择，直接选择3: 
<div align="center">
<img src="https://github.com/ZYCheng1002/platypus/blob/main/images/welcome-to-jekyll/ridk_install.png?raw=true" alt="ridk install" width="400">
</div>
安装结束后, 最后进行选择时, 直接回车即可:
<div align="center">
<img src="https://github.com/ZYCheng1002/platypus/blob/main/images/welcome-to-jekyll/enter.png?raw=true" alt="ridk install" width="400">
</div>


## 2. 安装Jekyll
输入指令:
`gem install bundler`  

输入指令:
`gem install jekyll`  
检查jekyll安装是否成功:   
`jekyll -v`

## 3. 安装本项目及其依赖

`git clone https://github.com/ZYCheng1002/ZYCheng1002.github.io`  
更改Gemfile中的`source "https://gems.ruby-china.com/"`为国内源  
执行指令:  
`bundle install`

等待安装完成后， 运行  
`bundle exec jekyll serve`  
在浏览器里打开 [http://127.0.0.1:4000](http://127.0.0.1:4000)

## 参考链接

- [使用Jekyll在GitHub Pages上搭建网站个人博客](https://blog.csdn.net/qq_46207024/article/details/140456475): 有关于如何解决错误
- [RedKetchup](https://redketchup.io/favicon-generator): 生成icon
- [jekyll-klise](https://github.com/piharpi/jekyll-klise): 模板链接

## 注

Jekyll 要求博客文章文件按照以下格式命名:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.






