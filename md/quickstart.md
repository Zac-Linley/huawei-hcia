# 快速开始

## 创建仓库

你可以选择[GitHub](https://github.com/)或[Gitee](https://gitee.com/)来托管你的文档。

## 克隆远程仓库

文档的编辑和修改是需要再本地完成的，所以需要把仓库克隆到本地。

[#如何安装配置git](https://www.runoob.com/git/git-install-setup.html)

## 初始化docsify

### 安装`docsify-cli`工具 :id=doc-cli

`docsify-cli`依赖于Node

[如何安装配置Node.js](https://www.runoob.com/nodejs/nodejs-install-setup.html)

使用如下命令验证安装：
```shell
#查看node版本号
node -v
#查看npm版本号
npm -v
```

> npm其实是Node.js的包管理工具（package manager）</br>npm已经在Node.js安装的时候顺带装好了。

安装`docsify-cli`工具：

```shell
npm i docsify-cli -g
```

!> `-g`表示全局安装`docsify-cli` 工具，可以方便地创建及在本地预览生成的文档。

### docsify初始化 :id=init

```shell
docsify init <Project Path>
```
> `<Project path>`是从git仓库克隆项目的本地路径。

### 本地预览

这个基于刚刚安装的[`docsify-cli`](#doc-cli)

```shell
docsify serve <Project Path>

Serving <Project Path> now.
Listening at http://localhost:3000
```

在浏览器中访问`http://localhost:3000`即可实时预览。

## 目录结构

初始化即自动创建下面几个文件：

```text
<Project path>
.
├── README.md  //入口文件
├── index.html  //会做为主页内容渲染
└── .nojekyll  //用于阻止GitHub Pages忽略掉下划线开头的文件和文件夹
```

## 撰写文档

到这里已经搭建起来了一个基本的框架，下面就是来填充丰富的功能和撰写你自己的文档。

- [定制化](md/custom.md)  如何更改封面、logo、侧边栏、导航栏等基础功能。
- [插件](md/plugins.md)  一些具有使用功能的插件安装，包括katex公式、图表、评论系统等。
- [文档助手](md/helper.md)  基于官方的文档助手，结合安装的插件，扩充的文档语法。

## 基于GitHub Pages托管

### 上传到git仓库

一切都准备好了，现在将项目上传到托管仓库，以GitHub为例。

```bash
cd <Project Path>
git add *  #将所有文件添加到暂存区
git commit -m "仓库提交注释"  
git push -f orgin main #上传到远程仓库并合并代码，`-f`强制推送
```

### 获取访问链接

在项目仓库中找到`⚙️Setting➔Pages➔Source`。

<img src="https://linley.oss-cn-shanghai.aliyuncs.com/typora_image/quickstart2022-03-09-21-44-25.png" alt="quickstart2022-03-09-21-44-25" width="" height="">