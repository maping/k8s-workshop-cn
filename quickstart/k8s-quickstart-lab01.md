# 实验一 使用 Docker 内置的 Kubernetes 集群

## 1. 安装 Docker Desktop 

### 1.1 MAC 环境下安装 Docker for MAC

### 1.2 Windows 10 环境下安装 Docker for Windows

## 2. 启动 Docker 内置的 Kubernetes 集群
点击 Docker 鲸鱼图标 -> Preferences... -> Kubernetes，勾选
- Enable Kubernetes
- Deploy Docker Stacks to Kubernetes by default
- Show system containers(advanced)
点击 Apply，Docker 会重新启动，同时启动内置的 Kubernetes 集群。
![image](./images/k8s-quickstart-lab01-01.png)

## 3. 确认 Docker 内置的 Kubernetes 集群工作正常
查看自动安装的 Kubernetes 相关容器
```console
$ docker container ls --format "table{{.Names}}\t{{.Image }}\t{{.Command}}"
NAMES                                                                                                                   IMAGE                            COMMAND
k8s_compose_compose-api-6757787584-d7zsl_docker_9ddb62e0-750f-11e9-9c87-025000000001_0                                  docker/kube-compose-api-server   "/api-server --kubec…"
k8s_compose_compose-74649b4db6-zclv4_docker_21021466-7464-11e9-a5e0-025000000001_0                                      docker/kube-compose-controller   "/compose-controller…"
k8s_sidecar_kube-dns-86f4d74b45-7zr8j_kube-system_c3658298-7237-11e9-bffb-025000000001_0                                6f7f2dc7fab5                     "/sidecar --v=2 --lo…"
k8s_dnsmasq_kube-dns-86f4d74b45-7zr8j_kube-system_c3658298-7237-11e9-bffb-025000000001_0                                c2ce1ffb51ed                     "/dnsmasq-nanny -v=2…"
k8s_kubedns_kube-dns-86f4d74b45-7zr8j_kube-system_c3658298-7237-11e9-bffb-025000000001_0                                80cc5ea4b547                     "/kube-dns --domain=…"
k8s_kube-proxy_kube-proxy-vpg7m_kube-system_c338829d-7237-11e9-bffb-025000000001_0                                      7387003276ac                     "/usr/local/bin/kube…"
k8s_POD_compose-api-6757787584-d7zsl_docker_9ddb62e0-750f-11e9-9c87-025000000001_0                                      k8s.gcr.io/pause-amd64:3.1       "/pause"
k8s_POD_kube-proxy-vpg7m_kube-system_c338829d-7237-11e9-bffb-025000000001_0                                             k8s.gcr.io/pause-amd64:3.1       "/pause"
k8s_POD_kube-dns-86f4d74b45-7zr8j_kube-system_c3658298-7237-11e9-bffb-025000000001_0                                    k8s.gcr.io/pause-amd64:3.1       "/pause"
k8s_POD_compose-74649b4db6-zclv4_docker_21021466-7464-11e9-a5e0-025000000001_0                                          k8s.gcr.io/pause-amd64:3.1       "/pause"
k8s_kube-scheduler_kube-scheduler-docker-for-desktop_kube-system_b6155a27330304c86badfef38a6b483b_0                     d2c751d562c6                     "kube-scheduler --ad…"
k8s_kube-apiserver_kube-apiserver-docker-for-desktop_kube-system_c158ce5b29225e1de9a2153c231532c8_0                     e851a7aeb6e8                     "kube-apiserver --ad…"
k8s_etcd_etcd-docker-for-desktop_kube-system_a3b09d6f4b2a75e76bab2b9be7266eed_0                                         52920ad46f5b                     "etcd --listen-clien…"
k8s_kube-controller-manager_kube-controller-manager-docker-for-desktop_kube-system_49730b387e8bebf0751e355aee021543_0   978cfa2028bf                     "kube-controller-man…"
k8s_POD_kube-apiserver-docker-for-desktop_kube-system_c158ce5b29225e1de9a2153c231532c8_0                                k8s.gcr.io/pause-amd64:3.1       "/pause"
k8s_POD_etcd-docker-for-desktop_kube-system_a3b09d6f4b2a75e76bab2b9be7266eed_0                                          k8s.gcr.io/pause-amd64:3.1       "/pause"
k8s_POD_kube-scheduler-docker-for-desktop_kube-system_b6155a27330304c86badfef38a6b483b_0                                k8s.gcr.io/pause-amd64:3.1       "/pause"
k8s_POD_kube-controller-manager-docker-for-desktop_kube-system_49730b387e8bebf0751e355aee021543_0                       k8s.gcr.io/pause-amd64:3.1       "/pause"
```
>说明：关于各个容器的作用，请参考[这里](https://github.com/kubernetes/kubernetes/tree/master/build) 。

查看自动安装的 namespaces
```console
$ kubectl get namespaces
NAME          STATUS   AGE
default       Active   4d
docker        Active   4d
kube-public   Active   4d
kube-system   Active   4d
```

查看自动安装的 kube-system namespace 中的 pods
```console
$ kubectl get pods --namespace kube-system
NAME                                         READY   STATUS    RESTARTS   AGE
etcd-docker-for-desktop                      1/1     Running   0          4d
kube-apiserver-docker-for-desktop            1/1     Running   0          4d
kube-controller-manager-docker-for-desktop   1/1     Running   0          4d
kube-dns-86f4d74b45-7zr8j                    3/3     Running   0          4d
kube-proxy-vpg7m                             1/1     Running   0          4d
kube-scheduler-docker-for-desktop            1/1     Running   0          4d
```

查看 Kubernetes 版本
```console
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"14", GitVersion:"v1.14.1", GitCommit:"b7394102d6ef778017f2ca4046abbaa23b88c290", GitTreeState:"clean", BuildDate:"2019-04-19T22:12:47Z", GoVersion:"go1.12.4", Compiler:"gc", Platform:"darwin/amd64"}
Server Version: version.Info{Major:"1", Minor:"10", GitVersion:"v1.10.11", GitCommit:"637c7e288581ee40ab4ca210618a89a555b6e7e9", GitTreeState:"clean", BuildDate:"2018-11-26T14:25:46Z", GoVersion:"go1.9.3", Compiler:"gc", Platform:"linux/amd64"}
```
> 说明：可以看出 Docker 自带的 Kubernetes 版本相对比较低
## 3. 在本地测试应用程序
访问 http://localhost:8080
![image](./images/aks-tutorial-lab01-01.png)

## 4. 停止并删除容器
```console
$ docker-compose stop
$ docker-compose down
```
