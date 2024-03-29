## 简介

本文档提供关于存储桶、对象的访问控制列表（ACL）的相关 API 概览以及 SDK 示例代码。

**存储桶 ACL**

| API                                                          | 操作名         | 操作描述                                |
| ------------------------------------------------------------ | -------------- | --------------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | 设置存储桶 ACL | 设置指定存储桶的访问权限控制列表（ACL） |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | 查询存储桶 ACL | 查询指定存储桶的访问权限控制列表（ACL） |

**对象 ACL**

| API                                                          | 操作名       | 操作描述                                      |
| ------------------------------------------------------------ | ------------ | --------------------------------------------- |
| [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748) | 设置对象 ACL | 设置存储桶中某个对象的访问控制列表 |
| [GET Object acl](https://intl.cloud.tencent.com/document/product/436/7744) | 查询对象 ACL | 查询对象的访问控制列表                |

## 存储桶 ACL
### 设置存储桶 ACL

#### 功能说明

设置指定存储桶的访问权限控制列表（PUT Bucket acl）。该操作是覆盖操作，会覆盖已有的权限设置。ACL 包括预定义权限策略（CannedAccessControlList）或者自定义的权限控制（AccessControlList）。两类权限当同时设置时将忽略预定义策略，以自定义策略为主。

#### 方法原型

```cpp
CosResult PutBucketACL(const PutBucketACLReq& request, PutBucketACLResp* response);
```

#### 请求示例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

// PutBucketACLReq 的构造函数需要传入 bucket_name
qcloud_cos::PutBucketACLReq req(bucket_name);
qcloud_cos::PutBucketACLResp resp;

// 设置 ACL 配置(可以通过 Body、Header 两种方式，但只能二选一，否则会有冲突)
// 1.通过 header 设置 ACL
req.SetXCosAcl("public-read-write");

// 2.通过 body 设置 ACL
qcloud_cos::Owner owner = {"qcs::cam::uin/00000000001:uin/00000000001", "qcs::cam::uin/00000000001:uin/00000000001" };
qcloud_cos::Grant grant;
req.SetOwner(owner);
grant.m_grantee.m_type = "Group";
grant.m_grantee.m_uri = "http://cam.qcloud.com/groups/global/AllUsers";
grant.m_perm = "READ";
req.AddAccessControlList(grant);

qcloud_cos::PutBucketACLResp resp;
qcloud_cos::CosResult result = cos.PutBucketACL(req, &resp);

if (result.IsSucc()) {
    // 请求成功
} else {
    // 请求失败，调用 CosResult 的成员函数输出错误信息，例如 requestID 等
} 
```

#### 参数说明

| 参数 | 参数描述                | 类型            | 是否必填  |
| ---- | ------------------------| ----------------| ------|
| req  | PutBucketACL 操作的请求  | PutBucketACLReq | 是    |
| resp | PutBucketACL 操作的响应  | PutBucketACLResp| 是    |

PutBucketACLReq 提供以下成员函数：

```
// 定义 Bucket 的 ACL 属性,有效值：private,public-read-write,public-read
// 默认值：private
void SetXCosAcl(const std::string& str);

// 赋予被授权者读的权限.格式：x-cos-grant-read: id=" ",id=" ".
// 当需要给子账号授权时,id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"
// 当需要给主账号授权时,id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantRead(const std::string& str);

// 赋予被授权者写的权限,格式：x-cos-grant-write: id=" ",id=" "./
// 当需要给子账号授权时,id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 当需要给主账号授权时,id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantWrite(const std::string& str);

// 赋予被授权者读写权限.格式：x-cos-grant-full-control: id=" ",id=" ".
// 当需要给子账号授权时,id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>",
// 当需要给主账号授权时,id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"
void SetXCosGrantFullControl(const std::string& str);

// Bucket 持有者 ID
void SetOwner(const Owner& owner);

// 设置被授权者信息与权限信息
void SetAccessControlList(const std::vector<Grant>& grants);

// 添加单个 Bucket 的授权信息
void AddAccessControlList(const Grant& grant);

```

> !SetXCosAcl、SetXCosGrantRead、SetXCosGrantWrite、SetXCosGrantFullControl 这类接口与 SetAccessControlList、AddAccessControlList 不可同时使用。因为前者实际是通过设置 HTTP Header 实现，而后者是在 Body 中添加了 XML 格式的内容，二者只能二选一。 SDK 内部优先使用第一类。

该请求涉及到的类定义如下：

```
struct Owner {
    // 存储桶持有者信息
    std::string m_id; // owner 的完整 ID，格式为：qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name;  // owner 的描述
};

struct Grantee {
    // type 类型可以为 RootAccount， SubAccount
    // 当 type 类型为 RootAccount 时，可以在 id 中 uin 填写账号 ID，也可以用 anyone（指代所有类型用户）代替 uin/<OwnerUin> 和 uin/<SubUin>
    // 当 type 类型为 RootAccount 时，uin 代表主账号，Subaccount 代表子账号
    std::string m_type; 
    std::string m_id; // qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name; // 非必选
    std::string m_uri;
};

struct Grant {
    Grantee m_grantee; // 被授权者资源信息
    std::string m_perm; // 指明授予被授权者的权限信息，可选值"READ"，"WRITE"，"FULL_CONTROL"
};

```

### 查询存储桶 ACL

#### 功能说明

查询指定存储桶的访问权限控制列表。

#### 方法原型

```cpp
CosResult GetBucketACL(const GetBucketACLReq& req, GetBucketACLResp* resp)
```

#### 请求示例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
std::string bucket_name = "examplebucket-1250000000";

qcloud_cos::GetBucketACLReq req(bucket_name);
qcloud_cos::GetBucketACLResp resp;
qcloud_cos::CosResult result = cos.GetBucketACL(req, &resp);

if (result.IsSucc()) {
    // 请求成功，调用 resp 的成员函数获取返回内容
} else {
    // 请求失败，可以调用 CosResult 的成员函数输出错误信息，例如 requestID 等
} 

```

#### 参数说明

| 参数 | 参数描述                | 类型            | 是否必填  |
| ---- | ------------------------| ----------------| ------|
| req  | GetBucketACL 操作的请求  | GetBucketACLReq | 是    |
| resp | GetBucketACL 操作的响应  | GetBucketACLResp| 是    |


GetBucketACLResp 提供以下成员函数：

```
std::string GetOwnerID();
std::string GetOwnerDisplayName();
std::vector<Grant> GetAccessControlList();
```

## 对象 ACL


### 设置对象 ACL

#### 功能说明

设置存储桶中某个对象的访问控制列表。

> !当前访问策略条目限制为1000条，如果您不需要进行对象 ACL 控制，请不要设置，默认继承 Bucket 权限。

ACL 包括预定义权限策略（CannedAccessControlList）或者自定义的权限控制（AccessControlList）。两类权限当同时设置时将忽略预定义策略，以自定义策略为主。

#### 方法原型

```cpp
CosResult PutObjectACL(const PutObjectACLReq& req, PutObjectACLResp* resp)
```

#### 请求示例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "test";

// 1 设置 ACL 配置（通过 Body, 设置 ACL 可以通过 Body、Header 两种方式，但只能二选一，否则会有冲突）
{   
    qcloud_cos::PutObjectACLReq req(bucket_name, object_name);
    qcloud_cos::Owner owner = {"qcs::cam::uin/xxxxx:uin/xxx", "qcs::cam::uin/xxxxxx:uin/xxxxx" };
    qcloud_cos::Grant grant;
    req.SetOwner(owner);
    grant.m_grantee.m_type = "Group";
    grant.m_grantee.m_uri = "http://cam.qcloud.com/groups/global/AllUsers";
    grant.m_perm = "READ";
    req.AddAccessControlList(grant);

    qcloud_cos::PutObjectACLResp resp;
    qcloud_cos::CosResult result = cos.PutObjectACL(req, &resp);
    if (result.IsSucc()) {
        // 请求成功
    } else {
        // 请求失败，可以调用 CosResult 的成员函数输出错误信息，例如 requestID 等
    } 
}   

// 2 设置 ACL 配置（通过 Header, 设置 ACL 可以通过 Body、Header 两种方式，但只能二选一，否则会有冲突）
{   
    qcloud_cos::PutObjectACLReq req(bucket_name, object_name);                                                                                                                    
    req.SetXCosAcl("public-read-write");

    qcloud_cos::PutObjectACLResp resp;
    qcloud_cos::CosResult result = cos.PutObjectACL(req, &resp);
    if (result.IsSucc()) {
        // 请求成功
    } else {
        // 请求失败，可以调用 CosResult 的成员函数输出错误信息，例如 requestID 等
    } 
}   
```


#### 参数说明

| 参数 | 参数描述                | 类型             | 是否必填  |
| ---- | ------------------------| -----------------| ------|
| req  | PutObjectACL 操作的请求  | PuttObjectACLReq | 是    |
| resp | PutObjectACL 操作的响应  | PutObjectACLResp | 是    |


PutObjectACLReq 包含以下成员函数：

```
// 定义 Object 的 ACL 属性,有效值：private,public-read
// 默认值：private
void SetXCosAcl(const std::string& str);

// 赋予被授权者读的权限。格式：id="[OwnerUin]" 
void SetXCosGrantRead(const std::string& str);

// 赋予被授权者所有的权限。格式：id="[OwnerUin]"
void SetXCosGrantFullControl(const std::string& str);

// Object 持有者 ID
void SetOwner(const Owner& owner);

// 设置被授权者信息与权限信息
void SetAccessControlList(const std::vector<Grant>& grants);

// 添加单个 Object 的授权信息
void AddAccessControlList(const Grant& grant);

```

> !SetXCosAcl/SetXCosGrantRead/SetXCosGrantWrite/SetXCosGrantFullControl 这类接口与  SetAccessControlList/AddAccessControlList 不可同时使用。因为前者实际是通过设置 HTTP Header 实现，而后者是在Body 中添加了 XML 格式的内容，二者只能二选一。SDK 内部优先使用第一类。

ACLRule 定义如下：

```
struct Grantee {
    // type 类型可以为 RootAccount， SubAccount
    // 当 type 类型为 RootAccount 时，可以在 id 中 uin 填写账号 ID，也可以用 anyone（指代所有类型用户）代替 uin/<OwnerUin> 和 uin/<SubUin>
    // 当 type 类型为 RootAccount 时，uin 代表主账号账号，Subaccount 代表子账号账号
    std::string m_type; 
    std::string m_id; // qcs::cam::uin/<OwnerUin>:uin/<SubUin>
    std::string m_display_name; // 非必选
    std::string m_uri;
};

struct Grant {
    Grantee m_grantee; // 被授权者资源信息
    std::string m_perm; // 指明授予被授权者的权限信息，可选值"READ"，"WRITE"，"FULL_CONTROL"
};

```

### 查询对象 ACL

#### 功能说明

查询对象的访问控制列表。

#### 方法原型

```cpp
CosResult GetObjectACL(const GetObjectACLReq& req, GetObjectACLResp* resp)
```

#### 请求示例

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);

std::string bucket_name = "examplebucket-1250000000";
std::string object_name = "exampleobject";

// GetObjectACLReq 的构造函数需要传入 Object_name
qcloud_cos::GetObjectACLReq req(bucket_name, object_name);
qcloud_cos::GetObjectACLResp resp;
qcloud_cos::CosResult result = cos.GetObjectACL(req, &resp);

if (result.IsSucc()) {
    // 请求成功，调用 resp 的成员函数获取返回内容
} else {
    // 请求失败，可以调用 CosResult 的成员函数输出错误信息，例如 requestID 等
} 
```

#### 参数说明

| 参数 | 参数描述                | 类型            | 是否必填  |
| ---- | ------------------------| ----------------| ------|
| req  | GetObjectACL 操作的请求  | GetObjectACLReq | 是    |
| resp | GetObjectACL 操作的响应  | GetObjectACLResp| 是    |


GetObjectACLResp 包含以下成员函数：

```
std::string GetOwnerID();
std::string GetOwnerDisplayName();
std::vector<Grant> GetAccessControlList();
```
