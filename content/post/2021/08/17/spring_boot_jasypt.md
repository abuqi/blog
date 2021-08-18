---
title: "SpringBoot配置文件加密 2021/08/17"
tags: [spring,jasypt]
categories: [技术]
date: 2021-08-17T14:22:35+08:00
url: "/2021/08/17/Spring_boot_jasypt.html"
toc: true
---

保护Spring Boot 配置中的敏感信息

<!--more-->


参考[Spring Boot 配置中的敏感信息如何保护？](https://juejin.cn/post/6996837932141133832)

## 问题:

1. 执行[mvn jasypt:encrypt]时,出现[Error Encrypting: Unable to read file xxxx]的错误
```
  添加下面参数 
  -Djasypt.plugin.path="file:D:\Projects\xxxxx\application.yml"
```

2. 加密密钥如果放入application.yml中, 还是有泄露的风险
```
  在Jar的启动参数中加入下面参数
  -Djasypt.encryptor.password=加密密钥
  
```