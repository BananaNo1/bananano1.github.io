---
title: docker使用mongoDb
date: 2018-12-04 13:55:54
tags: [docker,数据库,mongodb]
categories: 数据库
---

#### 安装mongodb

1. 从docke hub上获取下载地址

   ![下载地址](docker使用mongoDb\TIM截图20181204160443.png)

   > 默认版本信息为(latest) 如需其他版本也可在docker hub中查找 

#### 运行镜像

**基本执行**

> ```
> docker run --name mongo -d mongo:tag
> --name 别名
> -d 后台执行
> mongo:tag：下载的mongodb版本 默认为latest
> 默认端口:27017
> ```

**持久化**

在宿主机上创建一个数据存储目录（/etc/data/mongodb），将其映射到容器中的目录中。将数据库文件存储在主机系统，便于主机系统上的工具和应用程序访问文件

> mkdir -p /etc/data/mongodb
>
> docker run --name mongo -v /etc/data/mongodb:/data/db  -d mongo

 **坑**: 使用命令 docker ps 查看运行容器  发现容器没有启动

![查看](docker使用mongoDb\TIM截图20181204162115.png)

使用命令docker ps -a 查看 发现容器已经退出 

使用命令docker logs (containerId) 查看日志信息

![](docker使用mongodb\TIM截图20181204162659.png) 

提示权限不够  在运行命令加上  --privileged=true 

```
docker run --name mongo -v /etc/data/mongodb:/data/db --privileged=true -d mongo
```

如果提示容器名已在使用（is already in use ）docker rm mongo

容器启动后，运行如下命令以管理员进入终端命令行

```
docker exec -it mongo mongo admin 
```

可以看到  /etc/data/mongodb 目录下已存在数据