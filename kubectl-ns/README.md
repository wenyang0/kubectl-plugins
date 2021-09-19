# kubectl-ns


## 插件背景
kubectl 工具使用中经常来回切换命名空间，增加了查看资源的时间。建议改进。


## 原理

示例cli插件使用[client go library](https://github.com/kubernetes/client-go/tree/master/tools/clientcmd)修补用户环境中的现有KUBECONFIG文件，以便更新上下文信息，以将客户端指向新的或现有的命名空间。

为了尽可能无损，任何现有上下文都不会以任何方式进行修改。相反，将检查当前上下文，并与现有上下文匹配，以找到包含相同“AuthInfo”和“Cluster”信息的上下文，但包含用户请求的新名称空间。


## 编译安装

```sh

# 下载代码
$ git clone  https://gitlab-ce.alauda.cn/ops/kubectl-plugins.git
$ cd kubectl-plugins/kubectl-ns/

# 编译命令(确保你有一个可用的kubeconfig)
$ GO111MODULE="on" go build -ldflags '-w -s' cmd/kubectl-ns.go

# 将构建的二进制文件放到可执行路径中
$ cp ./kubectl-ns /usr/local/bin

#现在可以开始将此插件作为常规kubectl命令使用：
```

## 用法
```sh
#更新配置以指向“新命名空间”
$ kubectl ns new-namespace
# 从现在开始执行的任何kubectl命令都将使用 "new-namespace"
$ kubectl get pod
NAME                READY     STATUS    RESTARTS   AGE
new-namespace-pod   1/1       Running   0          1h

# 列出KUBECONFIG中上下文使用的所有命名空间
$ kubectl ns --list

# 显示KUBECONFIG中当前设置的上下文指向的命名空间
$ kubectl ns
```

## 使用帮助
```sh
Usage:
  ns [new-namespace] [flags]

Examples:

	# view the current namespace in your KUBECONFIG
	kubectl ns

	# view all of the namespaces in use by contexts in your KUBECONFIG
	kubectl ns --list

	# switch your current-context to one that contains the desired namespace
	kubectl ns foo
```

## 清除插件

您只需从路径中删除该插件，即可从kubectl“卸载”该插件：

    $ rm /usr/local/bin/kubectl-ns

## 项目来自于哪里？

`kubectl-ns` 来自于:

https://github.com/kubernetes/kubernetes/blob/master/staging/src/k8s.io/sample-cli-plugin