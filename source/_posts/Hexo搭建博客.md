---
title: Hexo搭建博客（Fluid 主题）
date: 2023-02-11 04:45:45
categories: Blog
tags:
    - Hexo
    - Blog
---

## 运行环境准备

安装[Git](https://git-scm.com/download/win)

安装[Node.js](https://nodejs.org/en/)

安装Hexo

```shell
npm install -g hexo-cli
```

## 建站

```shell
hexo init <folder>
cd <folder>
npm install
hexo server
```

> 安装过程中开启VPN能够加速安装过程。

## 指定主题

安装步骤：

1. 将博客网站文件**fluid**放置在**theme**文件夹下
2. 将**_config.yml**中的theme名称修改为：**fluid**
3. 设置博客语言为 zh-CN

## 创建关于页（首次使用）

```shell
hexo new page about
```

创建成功后修改 `./source/about/index.md`，必须添加 `layout` 属性且值为 **about**。

```markdown
---
title: 标题
layout: about
---

这里可以写正文，支持 Markdown, HTML
```

## 博文添加

在`./source/_posts`文件夹下添加**.md**文件，格式如下：

```html
---
title: Hello World              // 文章标题
date: 2023-02-11 03:10:45       // 创建时间
tags: hello                     // 文章标签
categories: txt                 // 文章分类
index_img:                      // 首页文章的封面图
banner_img:                     // 文章页顶部大图
---
<-- 正文内容 -->
```

图片存放在`./themes/fluid/source/img`下，引用时使用绝对路径`/img/img_name`。

## 配置自定义

将主题`_config.yml`配置文件放置在主题文件夹之外，避免更新主题文件时丢失自定义配置。

方法：将fluid主题`_config.yml`配置文件复制到博客目录下，并重命名为创建 `_config.fluid.yml` 。

## 常用命令汇总

☛ hexo init [folder]，新建网站

☛ hexo new [name]，新建文章

☛ hexo server，运行博客网站

☛ hexo clean，清除缓存文件 (`db.json`) 和已生成的静态文件 (`public`)

☛ hexo generate，生成静态网站文件

☛ hexo deploy，部署网站

☛ hexo version，查看hexo版本

## 指导文章

https://hexo.io/zh-cn/docs/

https://github.com/fluid-dev/hexo-theme-fluid

https://hexo.fluid-dev.com/docs/