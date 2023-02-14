---
title: 初始Django
date: 2023-02-14 22:06:59
categories: Django
tags: Django
---

# 初识Django

Django 是一个由 Python 编写的一个开放源代码的 Web 应用框架（用于进行Web开发的一套软件架构）。Django基于MTV模型开发，本质上和MVC模型是一样的（Model 模型、View 视图、Controller 控制器）。

| MVC模型                                                      | MTV模型                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| @Model，功能实现，负责业务对象和数据库的映射（ORM）；<br />@View，图形界面，负责和用户交互；<br />@Controller，处理、转发请求； | @Model，功能实现，负责业务对象和数据库的映射（ORM）；<br />@Template，负责如何把页面（html）展示给用户；<br />@View，用户交互，调用Model、Template； |
| ![img](/img/Django (3).png) | ![img](/img/Django (1).png) |



## 1. Django环境搭建

- 通过pip安装django；

```shell
方法1：
pip --default-timeout=100 install -U django

方法2：
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple django

//不建议直接使用 pip install django，国内网速太慢会导致下载超时报错。
```

- 能够查看Django版本则安装成功；

```python
C:\Users\13960>python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import django
>>> django.get_version()
'4.1.4'
```

- 在D:\Django路径下创建Django项目**HelloWorld**，并启动服务器，Django项目文件结构如下：
  - **HelloWorld:** 项目的容器；
    - **__init__.py:** 一个空文件，告诉 Python 该目录是一个 Python 包；
    - **asgi.py:** 一个 ASGI 兼容的 Web 服务器的入口，以便运行你的项目；
    - **settings.py:** 该 Django 项目的设置/配置；
    - **urls.py:** 该 Django 项目的 URL 声明; 一份由 Django 驱动的网站"目录"；
    - **wsgi.py:** 一个 WSGI 兼容的 Web 服务器的入口，以便运行你的项目；
  - **manage.py:** 一个实用的命令行工具，可让你以各种方式与该 Django 项目进行交互；

```powershell
PS D:\Django> django-admin startproject HelloWorld
PS D:\Django> cd .\HelloWorld\
PS D:\Django\HelloWorld> python manage.py runserver 0.0.0.0:8000
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
December 11, 2022 - 13:00:05
Django version 4.1.4, using settings 'HelloWorld.settings'
Starting development server at http://0.0.0.0:8000/
Quit the server with CTRL-BREAK.
[11/Dec/2022 13:00:40] "GET / HTTP/1.1" 200 10681
[11/Dec/2022 13:00:40] "GET /static/admin/css/fonts.css HTTP/1.1" 200 423
[11/Dec/2022 13:00:40] "GET /static/admin/fonts/Roboto-Bold-webfont.woff HTTP/1.1" 200 86184
[11/Dec/2022 13:00:40] "GET /static/admin/fonts/Roboto-Regular-webfont.woff HTTP/1.1" 200 85876
[11/Dec/2022 13:00:40] "GET /static/admin/fonts/Roboto-Light-webfont.woff HTTP/1.1" 200 85692
Not Found: /favicon.ico
[11/Dec/2022 13:00:40] "GET /favicon.ico HTTP/1.1" 404 2114
```

- 浏览器能够成功打开**http://127.0.0.1:8000/**页面，则服务器正常启动；

![image-20221211130557213](/img/Django (2).png)
