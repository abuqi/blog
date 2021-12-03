---
title: "Github使用tokens"
tags: [github]
categories: [技术]
date: 2021-12-03T16:38:59+08:00
url: "/2021/12/03/personal_access_tokens.html"
toc: true
---

Github使用Personal access tokens的方法

<!--more-->

## 创建Token
1. 打开Github的[Personal access tokens](https://github.com/settings/tokens).
![图片](/blog/images/2021/164620.png)
2. 点击[Generate new token]按钮. 
   ```
   [Note] 写入这个token的目的
   [Expiration] 选择过期时间
   [Select scopes] 部分根据需求选取权限
   ```
![图片](/blog/images/2021/165720.png)
3. 点击[Generate token]按钮
![图片](/blog/images/2021/170256.png)
4. 复制生成的token字符串。**只会显示一次**

## 修改本地git配置信息
1. 找到本地clone的仓库，找到隐藏目录.git，打开config文件。
![图片](/blog/images/2021/170815.png)
2. 修改URL，格式为

> https://*用户名*:token字符串@github.com/*用户名*/xxx.git

![图片](/blog/images/2021/170957.png)

