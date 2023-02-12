---
title: GitHub搭建博客
date: 2023-02-12 01:53:00
categories: Blog
tags:
    - GitHub
    - Blog
    - Hexo
comment: 'disqus'
index_img:
---

<blockquote alt="success"><p>
    工具准备：Node.js、Hexo、GitHub、Git。
    </p></blockquote>

## 创建GitHub站点

[GitHub官网](https://github.com/)

1、使用GitHub用户名创建仓库，命名格式：*user*.github.io，默认分支为**master**；（user必须为GitHub的用户名）

2、在*user*.github.io仓库中新建index.html文件，文件内容如：（一般来说，需要仓库名填写正确+仓库非空，仓库才会对外发布）

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>网站测试</title>
</head>

<body>
     <h1>成功！！！可以进行下一步了</h1>
</body>

</html>
```

3、在仓库“Settings”→“Pages”页面可看到如下提示，则仓库发布正常，点击`https://user.github.io/`可跳转到网站首页；

```shell
Your site is live at https://user.github.io/
Last deployed by @user user 12 minutes ago
```

## 安装[Hexo](https://hexo.io/zh-cn/)

Hexo是一个快速、简洁且高效的博客框架。Hexo使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他渲染引擎）解析文章，能够在几秒内利用靓丽的主题生成静态网页。

1、安装[Node.js](https://nodejs.org/en/)，选择左边的LTS版本（长期支持版本）；

2、安装Hexo，CMD中执行`npm install hexo-cli -g`；

3、创建博客文件夹，在期望路径下打开Git bash，执行以下命令；

```shell
hexo init <folder>
cd <folder>
npm install
hexo server
```
详细操作参考：[Hexo搭建博客](https://sslin.online/2023/02/11/Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2/)

## 保证本地可访问GitHub仓库

1、配置GitHub用户名、邮箱；

```shell
git config --global user.name “用户名”
git config --global user.email “邮箱”
```

2、配置秘钥，使用命令`ssh-keygen -t rsa`生成秘钥，并将公钥添加到GitHub账户；

## 部署网站

1、网站目录下打开Git Bash安装发布插件，安装命令`npm install hexo-deployer-git --save`；

2、修改博客配置文件`_config.yml`的deploy部分；

```yaml
deploy:
    type: git
    repository: ssh://git@github.com/user/user.github.io.git
    brandh: master
    messge:
```

3、上传博客代码

```shell
hexo s
hexo clean
hexo g
hexo d
```

4、博客网站搭建完成了，通过`https://user.github.io/`即可访问博客。

## CNAME、README.md等文件丢失

当你重新提交博客代码后会发现以前其它代码消失了。解决方法是将非md文件放置在`source`文件夹下，hexo每次提交代码时会将这里的文件复制到`public`目录后提交到GitHub仓库。

由于md文件会被转换为html。因此，每次提交代码时需要在生成（`hexo g`）、上传（`hexo d`）之间，将md文件手动复制到`public`目录。

## 绑定域名

如果你觉得域名`user.github.io`太丑且拥有自己的域名的话，也可以将自己的域名绑定到`user.github.io`，实现通过自己的域名访问`user.github.io`。

域名配置分为：CNAME、A记录。互联网中用IP地址表示一个网站的访问地址，A记录实现用一个容易识别的字符串（域名）表示IP地址，CNAME实现一个域名映射到另一个域名。以百度网站举例，最原始用户只能通过`36.152.44.96`地址访问，添加A记录后能够通过`www.baidu.com`，而添加CNAME后又能通过`www.baidu2.com`访问。

- A记录：www.baidu.com → 36.152.44.96
- CNAME：www.baidu2.com → www.baidu.com

我的域名是在[阿里云](https://www.aliyun.com/)上申请的，所以需要上阿里云网站添加A记录和CNAME。

1、CMD上ping `user.github.io`获取网站IP；

2、在阿里云域名解析配置中添加以下规则：

```
A：域名 → 网站IP
CNAME：www.域名 → user.github.io
```

3、在GitHub项目中新建CNAME文件（无后缀），内容为：

```
域名
www.域名
```

4、配置完成，浏览器上通过`域名`、`www.域名`、`user.github.io`都能够访问博客了。

## 在线编辑博文

Hexo本地搭建博客后，用户每次编辑博文都需要重新将源码提交到GitHub，并编译提交网站源码。为了提高Hexo编辑博文的易用性，我们可以通过[GitHub Actions](https://docs.github.com/zh/actions/learn-github-actions)实现博客的自动编译发布，即我们每次提交博客源码或GitHub上更新博文后，GitHub Actions自动触发博客的编译发布。

1、添加秘钥用于deploy过程操作GitHub仓库；

使用命令`ssh-keygen -t rsa -b 4096 -C "$(git config user.email)" -f gh-pages -N ""`生成`gh-pages`私钥、`gh-pages.pub`公钥；

仓库配置`Deploy Keys`→`Add deploy key`添加 `gh-pages.pub`公钥，name为`public key of ACTIONS_DEPLOY_KEY`，并在新建deploy key后点击`approve`按钮。

仓库配置`secrets and variables`→`Actions`→`New repository secret` ，name为`ACTIONS_DEPLOY_KEY`（后续yml文件中使用）。

2、新建`.github/workflows/pages.yml`文件自定义GitHub Actions操作，内容参照[Hexo指导文档](https://hexo.io/zh-cn/docs/github-pages)。

```yaml
name: Pages

on:
  push:
    branches:
      - sources # default branch

jobs:
  pages:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Use Node.js 19.x
        uses: actions/setup-node@v2
        with:
          node-version: "v19.6.0"
      - name: Cache NPM dependencies
        uses: actions/cache@v2
        with:
          path: node_modules
          key: ${{ runner.OS }}-npm-cache
          restore-keys: |
            ${{ runner.OS }}-npm-cache
      - name: Install Dependencies
        run: npm install
      - name: Build
        run: npm run build
      - name: Setup Git Infomation
        run: |
          git config --global user.name 'name'
          git config --global user.email 'email'
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          deploy_key: ${{ secrets.ACTIONS_DEPLOY_KEY }}
          user_name: ${user.name}
          user_email: ${user.email}
          # 获取提交文章源码时的commit message，作为发布gh-pages分支的信息
          commit_message: ${{ github.event.head_commit.message }}
          full_commit_message: ${{ github.event.head_commit.message }}
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public

```
3、在博文底部添加编辑文章按钮，支持跳转到GitHub编辑界面。编辑`themes`→`主题文件夹`→`layoutpost.ejs`文件，在`markdown-body`模块下添加：

```html
<div style="text-align: center ">
<a href="https://github.com/user/user.github.io/edit/sources/source/<%- page.source %>" target="_blank">编辑文章✏</a>
</div>
```
