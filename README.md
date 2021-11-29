# 模块八作业

> 编写 Kubernetes 部署脚本将 httpserver 部署到 kubernetes 集群，以下是你可以思考的维度

1. 优雅启动
2. 优雅终止
3. 资源需求和 QoS 保证
4. 探活
5. 日常运维需求，日志等级
6. 配置和代码分离

> 除了将 httpServer 应用优雅的运行在 Kubernetes 之上，我们还应该考虑如何将服务发布给对内和对外的调用方。来尝试用 Service, Ingress 将你的服务发布给集群外部的调用方吧; 在第一部分的基础上提供更加完备的部署 spec，包括（不限于）

1. Service
2. Ingress

### 执行路程

```Bash
$ docker build -t httpdemo:v1.0.0 .
$ docker images httpdemo
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
httpdemo     v1.0.0    caa766d99aaa   3 minutes ago   926MB

$ helm install httpdemo .
NAME: httpdemo
LAST DEPLOYED: Mon Nov 29 16:10:56 2021
NAMESPACE: test
STATUS: deployed
REVISION: 1
TEST SUITE: None

# 测试
$ kp httpdemo-685fbc8777-9b5jg
NAME                        READY   STATUS    RESTARTS   AGE
httpdemo-685fbc8777-9b5jg   1/1     Running   0          98s
$ ks httpdemo
NAME       TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
httpdemo   NodePort   172.30.244.126   <none>        8081:31889/TCP   78s
$ k get endpoints httpdemo
NAME       ENDPOINTS             AGE
httpdemo   172.16.166.151:8081   87s

```