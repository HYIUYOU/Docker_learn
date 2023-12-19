# Docker 学习记录

## 1. Docker 镜像

### 1. Overview

docker镜像类似一个**只读模板**，通过他可以创建docker容器

镜像有多种生成方法：

- 从无到有创建镜像
- 下载并使用别人创建好的镜像
- 从现有的镜像上创建新的镜像

可以把创建镜像的步骤写在一个文件中，这个文件称为**Dockerfile**。

通过：

```shell
docker build <dockerfile>
```

来快速构建出docker镜像。

删除镜像

```shell
docker rmi <image>
```



### 2. base镜像

base镜像：不依赖其他镜像，从scratch构建，其他镜像可以以此为基础进行扩展。因此base镜像通常时linux的各种发行版本的镜像，如ubuntu, centos等。

#### 构建base镜像的方法

1. 构建base镜像的第一个方法：docker pull

   ```shell
   docker pull centos
   
   docker images #查看当前的镜像
   ```

2. 构建base镜像的第二个方法： Dockerfile

   - 写Dockerfile，通过离线的centos-docker的tar包进行安装

   ```txt
   FROM scratch
   ADD CentOS-7-docker.tar.xz /
   CMD ["/bin/bash"]
   ```

   - docker build 进行构建

   ```shell
   docker build -f hello-DF -t hello:1.0 .
   ```

   - 通过docker run进入交互场景

   ```shell
   docker run -it hello:1.0
   # -it 交互模式运行容器
   ```

   

   



## 2. docker容器

==docker容器就是docker镜像运行的实例。==

- 镜像是软件构建和打包的阶段
- 容器时启动和运行的阶段







## 3. Docker 命令

## 0. 查看镜像

```shell
docker images
```

## 1.查看当前运行的镜像

```shell
docker ps
```

### 2.交互式运行镜像

[教程](https://www.bilibili.com/video/BV1X84y1t7R8/?spm_id_from=333.337.search-card.all.click&vd_source=39af172533d3663527b92ccaa287e4d6)

```shell
docker run -it ubuntu
```

> 在使用这个命令后，对该镜像所有的操作将会在退出后自动格式化，不会被保存。
>
> 先使用
>
> ```shell 
> docker commit <容器 names> <另存为新的镜像的名字 首字母不能大写>
> ```
>
> 再退出

