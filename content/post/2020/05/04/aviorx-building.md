---
title: "Aviorx 构建"
date: 2020-05-04T22:46:20+08:00
tags: [aviorx]
categories: [技术]
url: "/2020/05/04/aviorx-building.html"
toc: true
---


基于docker-compose构建Aviorx服务站点.

[AviorX]^(安全可靠的企业应用)
<!--more-->

## 环境

1. JDK 1.8
2. CentOS 7
3. docker 1.13.1
4. docker-compose 1.24.1

## 问题

1. docker 不能启动mysql容器, 对挂载的目录没有权限。 Permission denied
原因： centos7中安全模块selinux把权限禁掉了。
解决方法：添加linux规则，把要挂载的目录添加到selinux白名单
```
# 更改安全性文本的格式如下
chcon [-R] [-t type] [-u user] [-r role] 文件或者目录

选顷不参数： 
-R  ：该目录下的所有目录也同时修改； 
-t  ：后面接安全性本文的类型字段，例如 httpd_sys_content_t ； 
-u  ：后面接身份识别，例如 system_u； 
-r  ：后面街觇色，例如 system_r
```
执行
```
chcon -Rt svirt_sandbox_file_t /opt/xxx/yyyy/data/
```

2. 执行 docker-compose up -d 后, nacos不能正常访问.错误日志显示,mysql数据库不能连接.
 初步怀疑是docker的启动顺序造成的.  nacos启动时,mysql数据库还未能正常启动.
 查询工单未能发现相同问题.
 使用docker-compose build命令后,nacos能正常访问. 但是,mysql容器下面的xxl-job-admin的日志中, 仍然有数据库不能访问的信息. (以后要详细调查)

3. 核心服务[cloud-upms]不能启动.
 发现日志中包含下列信息
```
 No typehandler found for property authorizedGrantTypes
```
根据工单系统中[810](https://git.pig4cloud.com/pig/pigx/issues/810)中描述,添加[application-dev.yml]中下列内容
```
  type-handlers-package:  com.xxx.yyy.common.data.handler
```

4. 使用heidisql链接mysql时,提示找不到验证工具【caching_sha2_password 】的错误。
原因：Mysql8.0使用了caching_sha2_password 的认证方式,而链接工具不支持。
解决方案：把认证方式修改成原来的mysql_native_password
```
ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'xxxxxx';
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'xxxxxx';
FLUSH PRIVILEGES;
```

## 然后

未完待续...