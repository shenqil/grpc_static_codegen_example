# 1. 下载官方示例
```
git clone git@github.com:grpc/grpc-node.git
```
+ 复制`examples\helloworld\static_codegen`demo

# 2. 得到如下目录
![image.png](https://upload-images.jianshu.io/upload_images/25820166-96202a9efec0f5ba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
+ 安装项目依赖
```sh
npm i @grpc/grpc-js
npm i google-protobuf
npm i minimist
```
##  2.1 安装工具依赖
```sh
npm install -g grpc-tools
```
## 2.2 编译 `.proto` 文件
```sh
cd ./pb
grpc_tools_node_protoc.cmd --js_out=import_style=commonjs,binary:./ --grpc_out=grpc_js:./ helloworld.proto
```
+ 这里根据官方给的`grpc_tools_node_protoc --js_out=import_style=commonjs,binary:./ --grpc_out=grpc_js:./ helloworld.proto`得不到`helloworld_pb.js`文件; 详情请看[helloworld_pb.js file is not generated #2600](https://github.com/grpc/grpc-node/issues/2600) 

# 3. 修改官方示例
```js
// greeter_server.js

  - server.addService(services.GreeterService, {sayHello: sayHello});
  + server.addService(services['helloworld.Greeter'], {sayHello: sayHello});
```
```js
// greeter_client.js
- var client = new services.GreeterClient(target,
                                          grpc.credentials.createInsecure());

+ var GreeterClient = grpc.makeGenericClientConstructor(services['helloworld.Greeter']);

+ const client = new GreeterClient(target, grpc.credentials.createInsecure())
```

# 4.运行
```
node .\greeter_server.js
node .\greeter_client.js
```


