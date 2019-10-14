# 从0开发CRD

## 安装code-generator
 
```
$ cd $GOPATH/src
$ git clone https://github.com/kubernetes/code-generator k8s.io/code-generator
```

## 初始化

```
$ mkdir $GOPATH/src/selfcrd
$ cd $GOPATH/src/selfcrd
$ mkdir -p example
$ mkdir -p pkg/apis/selfcrd/v1
```

## 定义crd

```
$ cd example
$ cat crd.yaml selfcrd_example.yaml
```

## 定义消息格式

```
cat doc.go
cat types.go
cat register.go
```

## 生成客户端

```
$GOPATH/src/k8s.io/code-generator/generate-groups.sh all     "github.com/asdfsx/selfcrd/pkg/client"     "github.com/asdfsx/selfcrd/pkg/apis"     "selfcrd:v1"
${GOPATH}/bin/defaulter-gen  --input-dirs github.com/asdfsx/selfcrd/pkg/apis/selfcrd/v1 -O zz_generated.defaults 
```

## 创建客户端

复制[workqueue-example](https://github.com/kubernetes/client-go/blob/master/examples/workqueue/main.go)到本地

修改相关的业务逻辑

## 本地运行

```
go build -mod vendor .
./selfcrd --kubeconfig ~/.kube/config
```


可以通过使用`git log`查看本项目的历史记录。来查看每一步发生的变更