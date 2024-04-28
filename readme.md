```sh
grpc_tools_node_protoc.cmd --js_out=import_style=commonjs,binary:. --grpc_out=generate_package_definition:. helloworld.proto
grpc_tools_node_protoc --js_out=import_style=commonjs,binary:../helloworld/static_codegen/ --grpc_out=grpc_js:../helloworld/static_codegen/ helloworld.proto

grpc_tools_node_protoc.cmd --js_out=import_style=commonjs,binary:./ --grpc_out=grpc_js:./ helloworld.proto
```