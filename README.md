# Kubectl-plugins

![kubectl logo](./images/kubectl-logo-medium.png)

解决频繁的执行kubectl命令的繁琐，减少定位问题的时间，期待大家一起加入！


## 使用方法

在原生k8s集群中使用下面的方法安装插件：
```sh
方法一：

# 下载代码
$ git clone  https://gitlab-ce.alauda.cn/ops/kubectl-plugins.git
$ cd kubectl-plugins/kubectl-all/
# 将构建的二进制文件放到可执行路径中
$ cp * /usr/local/bin/

方法二：
#或者可以使用下面这条命令来完成一键安装
mkdir -p /tmp/kubectl-all && \
cd /tmp/kubectl-all && \
wget https://github.com/opensource/kubectl-plugins/-/archive/master/kubectl-plugins-master.tar.gz?path=kubectl-all -O kubectl-all.tar.gz && \
tar -zxvf kubectl-all.tar.gz && \
cp -rvf ./kubectl-plugins-master-kubectl-all/kubectl-all/* /usr/local/bin/


```
现在可以开始将此插件作为常规kubectl命令使用

```sh
命令演示：

# 切换命令空间
kubectl ns kube-system && kubectl get pod

# 展示命名空间所有镜像和pod
kubectl images -n kube-system
 
# 查看deployment 的资源树
kubectl tree deployment coredns -n kube-system

# 查看pod的详细资源关系(name 可以模糊匹配)
kubectl podlens api -n kube-system

```


## 配合使用

```sh
kubectl命令自动补全：

yum install -y bash-completion
source <(kubectl completion bash)
echo "source <(kubectl completion bash)" >> ~/.bashrc
source  ~/.bashrc


kubectl 配置别名：

echo "alias kc='kubectl'" >> ~/.bashrc
source ~/.bashrc

```

## Linux系统编译环境配置

```sh
# 机器上安装 gcc +  git  + wget + krb5-devel
$ yum install gcc git  wget krb5-devel -y


# 安装go环境
$ wget https://golang.google.cn/dl/go1.16.6.linux-amd64.tar.gz

$ tar -C /usr/local -xzf go1.16.6.linux-amd64.tar.gz
$ echo 'export PATH=$PATH:/usr/local/go/bin' >> /etc/profile
$ source /etc/profile

# 编译的时候 默认使用的是proxy.golang.org，在国内无法访问 可能会报错
go: github.com/spf13/cobra@v1.1.3: Get "https://proxy.golang.org/github.com/spf13/cobra/@v/v1.1.3.mod": dial tcp 216.58.200.241:443: i/o timeout

# 解决方法：换一个国内能访问的代理地址：https://goproxy.cn
$ go env -w GOPROXY=https://goproxy.cn

```
