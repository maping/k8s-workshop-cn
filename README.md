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
- [Azure Kubernetes Service](https://docs.microsoft.com/zh-cn/azure/aks/)
- [Azure Container Registry](https://docs.microsoft.com/zh-cn/azure/container-registry/) 
    - [Azure Container Registry 身份验证](https://docs.microsoft.com/zh-cn/azure/container-registry/container-registry-auth-aks)
- [Azure DevOps Projects](https://docs.microsoft.com/zh-cn/azure/devops-project/)   
    - [使用 Azure DevOps Projects 将 ASP.NET Core 应用部署到 AKS](https://docs.microsoft.com/zh-cn/azure/devops-project/azure-devops-project-aks?toc=%2Fen-us%2Fazure%2Fdevops-project%2Ftoc.json&bc=%2Fen-us%2Fazure%2Fbread%2Ftoc.json)
