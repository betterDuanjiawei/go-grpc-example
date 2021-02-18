#gRPC 相关

## gRPC
* go get -u google.golang.org/grpc

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

## Protoc Plugin
* go get -u github.com/golang/protobuf/protoc-gen-go