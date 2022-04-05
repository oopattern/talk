FROM golang:alpine

# 安装 curl, 默认安装在 /usr/bin目录, 用 find / -name curl 找出对应的位置
RUN apk add --update curl && rm -rf /var/cache/apk/*

# 为我们的镜像设置必要的环境变量
ENV GO111MODULE=on \
    CGO_ENABLED=0 \
    GOOS=linux \
    GOARCH=amd64 \
	GOPROXY="https://goproxy.cn,direct"

# 移动到工作目录：$GOPATH/src/talk 这个目录 是你项目代码 放在linux上  
WORKDIR /work/code/goworksapce/src/talk

# 将代码复制到容器中
COPY . .

RUN go mod init github.com/oopattern/talk
RUN go mod tidy

# 将我们的代码编译成二进制可执行文件  可执行文件名为 webtest
RUN go build -o webtest .

# 为镜像打标签?
LABEL Name=webtest Version=0.0.1

# 声明服务端口
EXPOSE 8080

# 启动容器时运行的命令
ENTRYPOINT ["./webtest"]
