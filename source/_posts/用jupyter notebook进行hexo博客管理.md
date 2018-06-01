---
title: 用jupyter notebook进行hexo博客管理
date: 2017-06-18 10:59:29
tags:
  - jupyter
  - 环境配置
  - python
categories:
  - 环境配置
comments: false
---

&emsp;&emsp;我很久都没有再发博客，很大一部分的原因是我总是很懒得切换系统去发博客，而且我的linux输入法有问题每次都需要重装，这让我觉得很痛苦。前几天丁丁给我安利了jupyter notebook，我也恰巧想把博客转成一个随记的地方，就配置了试试。

## 准备工作
&emsp;&emsp;我是在服务器上安装jupyter notebook,系统是Linux。这里有一个官方的安装配置的[介绍][1]，可以参考下。
[1]: http://jupyter.org/install.html
&emsp;&emsp;智障的我一开始以为是本地安装，虽然后面改正了，但是还是被丁丁嘲笑&&嫌弃了。又颠颠地跑去服务器重新配置了下环境，其实就是python和pip，具体的安装命令要是不知道就输入这两个命令，会有提示的。哦，记得要加sudo，我为此还辛辛苦苦找了半天的错 ಥ_ಥ。

## 安装过程
&emsp;&emsp;在安装好pip之后就可以试用一下命令安装jupyter notebook了。
```shell
pip install jupyter
```

## 配置过程
&emsp;&emsp;官方说法是输入以下命令就可以打开一个jupyter notebook的网页了。
```shell
jupyter notebook
```
&emsp;&emsp;但是我是服务器啊，还是个没有浏览器的服务器，即使我手动输入网址，也是没有办法访问，所以这时候就需要对jupyter notebook做一些配置，这个过程我参考了丁丁的[博客][2]。
[2]: https://blog.mythsman.com/2016/03/06/1/
&emsp;&emsp;首先是密码部分，你肯定不希望谁都能通过这个端口访问你的文件，苏偶一这时候我们就需要一个密码。按照他博客上说的方法也是可行的，但是jupyter notebook自己就带了可以修改密码的命令，然后输入密码就可以了。
```shell
jupyter notebook passwd
```
&emsp;&emsp;在一开始的时候是在找不到jupyter notebook的.config文件的，需要用下面的命令生成一个这样的文件。
```shell
jupyter notebook --generate-config
```
&emsp;&emsp;然后就可以通过这个命令对配置进行修改了，在文件中去掉一些注释，然后修改赋值，具体如下：
```shell
c.NotebookApp.ip = '*'
c.NotebookApp.open_browser = False
c.NotebookApp.port = 8888
```

## 存在的问题
&emsp;&emsp;做完以上的这些事情我就可以访问我的jupyter notebook了，但是在访问的过程中存在一个问题，就是对于.md结尾的文件，点击文件名永远是view的界面，但对于txt的文件，就直接是edit的界面。而且对于所有的中文名的文件，点击edit都是无法编辑，显示404错误，但是可以通过将view的界面手动改成edit来修改文件。对于英文名称的文件都是可以编辑的。这个我也很忧桑，丁丁也帮我挣扎了一会儿，无果。要看到这篇博客的各位恰巧知道解决方法的话，拜托联系我下，谢谢。
