# Go打包


[[toc]]




## flag

* [Go语言-打包静态文件](https://c.isme.pub/2019/01/10/go-static)


* [https://github.com/go-bindata/go-bindata](https://github.com/go-bindata/go-bindata)
* [https://github.com/shuLhan/go-bindata](https://github.com/shuLhan/go-bindata)
* [https://github.com/elazarl/go-bindata-assetfs](https://github.com/elazarl/go-bindata-assetfs)
* [https://github.com/rakyll/statik](https://github.com/rakyll/statik)
* [https://github.com/GeertJohan/go.rice](https://github.com/GeertJohan/go.rice)
* [https://github.com/mjibson/esc](https://github.com/mjibson/esc)
* [https://github.com/UnnoTed/fileb0x](https://github.com/UnnoTed/fileb0x)
* [https://github.com/gobuffalo/packr](https://github.com/gobuffalo/packr)



**cross compile**

> 交叉编译器（英语：Cross compiler）是指一个在某个系统平台下可以产生另一个系统平台的可执行文件的编译器。
> 交叉编译器在目标系统平台（开发出来的应用程序序所运行的平台）难以或不容易编译时非常有用。

> 交叉编译是在一个平台上生成另一个平台上的可执行代码。同一个体系结构可以运行不同的操作系统；
> 同样，同一个操作系统也可以在不同的体系结构上运行。

* [https://github.com/mitchellh/gox](https://github.com/mitchellh/gox)
* [https://github.com/wheelcomplex/goxx](https://github.com/wheelcomplex/goxx)
* [https://github.com/goreleaser/goreleaser](https://github.com/goreleaser/goreleaser)
* [https://github.com/laher/goxc](https://github.com/laher/goxc)
* [https://github.com/karalabe/xgo](https://github.com/karalabe/xgo)
* [https://github.com/techknowlogick/xgo](https://github.com/techknowlogick/xgo)
* [https://github.com/storyicon/gos](https://github.com/storyicon/gos)
* [https://github.com/docker/golang-cross](https://github.com/docker/golang-cross)
* [https://github.com/im4x5yn74x/dropper2](https://github.com/im4x5yn74x/dropper2)
* [https://github.com/caixw/gobuild](https://github.com/caixw/gobuild)



## 打包命令

* [https://golang.google.cn/doc/install/source#environment](https://golang.google.cn/doc/install/source#environment)
* [https://gist.github.com/asukakenji/f15ba7e588ac42795f421b48b8aede63](https://gist.github.com/asukakenji/f15ba7e588ac42795f421b48b8aede63)


### 设置编译环境

* [https://github.com/golang/go/blob/master/src/cmd/dist/build.go#L1513](https://github.com/golang/go/blob/master/src/cmd/dist/build.go#L1513)

- `go tool dist list` 获得所有受支持平台的列表

> `GOOS` 目标可执行程序运行操作系统，支持`darwin`、`freebsd`、`linux`、`windows`

> `GOARCH` 目标平台的体系架构，包括`386`、`amd64`、`arm`

> `CGO_ENABLED` CGO开关

> `-o` 参数为指定输出程序文件名


- 编译完成清理缓存`go clean -cache`


**`-ldflags`选项**

* 用`ldflags`给go链接器传入参数，`go tool link`查看可用值 [https://golang.org/cmd/link](https://www.godoc.org/cmd/link)

> `-ldflags="-w -s"` 选项可以减小编译后的程序体积

> 注意因为`date`和`go version`的输出有空格，所以`main.BUILD_TIME`和`main.GO_VERSION`必须使用引号括起来

```bash
go build -ldflags "-X main.VERSION=1.0.0 -X 'main.BUILD_TIME=`date`' \
-X 'main.GO_VERSION=`go version`' -X 'main.commitHash=`git rev-parse HEAD`'"
```

### windows

> `-ldflags="-H windowsgui"` 能隐藏黑窗口

```batch
# 交叉编译不支持 CGO 所以要禁用它
SET CGO_ENABLED=0
# 打包Linux 执行文件
SET GOOS=linux
# 打包386执行文件
SET GOARCH=amd64

go build main.go
# 打包文件成其他名字
go build -o test.exe main.go
```


### linux

```bash
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go
```


### 交叉编译代码


```go
package main

import (
	"flag"
	"fmt"
	"os"
	"os/exec"
	"path"
)

type syslist struct {
	GOOS   string
	GOARCH string
}

var syslists [32]syslist

func init() {
	syslists[0] = syslist{GOOS: "darwin", GOARCH: "386"}
	syslists[1] = syslist{GOOS: "darwin", GOARCH: "amd64"}
	syslists[2] = syslist{GOOS: "dragonfly", GOARCH: "amd64"}
	syslists[3] = syslist{GOOS: "freebsd", GOARCH: "386"}
	syslists[4] = syslist{GOOS: "freebsd", GOARCH: "amd64"}
	syslists[5] = syslist{GOOS: "freebsd", GOARCH: "arm"}
	syslists[6] = syslist{GOOS: "linux", GOARCH: "386"}
	syslists[7] = syslist{GOOS: "linux", GOARCH: "amd64"}
	syslists[8] = syslist{GOOS: "linux", GOARCH: "arm"}
	syslists[9] = syslist{GOOS: "linux", GOARCH: "arm64"}
	syslists[10] = syslist{GOOS: "linux", GOARCH: "ppc64"}
	syslists[11] = syslist{GOOS: "linux", GOARCH: "ppc64le"}
	syslists[12] = syslist{GOOS: "linux", GOARCH: "mips"}
	syslists[13] = syslist{GOOS: "linux", GOARCH: "mipsle"}
	syslists[14] = syslist{GOOS: "linux", GOARCH: "mips64"}
	syslists[15] = syslist{GOOS: "linux", GOARCH: "mips64le"}
	syslists[16] = syslist{GOOS: "linux", GOARCH: "s390x"}
	syslists[17] = syslist{GOOS: "nacl", GOARCH: "386"}
	syslists[18] = syslist{GOOS: "nacl", GOARCH: "amd64p32"}
	syslists[19] = syslist{GOOS: "nacl", GOARCH: "arm"}
	syslists[20] = syslist{GOOS: "netbsd", GOARCH: "386"}
	syslists[21] = syslist{GOOS: "netbsd", GOARCH: "amd64"}
	syslists[22] = syslist{GOOS: "netbsd", GOARCH: "arm"}
	syslists[23] = syslist{GOOS: "openbsd", GOARCH: "386"}
	syslists[24] = syslist{GOOS: "openbsd", GOARCH: "amd64"}
	syslists[25] = syslist{GOOS: "openbsd", GOARCH: "arm"}
	syslists[26] = syslist{GOOS: "plan9", GOARCH: "386"}
	syslists[27] = syslist{GOOS: "plan9", GOARCH: "amd64"}
	syslists[28] = syslist{GOOS: "plan9", GOARCH: "arm"}
	syslists[29] = syslist{GOOS: "solaris", GOARCH: "amd64"}
	syslists[30] = syslist{GOOS: "windows", GOARCH: "386"}
	syslists[31] = syslist{GOOS: "windows", GOARCH: "amd64"}
}

// 编译
func main() {
	// 文件存放目录
	var parentFolder string
	// 编译输出存放的子目录
	var subFolder string
	// 文件名前缀
	var filePrefix string
	// 要编译的源文件列表
	var files string
	// scanner := bufio.NewScanner(os.Stdin)
	// scanner.Scan()
	// fmt.Println(scanner.Text())
	//fmt.Println("请输文件存放目录：")
	// 当程序到此，会停止执行等待用户输入
	//fmt.Scanln(&parentFolder)

	flag.StringVar(&parentFolder, "p", "", "文件存放目录，默认：当前目录")
	flag.StringVar(&subFolder, "s", "", "编译输出存放子目录，默认：空")
	flag.StringVar(&filePrefix, "fp", "", "创建文件名前缀，默认：空")
	flag.StringVar(&files, "fs", "", "源文件列表，默认：空")
	flag.Parse()

	cmde := path.Join(parentFolder, subFolder, filePrefix)
	if filePrefix != "" && len(filePrefix) > 0 {
		cmde = cmde + "-"
	}
	for _, v := range syslists {
		ext := ""
		if v.GOOS == "windows" {
			ext = ".exe"
		}
		thisCmde := fmt.Sprintf("%v%v-%v%v", cmde, v.GOOS, v.GOARCH, ext)
		fmt.Println(thisCmde)
		cmd := exec.Command("go", "build", "-ldflags=-w", "-i", "-o", thisCmde, files)
		cmd.Env = append(os.Environ(), "GOARCH="+v.GOARCH, "GOOS="+v.GOOS)
		output, err := cmd.CombinedOutput()
		if err != nil {
			fmt.Println(fmt.Sprint(err) + ": " + string(output))
			return
		}
		fmt.Println(string(output))
	}
	fmt.Println("编译完成")
}
```



## 打包脚本

### 保存到项目根目录中

> 只需下载[go_7z_pack.bat](/files/go_7z_pack.bat)文件并保存到项目根目录中，且修改脚本中的`files`变量保存执行脚本即可


### 在任意目录新建

> 基本用法:`脚本名 rootPath files project`
>> `rootPath` 打包的根目录，路径必须完整
>>
>> `files` 需要打包的文件或文件夹，用双引号括起来
>>
>> `project` 打包完成后的压缩文件命名的前部分，可以不输入，默认为打包根目录的名称

> 示例：`脚本名 f:\\key-gin "pyutils static templates" key-gin`

* [go_7z_pack_arbitrary.bat](/files/go_7z_pack_arbitrary.bat)