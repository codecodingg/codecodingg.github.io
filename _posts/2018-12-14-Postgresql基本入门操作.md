---
layout:     post
title:      Postgresql 基本入门操作
subtitle:   Postgresql 基本操作
date:       2018-12-14
author:     Code Coding
header-img: 
catalog: true
tags:
    - Postgresql
---

# 前言

Postgresl数据安装,新建用户,新建数据库操作.

# 安装
1. 安装Postgresql服务器
```sh
    sudo apt install postgresql
```
- 正常完成安装以后, 会默认生成一个postgres的数据用户和一个postgres数据库. 数据库的默认端口是:5432

# 新建数据库用户和数据库
## 通过postgres用户来创建新的数据用户和数据
1. 切换到postgres用户
    ```sh
        sudo su - postgres
    ```
2. 登录到Posgresql控制台
    ```sh
        psql
    ```
3. 创建一个叫 newdbuser 的数据用户
    ```sql
        CREATE USER newdbuser WITH PASSWORD 'user_password';
    ```
4. 创建一个叫 testdb 的数据库
    ```sql
        CREATE DATABASE testdb OWNER newdbuser;
    ```
5. 把数据库 testdb 的全部权限赋予 newdbuser用户
    ```sql
       GRANT ALL PRIVILEGES ON DATABASE testdb to newdbuser;
    ```
6. 退出控制台
    ```sql
        \q
    ```
## 登录数据
1. 以新建的用户名的名义登录数据
    ```sh
        psql -U newdbuser -d testdb -h 127.0.0.1 -p 5432
    ```
    - -U: 数据库用户名
    - -d: 需要登录的数据库
    - -h: 服务器
    - -p: 数据库端口

2. 如果当前用户是linux用户也是postgresql用户,则可以通过简写不通过密码的状态登录数据,例如linux和postgresql都有用户newdbuser, 在linux登录 newdbuser 的状态下这样登录 testdb 数据库
    ```sql
    psql testdb
    ```

# Postgresql相关的控制台命令
- \l: 查看所有的数据库
- \d: 列出当前数据库的所有表
- \c [databasename]: 连接其他的数据
- \d [tablename]: 列出某张表的结构
- \conninfo: 列出当前数据和链接的信息

# 数据库相关操作
1. 创建新表
    ```sql
        CREATE TABLE user_info(name VARCHAR(10), sign_date DATE);
    ```
2. 在表中插入数据
    ```sql
        INSERT INTO user_info(name, sign_date) VALUES ('WOW', '2018-12-14');
    ```
3. 查询数据
    ```sql
        SELECT * FROM user_info;
    ```
4. 更新数据
    ```sql
        UPDATE user_info SET name='HOS' WHERE name='WOW';
    ```
5. 删除数据
    ```sql
        DELETE FROM user_info WHERE name='HOS';
    ```
6. 添加栏位
    ```sql
        ALTER TABLE user_info ADD passw VARCHAR(20);
    ```
7. 更新数据结构
    ```sql
        ALTER TABLE user_info ALTER name SET NOT NULL;
    ```
8. 修改字段名字
    ```sql
        ALTER TABLE user_info RENAME COLUMN name TO user_name;
    ```
9. 删除字段
    ```sql
        ALTER TABLE user_info DROP COLUMN passw;
    ```
10. 数据表改名
    ```sql
        ALTER TABLE user_info RENAME TO other_user_info;
    ```
11. 删除数据表
    ```sql
        DROP TABLE user_info;
    ```

# 文章参考
- [PostgreSQL新手入门](http://www.ruanyifeng.com/blog/2013/12/getting_started_with_postgresql.html)