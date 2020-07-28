1. The game process communicates with GSE through gRPC protocol. For gRPC proto files, please see `GameServerGrpcSdkService.proto` and `GseGrpcSdkService.proto`.
![](https://main.qcloudimg.com/raw/5426f569f7b99ca67160a038efb9b852.png)
2. The three service APIs defined by `GameServerGrpcSdkService.proto` are implemented by the game process, and GSE needs to call them at the appropriate time.
3. The nine service APIs defined by `GseGrpcSdkService.proto` are implemented by GSE, and the game process needs to call them at the appropriate time. The GSE API listens on gRPC at port 5758.
 >?We provide the proto files for defining services. You can [click here](https://gsegrpcdemo-1301007756.cos.ap-guangzhou.myqcloud.com/proto.zip) to directly download them with no need to generate them by yourself.

