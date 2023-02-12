---
title: Typora使用手册
date: 2023-02-11 04:25:45
categories: Markdown
tags:
   - Markdown
   - Typora
---

# Typora使用手册

## 快捷键汇总

[Typora的Markdown语法](https://support.typoraio.cn/zh/Markdown-Reference/)

| 样式            | Typora快捷键                           | Markdown语法                                                 |
| --------------- | -------------------------------------- | ------------------------------------------------------------ |
| 目录            |                                        | [toc]                                                        |
| H₁ 一级标题     | Ctrl +                                 | # + Space                                                    |
| H₂ 二级标题     | Ctrl + 2                               | ## + Space                                                   |
| H₃ 三级标题     | Ctrl + 3                               | ### + Space                                                  |
| H₄ 四级标题     | Ctrl + 4                               | #### + Space                                                 |
| H₅ 五级标题     | Ctrl + 5                               | ##### + Space                                                |
| H₆ 六级标题     | Ctrl + 6                               | ###### + Space                                               |
| 正文            | Ctrl + 0                               | /                                                            |
| 有序列表        | Ctrl + Shell + [                       | 1. + Space                                                   |
| 无序列表        | Ctrl + Shell + ]                       | - + Space                                                    |
| 任务列表        |                                        | - + Space + [ + Space + ] + Space + 文字                     |
| *斜体*          | Ctrl + I                               | * + 文字 + *                                                 |
| **粗体**        | Ctrl + B                               | ** + 文字 + **                                               |
| <u>下划线</u>   | Ctrl + U                               | <u> + 文字 + </u>                                            |
| ~~删除线~~      | Ctrl + Shell + 5                       | ~~ + 文字 + ~~                                               |
| ==高亮==        |                                        | == + 文字 + ==                                               |
| 引用/提示块     | Ctrl + Shell + Q                       | > + Space<br />或<blockquote><p><br/>    文字<br/>    </p></blockquote> |
| 分割线          | --- + Space                            | --- + Space                                                  |
| 代码块          | *Ctrl + Shell + K*（Ctrl + Shell + C） |                                                              |
| 公式块          | Ctrl + Shell + B                       |                                                              |
| 插入超链接      | Ctrl + K                               | [网址名称] + (网址)                                          |
| 插入图片        | Ctrl + Shell + I                       | ! + [图片名称] + (图片路径)                                  |
| <u>插入表格</u> | Ctrl + T                               | \| + Space +  表头1 + Space + \| + Space +  表头2 + Space + \| |
| <sup>上标</sup> |                                        | [^文字] ==（表格内不可用）==<br/>或 \<sup> + 文字 + \</sup>  |
| ~下标~          |                                        | ~ + 文字 + ~ <br/>或 \<sub> + 文字 + \</sub>                 |
| <kbd>方框</kbd> |                                        | \<kbd> + 文字 + \</kbd>                                      |
| 表情:smile:     |                                        | : + 表情名称 + : ==（键入:时Typora会出现提示）==             |

> 当期望字符单纯作为显示为字符时，使用转义符 **“\”**

<blockquote alt="warn"><p>
    引用（提示块）可通过 alt="" 置为“success”、"warn"、"danger"类型。
    </p></blockquote>



## 格式自定义


- **修改快捷键**

[快捷键指导手册](https://support.typora.io/Shortcut-Keys/#change-shortcut-keys)

打开安装路径下的**/conf/conf.user.json**文件，在**"keyBinding"**属性中添加目的动作及快捷键，如修改插入代码块的快捷键为Ctrl + Shell + C

```json
  "keyBinding": {
    "Code Fences": "Ctrl+Shift+C"
    // All other options are the menu items 'text label' displayed from each typora menu
  },
```

- **图片左对齐**

设置路径：文件→偏好设置→外观→打开主题文件，在所有CSS文件尾部追加以下代码。

```css
p .md-image:only-child {
    width: auto;
    text-align: left;
}
```

## 在线图片

![](/img/typora%20(2).png)

​		Typora使用以上规则存在图片时，如果复制Typora文件中的图片到其它软件上时会复制失败，这是因为Typora上保存的是图片的本地地址，其它软件无法直接读取。

​		解决方法是将图片保存在云端，Typora存放的是云链接。这里使用Gitee+PicGo进行图片云端备份，操作步骤如下：

1. 在Gitee中新建仓库用于存放图片；
   ![](/img/typora%20(4).png)
2. 在仓库“管理”选项→“基本信息”中，将仓库设置为**开源**方便共享图片；
   ![](/img/typora%20(5).png)
3. 生成私人令牌（个人头像→设置→私人令牌→生成新令牌）后续PicGo中需要用到；
   ![](/img/typora%20(6).png)
4. 安装Node.js插件（安装PicGo插件gitee-uploader依赖此插件，下载地址 http://nodejs.cn/download/，**安装路径不为C盘且选择仅为我安装**）；
5. 设置Node.js环境变量（系统属性→环境变量→“Path变量”），Path下新增Node.js安装**文件夹**路径；
6. 打开cmd，使用 **node -v**、**npm -v** 命令能够查询版本即为Node.js安装成功；
7. 安装PicGo（下载地址 https://github.com/Molunerfinn/PicGo）；
8. 管理员模式打开cmd，进入PicGo安装文件夹目录，执行命令 **npm install picgo-plugin-gitee-uploader** 安装gitee图床插件；
9. 重新打开PicGo可以在 图床设置中看到gitee选项，配置如下；
   ![](/img/typora%20(1).png)
10. Typora配置PicGo，配置如下：

问题记录：
404问题：
	picgo-plugin-gitee-uploader、picgo-plugin-gitee插件存在交替失效的问题，某个插件无法使用时切换到另一个插件即可。

403问题：

​	貌似因为本地电脑无法ssh通gitee，后续验证。

c6995dcea968e471d68eddc987720426

## 附件

[Typora-v1.4.8-中文安装包](.\Typora1.4.8中文直装版.exe)

[常用主题](https://github.com/muggledy/typora-dyzj-theme)（[主题预览](https://typora-dyzj-theme.vercel.app/)、[安装包](./typora-dyzj-theme-master.zip)）

[Node.js安装包](‪./node-v16.18.1-x64.msi)

