---
title: 如何用Hexo搭建Github个人博客
description: Hexo+Github
date: 2022-03-14
tags:
  - 博客
  - Hexo
license: false
categories:
    - 博客
    - 教程
---

## 前提条件

1. 拥有一个Github账号。
2. 本机装有node.js,Git,hexo。

## 具体步骤

1. 在Github中新建一个以<<你的名字>.github.io>命名的repo。
    - 点进这个repo的settings,拉到最下面的github pages,select任意一个themes,点进你的github.io网站预览。
2. 本地新建一个文件夹,右键Git Bash输入`git init`,以初始化这个文件夹。
3. 配置SSH公钥：
    - 在文件夹内右键`ssh-keygen -t rsa -C "<你的github注册名>"`
    - 在本机找到id_rsa.pub文件,把里面的内容复制。
    - 在Github点进头像settings进入SSH and GPG keys配置页面,add ssh key,把刚刚复制的公钥黏贴到内容栏,名字任意取,在本地git bash输入`ssh -T git@github.com`,如果没报错就是成功了。
4. 在本地文件夹shift右键打开powershell,进行git config配置
```cmd
  git config --global user.name "<你的github用户名>"
  git config --global user.email "<你的github注册邮箱>"
```
5. 在本地文件夹右键git bash,输入`hexo init`以及`npm install`。
6. 到这里,你已经拥有了一个没有和github打通的静态博客了。你可以通过`hexo g -s`在本地的`localhost:4000`预览它。
7. 要想在github.io网站得到你的博客,首先需要打开_congif.yml,修改信息,使其可以连接到Github。
    - 拖到最后,把deploy下的type改为git,添加repo和branch,最后修改结束的deploy长这样：
```javascript
deploy:
  type: git
  repo: <GitHub中repo的ssh地址>
  branch: gh-pages
```
8. 运行`hexo g -d`来尝试部署到github上,这时打开github.io网站可能看到的还是第1步中的页面,而非之前运行`hexo s`时预览的画面,没有关系。
    - 点开GitHub repo的settings,拉到最下面的github pages,进入,把默认的main分支改成gh-pages（也就是第7步中你定义的分支）,然后再执行`hexo clean, hexo g -d`,即可在github.io浏览到和预览一样的网页内容。

## 注意事项和坑
我在搭hexo的时候遇到的问题包括：
1. 本地无法部署到github,导致`hexo d`和`hexo s`不一样,而`hexo d`的内容与最早时候github pages一样。
这个错误在于在修改_config.yml的时候把branch设置成了网上大多教程里的master而非gh-pages,在修改了这一步之后同样别忘记把github-repo-setttings-github pages的main改成gh-pages,做完这两步再`hexo g -d`就可以解决这个问题。
2. 换themes的时候`git clone`的地址是在themes下,而非根目录下,会导致错误。
3. `hexo g -d`如果有问题可以试一下先`hexo clean`再`hexo g -d`,因为可能之前编译的public和新的修改有冲突,导致错误。

## 后续可以玩的事
1. theme定制
    -  几个我觉得不错的theme:makito,maupassant。
2. layout的修改
3. 增加评论服务如disqus等

## 有用的文档
* [Hexo官方中文文档](https://hexo.io/zh-cn/docs/index.html)
* [将Hexo部署到GitHub Pages](https://hexo.io/zh-cn/docs/github-pages.html)
* [民间教程1](https://zhuanlan.zhihu.com/p/26625249)
* [民间教程2](https://zhuanlan.zhihu.com/p/35668237)
* [民间教程3](https://z.arlmy.me/posts/hexo/Hexo_BlogSetup/)
