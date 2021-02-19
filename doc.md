#gRPC 相关

## gRPC
* go get -u google.golang.org/grpc
```
报错信息:
2021/02/18 19:37:26 client.Search err:rpc error: code = Unavailable desc = connection error: desc = "transport: authentication handshake failed: x509: certificate is not valid for any names, but wanted to match go-grpc-example"
生成证书时候的名称和代码里的不一致

2021/02/18 19:41:42 client.Search err:rpc error: code = Unavailable desc = connection error: desc = "transport: authentication handshake failed: x509: certificate relies on legacy Common Name field, use SANs or temporarily enable Common Name matching with GODEBUG=x509ignoreCN=0"
https://blog.csdn.net/shachao888/article/details/110850501(实测可用)
 GODEBUG=x509ignoreCN=0 go run client.go
https://www.cnblogs.com/jackluo/p/13841286.html
```

## Protocol Buffers v3
```
wget https://github.com/google/protobuf/releases/download/v3.5.1/protobuf-all-3.5.1.zip
unzip protobuf-all-3.5.1.zip
cd protobuf-3.5.1/
./configure
make
make install

检查是否安装成功
protoc --version
若出现以下错误，执行 ldconfig 命名就能解决这问题
protoc: error while loading shared libraries: libprotobuf.so.15: cannot open shared object file: No such file or directory
```
* 根据 proto生成 go 代码
cd proto
protoc --go_out=plugins=grpc:. stream.proto

## Protoc Plugin
* go get -u github.com/golang/protobuf/protoc-gen-go

##  go-grpc-middleware
* 可以发现 gRPC 本身居然只能设置一个拦截器，难道所有的逻辑都只能写在一起？关于这一点，你可以放心。采用开源项目 go-grpc-middleware 就可以解决这个问题，本章也会使用它。
* go get -u github.com/grpc-ecosystem/go-grpc-middleware

## 拦截器
* 普通方法：一元拦截器（grpc.UnaryInterceptor）
* 流方法：流拦截器（grpc.StreamInterceptor）

## Zipkin
* 安装 docker run -d -p 9411:9411 openzipkin/zipkin