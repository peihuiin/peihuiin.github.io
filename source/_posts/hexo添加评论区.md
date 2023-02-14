---
title: Hexo添加评论区
date: 2023-02-15 00:09:02
categories: Blog
tags:
    - Hexo
    - Blog
---

## Valine

官网：https://leancloud.cn/

1、`应用`→`创建应用`，创建完成后在`设置`→`应用Keys`中获取AppID和AppKey

2、在主题配置文件中指定Valine为评论模块

```yaml
post:
  comments:
    enable: true
    type: disqus
```

3、配置Valine评论模块参数

```
valine:
  appId: 								#Appid
  appKey: 								#AppKey
  path: window.location.pathname
  placeholder: '支持使用Markdown语法'		#评论区默认填充文字
  avatar: mp							#默认显示头像
  meta: ['nick', 'mail', 'link']		#显示评论者属性
  requiredFields: []
  pageSize: 10							#每页显示评论数
  visitor: true							#文章访问量统计
  lang: 'zh-CN'							#自定义语言
  highlight: true						#代码高亮
  recordIP: true						#是否记录评论者IP
  serverURLs: ''
  emojiCDN:
  emojiMaps:
  enableQQ: false
```

4、Valine需要使用[Gravatar](http://cn.gravatar.com/) 自定义评论列表头像；

5、在Valine应用`数据存储`→`结构化数据`→`Comment`内管理评论；