腾讯云对象存储服务（COS）相关接口及说明如下：

## Service 接口

| API                                                          | 操作名         | 操作描述                     |
| ------------------------------------------------------------ | -------------- | ---------------------------- |
| [GET Service（List Buckets）](https://intl.cloud.tencent.com/document/product/436/8291) | 查询存储桶列表 | 查询指定账号下所有存储桶列表 |

## Bucket 接口

#### 基本操作接口

| API                                                          | 操作名             | 操作描述                                       |
| ------------------------------------------------------------ | ------------------ | ---------------------------------------------- |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | 创建存储桶         | 在指定账号下创建一个存储桶                     |
| [GET Bucket（List Objects）](https://intl.cloud.tencent.com/document/product/436/30614) | 查询对象列表       | 查询存储桶下的部分或者全部对象                 |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | 检索存储桶及其权限 | 确认存储桶是否存在且是否有权限访问             |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | 删除存储桶         | 删除指定账号下的空存储桶                       |
| [GET Bucket Object versions](https://intl.cloud.tencent.com/document/product/436/31551) | 查询对象版本       | 查询存储桶下的部分或者全部对象及其历史版本信息 |


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



#### 存储桶标签（tagging）接口

| API                                                          | 操作名         | 操作描述                         |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | 设置存储桶标签 | 为已存在的存储桶设置标签         |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | 查询存储桶标签 | 查询指定存储桶下已有的存储桶标签 |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | 删除存储桶标签 | 删除指定的存储桶标签             |



#### 静态网站（website）接口

| API                                                          | 操作名           | 操作描述                           |
| ------------------------------------------------------------ | ---------------- | ---------------------------------- |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | 设置静态网站     | 为存储桶配置静态网站               |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | 查询静态网站配置 | 查询与存储桶关联的静态网站配置信息 |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | 删除静态网站配置 | 删除指定存储桶的静态网站配置信息   |


#### 智能分层（IntelligentTiering）接口

| API                                                          | 操作名           | 操作描述                     |
| ------------------------------------------------------------ | ---------------- | ---------------------------- |
| [PUT Bucket IntelligentTiering](https://intl.cloud.tencent.com/document/product/436/38314) | 设置智能分层配置 | 启用存储桶的智能分层存储配置 |
| [GET Bucket IntelligentTiering](https://intl.cloud.tencent.com/document/product/436/38315) | 查询智能分层配置 | 查询存储桶的智能分层配置信息 |




#### 清单（inventory）接口

| API                                                          | 操作名       | 操作描述                     |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30625) | 设置清单任务 | 在存储桶中创建清单任务       |
|  [POST Bucket inventory](https://intl.cloud.tencent.com/document/product/436/46869)       |    创建一次性清单任务             |  对一个存储桶创建一个一次性清单任务  |
| [GET Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30623) | 查询清单任务 | 查询存储桶的指定清单配置信息 |
| [List Bucket Inventory Configurations](https://intl.cloud.tencent.com/document/product/436/30627) | 查询所有清单 | 查询存储桶的所有清单任务     |
| [DELETE Bucket inventory](https://intl.cloud.tencent.com/document/product/436/30626) | 删除清单任务 | 删除存储桶中指定的清单任务   |

#### 版本控制（versioning）接口

| API                                                          | 操作名       | 操作描述                         |
| ------------------------------------------------------------ | ------------ | -------------------------------- |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | 设置版本控制 | 启用或者暂停存储桶的版本控制功能 |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | 查询版本控制 | 查询存储桶的版本控制信息         |

#### 存储桶复制（replication）接口

| API                                                          | 操作名         | 操作描述                                   |
| ------------------------------------------------------------ | -------------- | ------------------------------------------ |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | 设置存储桶复制 | 对已启用版本控制的存储桶配置存储桶复制规则 |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | 查询存储桶复制 | 查询存储桶的存储桶复制配置信息             |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | 删除存储桶复制 | 删除存储桶的存储桶复制配置信息             |

#### 日志管理（logging）接口

| API                                                          | 操作名       | 操作描述                   |
| ------------------------------------------------------------ | ------------ | -------------------------- |
| [PUT Bucket logging](https://intl.cloud.tencent.com/document/product/436/17054) | 设置日志管理 | 为源存储桶开启日志记录     |
| [GET Bucket logging](https://intl.cloud.tencent.com/document/product/436/17053) | 查询日志管理 | 查询源存储桶的日志配置信息 |

#### 全球加速（accelerate）接口

| API                   | 操作名       | 操作描述                   |
| ---------------------- | ------------ | -------------------------- |
| [PUT Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33411)|  设置全球加速  |  启用或暂停存储桶的全球加速功能 |
| [GET Bucket Accelerate](https://intl.cloud.tencent.com/document/product/436/33412)|  查询全球加速   |  查询存储桶的全球加速功能配置信息  |



#### 存储桶加密（encryption）接口

| API                                                          | 操作名         | 操作描述                       |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33459) | 设置存储桶加密 | 设置指定存储桶下的默认加密配置 |
| [GET Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33460) | 查询存储桶加密 | 查询指定存储桶下的默认加密配置 |
| [DELETE Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33461) | 删除存储桶加密 | 删除指定存储桶下的默认加密配置 |



#### 对象锁定（ObjectLock）接口


| API                                                          | 操作名         | 操作描述                       |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket ObjectLockConfiguration](https://intl.cloud.tencent.com/document/product/436/40133)|     设置对象锁定    |    为已存在的存储桶设置对象锁定   |
| [GET Bucket ObjectLockConfiguration](https://intl.cloud.tencent.com/document/product/436/40134)|     查询对象锁定    |    查询已生效的对象锁定配置    |
|[GET Object retention](https://www.tencentcloud.com/document/product/436/40135) | 查询对象锁定的到期日期   |    查询对象锁定的到期日期     |


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
| [SELECT Object Content](https://intl.cloud.tencent.com/document/product/436/32360) | 检索对象内容   | 检索指定对象的内容                       |

#### 访问控制接口

| API                                                          | 操作名       | 操作描述                           |
| ------------------------------------------------------------ | ------------ | ---------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 设置对象 ACL | 设置存储桶中某个对象的访问控制列表 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 查询对象 ACL | 查询对象的访问控制列表             |

#### 对象标签接口

| API                                                          | 操作名       | 操作描述                     |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT   Object tagging](https://intl.cloud.tencent.com/document/product/436/35709) | 设置对象标签 | 为已上传的对象设置标签       |
| [GET   Object tagging](https://intl.cloud.tencent.com/document/product/436/35710) | 查询对象标签 | 查询指定对象下已有的对象标签 |
| [DELETE   Object tagging](https://intl.cloud.tencent.com/document/product/436/35711) | 删除对象标签 | 删除指定对象下已有的对象标签 |

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


## 批量处理（batch）接口

| API                                                          | 操作名         | 操作描述                                         |
| ------------------------------------------------------------ | -------------- | ------------------------------------------------ |
| [CreateJob](https://intl.cloud.tencent.com/document/product/436/33781) | 创建任务       | 用于在存储桶中创建批量处理任务                   |
| [DescribeJob](https://intl.cloud.tencent.com/document/product/436/33782) | 描述任务       | 用于获取已创建的批量处理任务的参数和任务执行状态 |
| [ListJobs](https://intl.cloud.tencent.com/document/product/436/33783) | 查询任务       | 用于列出已创建的批量处理任务                     |
| [UpdateJobPriority](https://intl.cloud.tencent.com/document/product/436/33784) | 更新任务优先级 | 用于更新已创建任务的优先级                       |
| [UpdateJobStatus](https://intl.cloud.tencent.com/document/product/436/33785) | 更新任务状态   | 用于更新已创建任务的状态                         |
|  [公共元素](https://intl.cloud.tencent.com/document/product/436/33786)|—|   批量处理功能的公共元素|
|  [错误响应](https://intl.cloud.tencent.com/document/product/436/33787)|—|  批量处理功能的错误响应|




##  数据处理接口         


#### 数据处理接口

数据处理接口包括图片处理、AI 内容识别、媒体处理、文档处理、文件处理等接口类别，详情请参见 [数据处理接口](https://www.tencentcloud.com/document/product/436/36364)。



#### 内容审核接口

内容审核接口包括图片审核、视频审核、音频审核、文本审核、文档审核、网页审核、直播审核等接口类别，详情请参见 [内容审核接口](https://www.tencentcloud.com/document/product/436/48186)。


#### 任务与工作流接口

任务与工作流接口包括工作流接口、工作流实例、任务接口、模板接口、批量任务接口等接口类别，详情请参见 [任务与工作流接口](https://www.tencentcloud.com/document/product/436/46211)。


#### 云查毒接口

| API                                                          |  操作描述                                         |
| ---------------------------------------------- | -------------- |
|  [提交病毒检测任务](https://intl.cloud.tencent.com/document/product/436/50132) |  对云上的文件进行文件病毒（例如木马病毒、蠕虫病毒等）检测|
|  查询病毒检测任务结果 | 用于查询一个病毒检测任务的状态或结果 |







