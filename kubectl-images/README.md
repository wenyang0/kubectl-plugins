# kubectl-images


## 插件背景
通过表格化整理展示命名空间下的所有容器镜像，便于查看版本和发现问题。

## 原理
kubectl images使用kubectl命令。它首先调用kubectl get pods来检索pods细节，过滤出每个pod的容器图像信息，然后在表视图中打印出最终结果。

## 编译安装

```sh
# 下载代码
$ git clone https://gitlab-ce.alauda.cn/ops/kubectl-plugins.git
$ cd kubectl-plugins/kubectl-images 

# 编译命令(确保你有一个可用的kubeconfig)
GO111MODULE="on" go build  -ldflags '-w -s' -o kubectl-images cmd/main.go

# 将构建的二进制文件放到可执行路径中
$ cp ./kubectl-images /usr/local/bin

#现在可以开始将此插件作为常规kubectl命令使用：
```

## 用法

![image](https://user-images.githubusercontent.com/19553554/74729593-a9201e00-527f-11ea-8325-a4c332dde783.png)
![image](https://user-images.githubusercontent.com/19553554/74729607-ade4d200-527f-11ea-938d-892158d7560f.png)

### 使用帮助

```shell
~  kubectl images --help
Show container images used in the cluster.

Usage:
  kubectl-images [podname-regex] [flags]

Examples:
  # display a table of all images in current namespace using podName/containerName/containerImage as columns.
  kubectl images

  # display a table of images that match 'nginx' podname regex in 'dev' namespace using podName/containerImage as columns.
  kubectl images -n dev nginx -c 1,2

Flags:
  -A, --all-namespaces         if present, list images in all namespaces.
  -c, --columns string         specify the columns to display, separated by comma. [0:Namespace, 1:PodName, 2:ContainerName, 3:ContainerImage] (default "1,2,3")
  -h, --help                   help for kubectl-images
  -k, --kubeconfig string      path to the kubeconfig file to use for CLI requests.
  -n, --namespace string       if present, list images in the specified namespace only. Use current namespace as fallback.
  -o, --output-format string   output format. [json|table] (default "table")
      --version                version for kubectl-images
```

## 清除插件

您只需从路径中删除该插件，即可从kubectl“卸载”该插件：

    $ rm /usr/local/bin/kubectl-images

## 项目来自于哪里？

`kubectl-images` 来自于:

https://github.com/chenjiandongx/kubectl-images