当前数据万象开放子账号数据持久化操作权限，通过关联 COS 指定资源写入权限实现。以下为相关案例，可实现数据万象**全资源**持久化处理授权或对**指定资源**授予持久化操作权限。

>! 子账号配置数据持久化权限前，必须先关联 CI 全读写权限 **QcloudCIFullAccess**。


在配置自定义策略时，您可将以下参考策略复制粘贴至输入框**编辑策略内容**，根据实际配置修改即可，具体信息可参见 [CAM 策略语法](https://intl.cloud.tencent.com/document/product/598/10604) 说明文档。


<span id="授权子账号对所有资源进行持久化操作"></span>
## 授权子账号对所有资源进行持久化操作

假设企业账号 CompanyExample（OwnerUin 为100000000001，APPID 为1250000000）下有一个子账号 Developer，该子账号需要对企业账号 CompanyExample 下的所有资源进行持久化处理。

通过 COS 设置该账号下全部资源的写入权限来实现数据万象子账号持久化操作授权。

**方案A：**

企业账号 CompanyExample 将预设策略 **QcloudCOSDataWriteOnly** 授权给子账号 Developer。授权方式请参见 [授权管理](https://intl.cloud.tencent.com/document/product/598/10602)。

**方案B：**

step1：通过策略语法方式创建以下策略。

```
{
    "version": "2.0",
    "statement": [
        {
            "effect": "allow",
            "action": [
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload"
            ],
            "resource": "*"
        }
    ]
}
```

step2：将该策略授权给子账号。授权方式请参见 [授权管理](https://intl.cloud.tencent.com/document/product/598/10602)。
 
 
 <span id="授权子账号对特定目录的资源进行持久化操作"></span>
## 授权子账号对特定目录的资源进行持久化操作
假设企业帐号 CompanyExample（OwnerUin 为100000000001，APPID 为1250000000）下有一个子账号 Developer，该子账号需要对企业帐号的存储桶（名为 examplebucket，所属地域为上海）中的 doc 目录下的资源进行持久化处理。

通过 COS 设置特定目录下资源的写入权限来实现数据万象的子账号持久化操作授权。

**方案A：**

通过 COS 控制台对资源进行 Policy 和 ACL 设置，具体请参见 COS [添加存储桶策略](https://intl.cloud.tencent.com/document/product/436/30927) 说明文档。

**方案B：**

step1：通过策略语法方式创建以下策略。

```
{
   "version": "2.0",
   "statement": [
       {
           "effect": "allow",
           "action": [
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload"
           ],
           "resource":"qcs::cos:ap-shanghai:uid/1250000000:examplebucket-1250000000/doc/*"    
 }
    ]
}
```

step2：将该策略授权给子账号，授权方式请参见 [授权管理](https://intl.cloud.tencent.com/document/product/598/10602)。

<span id="授权子账号对指定资源进行持久化操作"></span>
## 授权子账号对指定资源进行持久化操作

假设企业帐号 CompanyExample（OwnerUin 为100000000001，APPID 为1250000000）下有一个子账号 Developer，该子账号需要对企业帐号的存储桶（名为 examplebucket，所属地域为上海）中的 doc 目录下图片 picture.jpg 进行持久化处理。

通过 COS 设置特定资源的写入权限来实现数据万象子账号持久化操作授权。

**方案A：**

通过 COS 控制台对资源进行 Policy 和 ACL 设置，具体请参见 COS [添加存储桶策略](https://intl.cloud.tencent.com/document/product/436/30927) 说明文档。

**方案B：**

step1：通过策略语法方式创建以下策略。

```
{
   "version": "2.0",
   "statement": [
       {
           "effect": "allow",
           "action": [
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload"
           ],
      "resource":"qcs::cos:ap-shanghai:uid/1250000000:examplebucket-1250000000/doc/picture.jpg"      
 }
    ]
}
```

step2：将该策略授权给子账号，授权方式请参见 [授权管理](https://intl.cloud.tencent.com/document/product/598/10602)。

 
<span id="授权子账号对指定前缀的资源进行持久化操作"></span>
## 授权子账号对指定前缀的资源进行持久化操作

假设企业帐号 CompanyExample（OwnerUin 为100000000001，APPID 为1250000000）下有一个子账号 Developer，该子账号需要对企业帐号的存储桶（名为 examplebucket，所属地域为上海）中的 doc 目录下以 test 为前缀的资源进行持久化处理。

通过COS设置指定前缀资源的写入权限来实现数据万象子账号持久化操作授权。
 
**方案A：**

通过 COS 控制台对资源进行 Policy 和 ACL 设置，具体请参见 COS [添加存储桶策略](https://intl.cloud.tencent.com/document/product/436/30927) 说明文档。

**方案B：**

step1：通过策略语法方式创建以下策略。

```
{
   "version": "2.0",
   "statement": [
       {
           "effect": "allow",
           "action": [
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload"
           ],
      "resource":"qcs::cos:ap-shanghai:uid/1250000000:examplebucket-1250000000/doc/test*"      
 }
    ]
}
```
 
step2：将该策略授权给子账号，授权方式请参见 [授权管理](https://intl.cloud.tencent.com/document/product/598/10602)。

<span id="授权子账号对特定目录下所有资源进行持久化操作并禁止对该目录下指定文件操作"></span>
## 授权子账号对特定目录下所有资源进行持久化操作并禁止对该目录下指定文件操作

假设企业帐号 CompanyExample（OwnerUin 为100000000001，APPID 为1250000000）下有一个子账号 Developer，该子账号需要对企业帐号的存储桶（名为 examplebucket，所属地域为上海）中的 doc 目录下所有资源进行持久化处理，但禁止对picture.jpg 文件进行持久化处理。

通过 COS 设置指定文件的写入权限来实现数据万象子账号持久化操作授权。

**方案A：**

通过 COS 控制台进行 Policy 和 ACL 设置，具体请参见 COS [添加存储桶策略](https://intl.cloud.tencent.com/document/product/436/30927) 说明文档。


**方案B：**

step1：通过策略语法方式创建以下策略。

```
{
   "version": "2.0",
   "statement": [
{
           "effect": "allow",
           "action": [
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload"
           ],
           "resource":"qcs::cos:ap-shanghai:uid/1250000000:examplebucket-1250000000/doc/*"    
 },
 
       {
           "effect": "deny",
           "action": [
                "cos:ListParts",
                "cos:PostObject",
                "cos:PutObject*",
                "cos:InitiateMultipartUpload",
                "cos:UploadPart",
                "cos:UploadPartCopy",
                "cos:CompleteMultipartUpload",
                "cos:AbortMultipartUpload"
           ],
      "resource":"qcs::cos:ap-shanghai:uid/1250000000:examplebucket-1250000000/doc/picture.jpg"      
 }
    ]
}
```

step2：将该策略授权给子账号，授权方式请参见 [授权管理](https://intl.cloud.tencent.com/document/product/598/10602)。