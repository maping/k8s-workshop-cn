# Kubernetes 从入门到精通

# 实验目录
- [Kubernetes 快速上手](./quickstart/k8s-quickstart-index.md)
- [Kubernetes 基础教程](./tutorial/k8s-tutorial-index.md)
- [Kubernetes 高级教程](./advanced/k8s-advanced-index.md)

# 常用 Docker 命令参考
## 停止所有容器
```console
$ for id in $(docker ps -q); do docker stop $id; done
```
## 删除所有容器
```console
$ for id in $(docker ps -aq); do docker rm $id; done
```
## 删除所有 Docker 镜像
```console
$ for id in $(docker images -aq); do docker rmi $id; done
$ docker rmi `docker images -aq`
```
## 删除所有没有 Tag 的 Docker 镜像
```console
$ docker rmi $(docker images | grep none | awk '{ print $3}')
```
# 参考文档
- [Kubernetes Github Project](https://github.com/kubernetes)
    - [Kubernetes Dashboard Github Repo](https://github.com/kubernetes/dashboard)
