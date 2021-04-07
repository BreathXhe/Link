## 一、在 Ubuntu 20.04 上安装 Go

完成下面的步骤，在 Ubuntu 20.04 上安装 Go

### 1.1 下载 Go 压缩包

当前Go 的最新版为 1.16.3

在我们下载安装包时，请浏览[Go 官方下载页面](https://golang.org/dl/),并且检查一下是否有新的版本可用

以 root 或者其他 sudo 用户身份运行下面的命令，下载并且解压 Go 二进制文件到`/usr/local`目录：

```
wget -c https://golang.org/dl/go1.16.3.linux-amd64.tar.gz -O - | sudo tar -xz -C /usr/local
```

### 1.2 调整环境变量

通过将 Go 目录添加到`$PATH`环境变量，系统将会知道在哪里可以找到 Go 可执行文件。

这个可以通过添加下面的行到`/etc/profile`文件（系统范围内安装）或者`$HOME/.profile`文件（当前用户安装）

`GOROOT` 是 Go 在机器中安装的路径

`GOPATH` 是工作目录的位置

```
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

保存文件，并且重新加载新的PATH 环境变量到当前的 shell 会话：

```
source ~/.profile
```

### 1.3 验证 Go 安装过程

通过打印 Go 版本号，验证安装过程。

```
go version
```

输出应该像下面这样：

```
go version go1.14.2 linux/amd64
```

在任意目录下使用终端执行 go env 命令，输出如下结果说明Go语言开发包已经安装成功。

```
root@ububtu:~$ go env
GO111MODULE=""
GOARCH="amd64"
GOBIN=""
GOCACHE="/home/feng/.cache/go-build"
GOENV="/home/feng/.config/go/env"
GOEXE=""
GOFLAGS=""
GOHOSTARCH="amd64"
GOHOSTOS="linux"
GONOPROXY=""
GONOSUMDB=""
GOOS="linux"
GOPATH="/home/feng/go"
GOPRIVATE=""
GOPROXY="https://proxy.golang.org,direct"
GOROOT="/usr/local/go"
GOSUMDB="sum.golang.org"
GOTMPDIR=""
...
```

提示：上面只显示了部分结果。

## 二、Go 语言快速入门

想要测试 Go 安装过程，我们将会创建一个工作区，并且构建一个简单的程序，用来打印经典的"Hello World"信息。

### 2.1.编写程序

默认情况下，`GOPATH`变量，指定为工作区的位置，设置为`$HOME/go`。想要创建工作区目录，输入：

```bash
mkdir ~/go
```

在工作区内，创建一个新的目录`src/hello`：

```bash
mkdir -p ~/go/src/hello
```

在那个目录下，创建一个新文件，名称为`hello.go`:

```bash
package main

import "fmt"

func main() {
    fmt.Printf("Hello, World\n")
}
```

想要学习更多关于 Go 工作区的目录，浏览 [Go 文档页面](https://golang.org/doc/code.html#Workspaces)。

### 2.2.测试程序

浏览到`~/go/src/hello`目录

```
cd ~/go/src/hello
```

输入以下命令，执行程序

```
go run hello.go
```

输出以下内容

```
Hello, World
```

### 2.3.编译程序

浏览到`~/go/src/hello`目录

```
cd ~/go/src/hello
```

输入以下命令，构建程序

```bash
go mod tidy
go build
```

上面的这个命令将会构建一个名为`hello`的可执行文件。

可以通过简单执行下面的命令，运行这个可执行文件：

```bash
./hello
```

输出一下内容

```bash
Hello, World
```