---
title: "Docker Tip"
date: 2020-05-05T15:53:39+08:00
tags: [Docker, 知识库]
categories: [技术]
url: "/2020/05/05/docker-tip.html"
toc: true
---


快速删除docker镜像，容器等。

[AviorX]^(安全可靠的企业应用)
<!--more-->

## 列出所有的容器 ID
```
docker ps -aq
```

## 停止所有的容器
```
docker stop $(docker ps -aq)
```

## 删除所有的容器
```
docker rm $(docker ps -aq)
```

## 删除所有的镜像
```
docker rmi $(docker images -q)
```

## 复制文件
```
docker cp container:/opt/file.txt /opt/local/
docker cp /opt/local/file.txt container:/opt/
```

## 进入容器 .
```
docker exec -it xxx bin\sh
```

转载地址: [https://colobu.com/2018/05/15/Stop-and-remove-all-docker-containers-and-images/](https://colobu.com/2018/05/15/Stop-and-remove-all-docker-containers-and-images/)
