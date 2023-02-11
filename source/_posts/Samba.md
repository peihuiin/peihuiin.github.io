---
title:  Samba实现Ubuntu共享文件夹
date: 2023-02-11 04:45:45
categories: Ubuntu
tags:
   - Samba
   - Ubuntu
---

1. 更新软件包

   ```shell
   sudo apt-get upgrade
   sudo apt-get update
   sudo apt-get dist-upgrade
   ```

2. 安装Samba服务器

   ```shell
   sudo apt-get install samba samba-common
   ```

3. 添加Samba用户

   ```shell
   sudo smbpasswd -a root
   ```

4. 修订配置文件
   vi /etc/samba/smb.conf

   ```shell
   [samba]
      comment = share folder
      browseable = yes
      path = /
      create mask = 0700
      directory mask = 0700
      valid users = root
      force user = root
      force group = root
      public = yes
      available = yes
      writable = yes
   ```

5. 重启Samba服务器

   ```shell
   sudo service smbd restart
   ```

6. 更新防火墙规则（Ubuntu20需要执行）

   ```shell
   sudo ufw allow samba
   ```

