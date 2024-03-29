## 简介

本文档提供关于存储桶、对象的访问控制列表（ACL）的相关 API 概览以及 SDK 示例代码。

**存储桶 ACL**

| API                                                          | 操作名         | 操作描述                       |
| :----------------------------------------------------------- | :------------- | :----------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | 设置存储桶 ACL | 设置指定存储桶访问权限控制列表 |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | 查询存储桶 ACL | 查询存储桶的访问控制列表       |

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

```java
// 方法 1 (设置自定义策略)
public void setBucketAcl(String bucketName, AccessControlList acl)
  throws CosClientException, CosServiceException;
// 方法 2 (设置预定义策略)
public void setBucketAcl(String bucketName, CannedAccessControlList acl) throws CosClientException, CosServiceException;
// 方法 3 (以上两种方法的封装, 包含两种策略设置，如果同时设置以自定定义策略为主)
public void setBucketAcl(SetBucketAclRequest setBucketAclRequest) 
  throws CosClientException, CosServiceException;
```

#### 请求示例

[//]: # (.cssg-snippet-put-bucket-acl)
```java
// bucket的命名规则为 BucketName-APPID ，此处填写的存储桶名称必须为此格式
String bucketName = "examplebucket-1250000000";
// 设置自定义 ACL
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
// uin 可以在控制台查看到： https://console.cloud.tencent.com/developer
owner.setId("qcs::cam::uin/100000000001:uin/100000000001");
acl.setOwner(owner);
String id = "qcs::cam::uin/100000000001:uin/100000000001";
UinGrantee uinGrantee = new UinGrantee("qcs::cam::uin/100000000001:uin/100000000001");
uinGrantee.setIdentifier(id);
acl.grantPermission(uinGrantee, Permission.FullControl);
cosClient.setBucketAcl(bucketName, acl);

// 设置预定义 ACL
// 设置私有读写（默认新建的 bucket 都是私有读写）
cosClient.setBucketAcl(bucketName, CannedAccessControlList.Private);
// 设置公有读私有写
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicRead);
// 设置公有读写
cosClient.setBucketAcl(bucketName, CannedAccessControlList.PublicReadWrite);
```


#### 参数说明

方法3参数同时包含1和2，因此以方法3为例进行介绍。

| 参数名称            | 描述           | 类型                |
| ------------------- | -------------- | ------------------- |
| setBucketAclRequest | 权限设置请求类 | SetBucketAclRequest |

Request 成员说明：

| Request 成员 | 设置方法            | 描述                                                         | 类型                    |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName   | 构造函数或 set 方法 | Bucket 的命名规则为 BucketName-APPID，详情请参见 [存储桶概述](https://intl.cloud.tencent.com/document/product/436/13312) | String                  |
| acl          | 构造函数或 set 方法 | 自定义权限策略                                               | AccessControlList       |
| cannedAcl    | 构造函数或 set 方法 | 预定义策略如公有读、公有读写、私有读                         | CannedAccessControlList |

| 成员名         | 描述                            | 类型     |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | 包含所有要授权的信息            | 数组     |
| owner          | 表示 Object 或者 Owner 的拥有者 | Owner 类 |

Grant 类成员说明：

| 成员名     | 描述                                       | 类型       |
| ---------- | ------------------------------------------ | ---------- |
| grantee    | 被授权人的身份信息                         | Grantee    |
| permission | 被授权的权限信息（如可读，可写，可读可写） | Permission |

Owner 类成员说明：

| 成员名      | 描述                           | 类型   |
| ----------- | ------------------------------ | ------ |
| id          | 拥有者的身份信息               | String |
| displayname | 拥有者的名字（目前和 id 相同） | String |

CannedAccessControlList 表示预设的策略，针对的是所有人。是一个枚举类，枚举值如下所示：

| 枚举值          | 描述                                             |
| --------------- | ------------------------------------------------ |
| Private         | 私有读写（仅有 owner 可以读写）                  |
| PublicRead      | 公有读私有写（ owner 可以读写， 其他客户可以读） |
| PublicReadWrite | 公有读写（即所有人都可以读写）                   |

#### 返回结果说明

- 成功：无返回值。
- 失败：发生错误（如身份认证失败）， 抛出异常 CosClientException 或者 CosServiceException。 详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。


### 查询存储桶 ACL

#### 功能说明

查询指定存储桶的访问权限控制列表。

#### 方法原型

```plaintext
public AccessControlList getBucketAcl(String bucketName)
       throws CosClientException, CosServiceException
```

#### 请求示例

[//]: # (.cssg-snippet-get-bucket-acl)
```java
// bucket的命名规则为 BucketName-APPID ，此处填写的存储桶名称必须为此格式
String bucketName = "examplebucket-1250000000";
AccessControlList accessControlList = cosClient.getBucketAcl(bucketName);
// 将存储桶权限转换为预设 ACL, 可选值为：Private, PublicRead, PublicReadWrite
CannedAccessControlList cannedAccessControlList = accessControlList.getCannedAccessControl();
```


#### 参数说明

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | Bucket 的命名格式为 BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312#.E5.AD.98.E5.82.A8.E6.A1.B6.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | String |

#### 返回结果说明

- 成功：返回一个 Bucket 的 ACL。 
- 失败：发生错误（如身份认证失败）， 抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

## 对象 ACL


### 设置对象 ACL

#### 功能说明

设置存储桶中某个对象的访问控制列表。

ACL 包括预定义权限策略（CannedAccessControlList）或者自定义的权限控制（AccessControlList）。两类权限当同时设置时将忽略预定义策略，以自定义策略为主。

#### 方法原型

```java
// 方法1 (设置自定义策略)
public void setObjectAcl(String bucketName, String key, AccessControlList acl)
       throws CosClientException, CosServiceException
// 方法2 (设置预定义策略)
public void setObjectAcl(String bucketName, String key, CannedAccessControlList acl)
       throws CosClientException, CosServiceException
// 方法3 (以上两种方法的封装, 包含两种策略设置，如果同时设置以自定定义策略为主)
public void setObjectAcl(SetObjectAclRequest setObjectAclRequest)
  throws CosClientException, CosServiceException;
```

#### 请求示例

[//]: # (.cssg-snippet-put-object-acl)
```java
// 权限信息中身份信息有格式要求，对于主账号与子账号的范式如下：
// uin 可以在控制台查看到： https://console.cloud.tencent.com/developer
// 下面的 root_uin 和 sub_uin 都必须是有效的 UIN 号
// 主账号 qcs::cam::uin/<root_uin>:uin/<root_uin> 表示授予主账号 root_uin 这个用户（即前后填的 uin 一样）
//  如 qcs::cam::uin/100000000001:uin/100000000001
// 子账号 qcs::cam::uin/<root_uin>:uin/<sub_uin> 表示授予 root_uin 的子账号 sub_uin 这个客户
//  如 qcs::cam::uin/100000000001:uin/100000000011 
// 存储桶的命名格式为 BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
// 设置自定义 ACL
AccessControlList acl = new AccessControlList();
Owner owner = new Owner();
// 设置 owner 的信息, owner 只能是主账号
owner.setId("qcs::cam::uin/100000000001:uin/100000000001");
acl.setOwner(owner);

// 授权给主账号100000000001可读可写权限
UinGrantee uinGrantee1 = new UinGrantee("qcs::cam::uin/100000000001:uin/100000000001");
acl.grantPermission(uinGrantee1, Permission.FullControl);
cosClient.setObjectAcl(bucketName, key, acl);

// 设置预定义 ACL
// 设置私有读写（Object 的权限默认集成 Bucket的）
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.Private);
// 设置公有读私有写
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.PublicRead);
// 设置公有读写
cosClient.setObjectAcl(bucketName, key, CannedAccessControlList.PublicReadWrite);
```


#### 参数说明

- **方法3** 参数同时包含1和2，因此以方法3为例进行介绍。

| 参数名称            | 描述   | 类型                |
| ------------------- | ------ | ------------------- |
| SetObjectAclRequest | 请求类 | setObjectAclRequest |

Request 成员说明：

| Request 成员 | 设置方法          | 描述                                                         | 类型                    |
| ------------ | ------------------- | ------------------------------------------------------------ | ----------------------- |
| bucketName   | 构造函数或 set 方法 | 存储桶的命名格式为 BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312#.E5.AD.98.E5.82.A8.E6.A1.B6.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | String                  |
| key          | 构造函数或 set 方法 | 对象键（Key）是对象在存储桶中的唯一标识。例如，在对象的访问域名 `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg` 中，对象键为 doc/picture.jpg，详情请参见 [对象键](https://intl.cloud.tencent.com/document/product/436/13324) | String                  |
| acl          | 构造函数或 set 方法 | 自定义权限策略                                               | AccessControlList       |
| cannedAcl    | 构造函数或 set 方法 | 预定义策略如公有读、公有读写、私有读                         | CannedAccessControlList |

| 成员名         | 描述                            | 类型     |
| -------------- | ------------------------------- | -------- |
| List&lt;Grant> | 包含所有要授权的信息            | 数组     |
| owner          | 表示 Object 或者 Owner 的拥有者 | Owner 类 |

Grant 类成员说明：

| 成员名     | 描述                                         | 类型       |
| ---------- | -------------------------------------------- | ---------- |
| grantee    | 被授权人的身份信息                           | Grantee    |
| permission | 被授权的权限信息（例如可读、可写、可读可写） | Permission |

Owner 类成员说明：

| 成员名      | 描述                           | 类型   |
| ----------- | ------------------------------ | ------ |
| id          | 拥有者的身份信息               | String |
| displayname | 拥有者的名字（目前和 ID 相同） | String |

CannedAccessControlList 表示预设的策略，针对的是所有人。是一个枚举类，枚举值如下所示：

| 枚举值          | 描述                                             |
| --------------- | ------------------------------------------------ |
| Private         | 私有读写（仅有 owner 可以读写）                  |
| PublicRead      | 公有读私有写（ owner 可以读写， 其他客户可以读） |
| PublicReadWrite | 公有读写（即所有人都可以读写）                   |

#### 返回结果说明

- 成功：无返回值。
- 失败：发生错误（如身份认证失败），抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。

### 查询对象 ACL

#### 功能说明

查询对象的访问控制列表。

#### 方法原型

```java
public AccessControlList getObjectAcl(String bucketName, String key)
  throws CosClientException, CosServiceException;
```

#### 请求示例

[//]: # (.cssg-snippet-get-object-acl)
```java
// 存储桶的命名格式为 BucketName-APPID
String bucketName = "examplebucket-1250000000";
String key = "exampleobject";
AccessControlList accessControlList = cosClient.getObjectAcl(bucketName, key);
// 将文件权限转换为预设 ACL, 可选值为：Private, PublicRead, Default
CannedAccessControlList cannedAccessControlList = accessControlList.getCannedAccessControl();
```


#### 参数说明

| 参数名称   | 描述                                                         | 类型   |
| ---------- | ------------------------------------------------------------ | ------ |
| bucketName | 存储桶的命名格式为 BucketName-APPID，详情请参见 [命名规范](https://intl.cloud.tencent.com/document/product/436/13312#.E5.AD.98.E5.82.A8.E6.A1.B6.E5.91.BD.E5.90.8D.E8.A7.84.E8.8C.83) | String |
| key        | 对象键（Key）是对象在存储桶中的唯一标识。例如，在对象的访问域名`examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/picture.jpg`中，对象键为 doc/picture.jpg，详情请参见 [对象键](https://intl.cloud.tencent.com/document/product/436/13324) | String |

#### 返回结果说明

- 成功：返回一个 Object 所在的 ACL。
- 失败：发生错误（如身份认证失败）， 抛出异常 CosClientException 或者 CosServiceException。详情请参见 [异常处理](https://intl.cloud.tencent.com/document/product/436/31537)。
