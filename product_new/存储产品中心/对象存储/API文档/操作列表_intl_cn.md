腾讯云对象存储服务（COS）相关接口及说明如下：

## Service 接口

| API                                                          | 操作名         | 操作描述                     |
| ------------------------------------------------------------ | -------------- | ---------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | 查询存储桶列表 | 查询指定账号下所有存储桶列表 |

## Bucket 接口

#### 基本操作接口

| API                                                          | 操作名             | 操作描述                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | 创建存储桶         | 在指定账号下创建一个存储桶         |
| [GET Bucket（List Object）](https://intl.cloud.tencent.com/document/product/436/7734) | 查询对象列表       | 查询存储桶下的部分或者全部对象     |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | 检索存储桶及其权限 | 确认存储桶是否存在且是否有权限访问 |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | 删除存储桶         | 删除指定账号下的空存储桶           |

#### 访问控制（acl）接口

| API                                                          | 操作名         | 操作描述                       |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | 设置存储桶 ACL | 设置指定存储桶访问权限控制列表 |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | 查询存储桶 ACL | 查询存储桶的访问控制列表       |



#### 跨域资源共享（cors）接口

| API                                                          | 操作名       | 操作描述                     |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | 设置跨域配置 | 设置存储桶的跨域访问权限     |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | 查询跨域配置 | 查询存储桶的跨域访问配置信息 |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | 删除跨域配置 | 删除存储桶的跨域访问配置信息 |



#### 生命周期（lifecycle）接口

| API                                                          | 操作名       | 操作描述                     |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | 设置生命周期 | 设置存储桶生命周期管理的配置 |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | 查询生命周期 | 查询存储桶生命周期管理的配置 |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | 删除生命周期 | 删除存储桶生命周期管理的配置 |



#### 存储桶策略（policy）接口

| API                                                          | 操作名         | 操作描述                 |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [ PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | 设置存储桶策略 | 设置指定存储桶的权限策略 |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | 查询存储桶策略 | 查询指定存储桶的权限策略 |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | 删除存储桶策略 | 删除指定存储桶的权限策略 |





#### 防盗链（referer）接口

| API                                                          | 操作名             | 操作描述                            |
| ------------------------------------------------------------ | ------------------ | ----------------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | 设置存储桶 referer | 设置存储桶 Referer 白名单或者黑名单 |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | 查询存储桶 referer | 查询存储桶 Referer 白名单或者黑名单 |



#### 标签（tagging）接口

| API                                                          | 操作名         | 操作描述                         |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | 设置存储桶标签 | 为已存在的存储桶设置标签         |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | 查询存储桶标签 | 查询指定存储桶下已有的存储桶标签 |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | 删除存储桶标签 | 删除指定的存储桶标签             |



#### 静态网站（website）接口

| API                                                          | 操作名             | 操作描述                           |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | 设置存储桶 website | 为存储桶配置静态网站               |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | 查询存储桶 website | 查询与存储桶关联的静态网站配置信息 |
| [DELETE Bucket website](<https://intl.cloud.tencent.com/document/product/436/30629>) | 删除存储桶 website | 删除指定存储桶的静态网站配置信息   |



## Object 接口

#### 基本操作接口

| API                                                          | 操作名         | 操作描述                                 |
| ------------------------------------------------------------ | -------------- | ---------------------------------------- |
| [PUT Object](https://intl.cloud.tencent.com/document/product/436/7749) | 简单上传对象   | 上传一个对象至存储桶                     |
| [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) | 设置对象复制   | 复制文件到目标路径                       |
| [POST Object](https://intl.cloud.tencent.com/document/product/436/14690) | 表单上传对象   | 使用表单请求上传对象                     |
| [GET Object](https://intl.cloud.tencent.com/document/product/436/7753) | 下载对象       | 下载一个对象至本地                       |
| [HEAD Object](https://intl.cloud.tencent.com/document/product/436/7745) | 查询对象元数据 | 查询对象的元数据信息                     |
| [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743) | 删除单个对象   | 在存储桶中删除指定对象                   |
| [DELETE Multiple Objects](https://intl.cloud.tencent.com/document/product/436/8289) | 删除多个对象   | 在存储桶中批量删除对象                   |
| [OPTIONS Object](https://intl.cloud.tencent.com/document/product/436/8288) | 预请求跨域配置 | 用预请求来确认是否可以发送真正的跨域请求 |
| [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633) | 恢复归档对象   | 将归档类型的对象取回访问                 |



#### 访问控制接口

| API                                                          | 操作名       | 操作描述                           |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 设置对象 ACL | 设置存储桶中某个对象的访问控制列表 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 查询对象 ACL | 查询对象的访问控制列表             |



#### 分块上传接口

| API                                                          | 操作名         | 操作描述                             |
| ------------------------------------------------------------ | -------------- | ------------------------------------ |
| [Initiate Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7746) | 初始化分块上传 | 初始化分块上传任务                   |
| [Upload Part](https://intl.cloud.tencent.com/document/product/436/7750) | 上传分块       | 分块上传文件                         |
| [Upload Part - Copy](https://intl.cloud.tencent.com/document/product/436/8287) | 复制分块       | 将其他对象复制为一个分块             |
| [Complete Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7742) | 完成分块上传   | 完成整个文件的分块上传               |
| [Abort Multipart Upload](https://intl.cloud.tencent.com/document/product/436/7740) | 终止分块上传   | 终止一个分块上传操作并删除已上传的块 |
| [List Multipart Uploads](https://intl.cloud.tencent.com/document/product/436/7736) | 查询分块上传   | 查询正在进行中的分块上传信息         |
| [List Parts](https://intl.cloud.tencent.com/document/product/436/7747) | 查询已上传块   | 查询特定分块上传操作中的已上传的块   |
