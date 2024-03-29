## 简介

VOD Migrate Tool 是一个集成了数据迁移功能的一体化工具。通过编写简单的配置文件，用户可以将源地址媒体文件快速迁移至 VOD 中。

## 支持的数据源
* [x] 本地文件夹
* [x] URL 列表
* [x] 腾讯云 COS
* [x] AWS S3
* [x] 阿里云 OSS
* [x] 七牛云 对象存储

## 使用环境

#### 系统环境

支持 Windows、Linux 和 macOS 系统。

#### 软件依赖

- Python 2.7/3.4+。
- 最新版本的 pip。
  
## 安装

### 通过 Pip 安装（推荐）
您可以通过 pip 安装方式将 SDK 安装到您的项目中，如果您的项目环境尚未安装 pip，请详细参见 pip 官网安装。

```
pip install vodmigrate
```


### 通过源码包安装
源码下载地址：[单击此处](https://github.com/tencentyun/vod-migrate.git)。
下载最新代码，解压后：

```shell
git clone https://github.com/tencentyun/vod-migrate.git
cd vod-migrate
python setup.py install
```

## 使用示例
执行命令：
```
vodmigrate config.toml
```
> ?迁移完成后，结果将输出到配置项"migrateResultOutputPath"对应的目录，文件名为：vod_migrate_result.txt。

## 配置文件说明
配置文件采用 toml 格式（参考：[config_template.toml](https://github.com/tencentyun/vod-migrate/blob/master/test/config_template.toml)，请确保文件为 UTF-8 编码），内容可以分为以下几部分：

### 1. 配置迁移类型

type 表示迁移类型，用户根据迁移需求填写对应的标识。例如，需要将本地数据迁移至 VOD，则`[migrateType]`的配置内容是`type=migrateLocal`。
```
[migrateType]
type="migrateLocal"
```
目前支持的迁移类型如下：

| migrateType  |           描述           |
| :----------- | :----------------------: |
| migrateLocal |     从本地迁移至 VOD     |
| migrateUrl   |   下载 URL 迁移到 VOD    |
| migrateCos   | 从 腾讯云 COS 迁移至 VOD |
| migrateAws   |   从 AWS S3 迁移至 VOD   |
| migrateAli   | 从阿里云 OSS 迁移至 VOD  |
| migrateQiniu |  从七牛云存储迁移至 VOD  |

### 2. 配置迁移任务

用户根据实际的迁移需求进行相关配置，主要包括迁移至 VOD 信息配置及迁移任务相关配置。

``` 
# 迁移工具公共配置
[common]
secretId = "SECRETID"
secretKey = "SECRETKEY"
region = 'REGION'
subAppId = 0
concurrency = 5
supportMediaClassification = [ 'video', 'audio', 'image' ]
excludeMediaType = [  ]
migrateDbStoragePath = ''
migrateResultOutputPath = ''
``` 

| 名称                       |                                                                                        描述                                                                                        |
| :------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| secretId                   |             用户密钥 SecretId，请将`SECRETID`替换为您的真实密钥信息。可前往 [访问管理控制台](https://console.cloud.tencent.com/cam/capi) 中的云 API 密钥页面查看获取             |
| secretKey                  |            用户密钥 SecretKey，请将`SECRETKEY`替换为您的真实密钥信息。可前往 [访问管理控制台](https://console.cloud.tencent.com/cam/capi) 中的云 API 密钥页面查看获取            |
| region                     | 接入点地域，即请求到哪个地域的云点播服务器，不同于存储地域，具体参考支持的 [地域列表](https://intl.cloud.tencent.com/document/product/266/34113) |
| subAppId                   |                点播 [子应用](https://intl.cloud.tencent.com/document/product/266/33987) ID。如果需要将文件迁移到子应用，则将该字段填写为子应用 ID；否则无需填写该字段             |
| concurrency                |                                                                            并发迁移文件的数量，最大值50                                                                            |
| supportMediaClassification |                                                        支持迁移的媒体类型列表：video（视频），audio（音频），image（图像）                                                         |
| excludeMediaType           |                                                                               需要排除的文件类型列表                                                                               |
| migrateDbStoragePath       |                                                                          迁移 db 保存路径，为空表示当前目录                                                                          |
| migrateResultOutputPath    |                                                      迁移结果保存路径（一条迁移记录对应一行 json 格式字符串），为空表示当前目录                                                      |

文件类型说明：
- 视频：MP4、TS、FLV、WMV、ASF、RM、RMVB、MPG、MPEG、3GP、MOV、WEBM、MKV、AVI，**不支持 HLS、DASH**
- 音频：MP3、M4A、FLAC、OGG、WAV
- 图像：JPG、JPEG、PNG、GIF、BMP、TIFF、AI、CDR、EPS

### 3. 配置数据源信息
根据 [migrateType] 的迁移类型配置相应的分节。例如 [migrateType] 的配置内容是 type=migrateLocal，则用户只需配置 [migrateLocal] 分节即可。

#### 3.1 配置本地数据源 migrateLocal

若从本地迁移至 VOD，则进行该部分配置，具体配置项及说明如下：

``` 
# 从本地迁移到 VOD 配置分节
[migrateLocal]
localPath = ''
excludes = [ ]
``` 

| 配置项    |                                 描述                                  |
| :-------- | :-------------------------------------------------------------------: |
| localPath |                     本地路径，要求格式为绝对路径                      |
| excludes  | 要排除的目录的绝对路径，表示将 localPath 下面某些目录下文件不进行迁移 |

#### 3.2 配置 URL 列表数据源 migrateUrl
若从指定 URL 列表迁移至 VOD，则进行该部分配置，具体配置项及说明如下：
```
# 从 URL 列表下载迁移到 VOD 配置分节
[migrateUrl]
urllistPath = 'D:\folder\urllist.txt'
```

| 配置项      |                                    描述                                    |
| :---------- | :------------------------------------------------------------------------: |
| urllistPath | 存储 URL 列表的文件绝对路径。文件的内容为 URL 文本，一行一条 URL 原始地址|

>?如需迁移本地大型文件至云点播，建议使用 [pullUpload](https://intl.cloud.tencent.com/document/product/266/34118) 接口拉取。
#### 3.3 配置 COS 数据源 migrateCos

若从腾讯云 COS 迁移至 VOD，则进行该部分配置，具体配置项及说明如下：
``` 
# 从腾讯云 COS 迁移至 VOD 配置分节
[migrateCos]
region = 'ap-shanghai'
bucket = 'examplebucket-1250000000'
secretId = 'COS_SECRETID'
secretKey = 'COS_SECRETKEY'
prefix = ''
``` 

| 配置项    |                                                    描述                                                     |
| :-------- | :---------------------------------------------------------------------------------------------------------: |
| region    |        Bucket 的 Region 信息，请参照 [可用地域](https://intl.cloud.tencent.com/document/product/436/6224)        |
| bucket    | Bucket 的名称，命名格式为`<BucketName-APPID>`，即 Bucket 名必须包含 APPID，例如 examplebucket-1250000000 |
| secretId  |   Bucket 隶属的用户密钥 SecretId，可在 [云 API 密钥](https://console.cloud.tencent.com/cam/capi) 查看  |
| secretKey |  Bucket 隶属的用户密钥 secret_key，可在 [云 API 密钥](https://console.cloud.tencent.com/cam/capi) 查看  |
| prefix    |                     要迁移路径的前缀，如果是迁移 Bucket 下所有的数据，则 prefix 为空                      |

#### 3.4 配置 AWS 数据源 migrateAws
若从 AWS 迁移至 VOD，则进行该部分配置，具体配置项及说明如下：
```
# 从 AWS 迁移到 VOD 配置分节
[migrateAws]
region = 'ap-northeast-2'
bucket = 'bucket-aws'
accessKeyId = 'AccessKeyId'
accessKeySecret = 'AccessKeySecret'
prefix = ''
```

| 配置项          |                                描述                                |
| :-------------- | :----------------------------------------------------------------: |
| region          |                        AWS 对象存储 Region                         |
| bucket          |                      AWS 对象存储 Bucket 名称                      |
| accessKeyId     |                  将 AccessKeyId 替换为用户的密钥                   |
| accessKeySecret |                将 AccessKeySecret 替换为用户的密钥                 |
| prefix          | 要迁移的路径的前缀，如果是迁移 Bucket 下所有的数据，则 prefix 为空 |

#### 3.5 配置阿里 OSS 数据源 migrateAli
若从阿里云 OSS 迁移至 VOD，则进行该部分配置，具体配置项及说明如下：

```
# 从阿里 OSS 迁移到 VOD 配置分节
[migrateAli]
bucket = 'bucket-aliyun'
accessKeyId = 'yourAccessKeyId'
accessKeySecret = 'yourAccessKeySecret'
endPoint = 'oss-cn-hangzhou.aliyuncs.com'
prefix = ''
```

| 配置项          |                                描述                                |
| :-------------- | :----------------------------------------------------------------: |
| bucket          |                       阿里云 OSS Bucket 名称                       |
| accessKeyId     |                将 yourAccessKeyId 替换为用户的密钥                 |
| accessKeySecret |              将 yourAccessKeySecret 替换为用户的密钥               |
| endPoint        |                        阿里云 endpoint 地址                        |
| prefix          | 要迁移路径的前缀，如果是迁移 Bucket 下所有的数据, 则 prefix 为空 |

#### 3.6 配置七牛数据源 migrateQiniu
若从七牛迁移至 VOD，则进行该部分配置，具体配置项及说明如下：
```
# 从七牛迁移到 VOD 配置分节
[migrateQiniu]
bucket = 'bucket-qiniu'
accessKeyId = 'AccessKey'
accessKeySecret = 'SecretKey'
endPoint = 'www.bkt.clouddn.com'
prefix = ''
```

| 配置项          |                                描述                                |
| :-------------- | :----------------------------------------------------------------: |
| bucket          |                      七牛对象存储 Bucket 名称                      |
| accessKeyId     |                   将 AccessKey 替换为用户的密钥                    |
| accessKeySecret |                   将 SecretKey 替换为用户的密钥                    |
| endPoint        |                 七牛下载地址，对应 downloadDomain                  |
| prefix          | 要迁移路径的前缀，如果是迁移 Bucket 下所有的数据，则 prefix 为空 |

## 限制说明
- 该工具定位为一次性的迁移工具。迁移分为**源站文件扫描**、**迁移中**、**迁移完成**三个阶段。文件扫描完成后，如果配置需变更，这时候需将 db 文件清空（删除 migrate.db 或者修改 db 存储路径），以规避配置文件 md5 校验报错。
- 迁移的文件必须显示的带后缀。
- 暂不支持 HLS/DASH 迁移。
- 迁移后无法维持原视频的目录关系、每个视频都是独立的 FileId，相互无关联。

## 迁移流程介绍
1. 读取配置文件，根据迁移 type，读取相应的配置分节，并执行参数的检查。
2. 根据指定的迁移类型，扫描源站，生成迁移任务。
3. 扫描完成后，执行迁移，并打印每个任务的结果及整体进度。
4. 迁移完成后，将详细信息输出到结果文件。
![](https://main.qcloudimg.com/raw/66946618fe7e54ea19f7a8a78890078b.png)

