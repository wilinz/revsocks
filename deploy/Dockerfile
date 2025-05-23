# 第一阶段：编译阶段
FROM golang:1.19-alpine AS builder

# 设置工作目录
WORKDIR /app

# 复制其余的源代码
COPY . .

RUN go mod download
RUN go build -o revsocks .

# 第二阶段：运行阶段
FROM alpine:latest

# 设置工作目录
WORKDIR /root/

RUN apk add --no-cache tzdata

# 从编译阶段复制二进制文件
COPY --from=builder /app/revsocks .

EXPOSE 13333 14444

# 运行二进制文件
CMD ["./revsocks","-listen","13333","-socks","127.0.0.1:14444"]
