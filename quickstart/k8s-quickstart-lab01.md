# 实验一 使用 Docker 内置的 Kubernetes 集群

## 1. 安装 Docker Desktop 

### 1.1 MAC 环境下安装 Docker for MAC

### 1.2 Windows 10 环境下安装 Docker for Windows

```console
$ git clone -b 1.0 https://github.com/maping/python-voting-web-app.git
```
>说明：-b 1.0 表示代码分支 1.0。

查看 python-voting-web-app\docker-compose.yaml 中的端口，默认使用8080 端口。
```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    container_name: azure-vote-back
    ports:
        - "6379:6379"

  azure-vote-front:
    build: ./azure-vote
    image: azure-vote-front
    container_name: azure-vote-front
    environment:
      REDIS: azure-vote-back
    ports:
        - "8080:80"
 ```

## 2. 使用 docker-compose 命令构建 Docker 镜像
```console
$ cd python-voting-web-app
$ docker-compose up --build -d
```
>说明：--build 参数表示启动容器前，重新构建镜像；-d 表示 Detached mode，即后台启动容器。

```console
$ docker images
REPOSITORY                                       TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                 latest              05806549d652        7 seconds ago       946MB
redis                                            latest              5958914cc558        4 weeks ago         94.9MB
tiangolo/uwsgi-nginx-flask                       python3.6           1947008ccef7        5 weeks ago         945MB
```
```console
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                           NAMES
c83cb78e3eaf        redis               "docker-entrypoint.s…"   19 seconds ago      Up 17 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
81b97f470dcf        azure-vote-front    "/entrypoint.sh /sta…"   19 seconds ago      Up 17 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
```

## 3. 在本地测试应用程序
访问 http://localhost:8080
![image](./images/aks-tutorial-lab01-01.png)

## 4. 停止并删除容器
```console
$ docker-compose stop
$ docker-compose down
```
