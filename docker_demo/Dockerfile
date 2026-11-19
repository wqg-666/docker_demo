FROM golang:alpine AS builder

# 为我们的镜像设置必要的环境变量
ENV GO111MODULE=on \
    CGO_ENABLED=0 \
    GOOS=linux \
    GOARCH=amd64

# 移动到工作目录：/build
WORKDIR /build

# 将代码复制到容器中
COPY . .

# 将我们的代码编译成二进制可执行文件 app
RUN go build -o app .

###################
# 接下来创建一个小镜像
###################
FROM scratch

# 从builder镜像中把/build/app 拷贝到当前目录
COPY --from=builder /build/app /

ENTRYPOINT ["/app"]

#第一阶段：builder
 #golang:alpine
 #- 包含 Go 编译环境
 #- 复制 Go 源代码
 #- 执行 go build
 #- 生成 app 可执行文件
 #只复制编译后的 app
#第二阶段：最终镜像
 #scratch
 #- 不包含 Go 编译环境
 #- 不包含 Go 源代码
 #- 只包含 app 可执行文件
 #- 启动 app