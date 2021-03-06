## 功能描述

本接口用于修改现有的索引信息。

## 请求

#### 请求示例

```
PUT /index HTTP/1.1
Host: <Region>.cls.myqcloud.com
Authorization: <AuthorizationString>
Content-Type: application/json
{
			"topic_id": "xxxx-xx-xx-xx-xxxxxxxx",
			"effective": true,
			"rule": {
				"full_text": {
					"case_sensitive": false,
					"tokenizer": "*{^&%"
				},
			    "key_value": {
					"case_sensitive": false,
					"keys": ["age","name"],
					"types": ["long","text"],
					"tokenizers": ["", "-"],
					"sql_flags":[true,false]
				},
				"tag": {
					"case_sensitive": false,
					"keys": ["age","name"],
					"types": ["long","text"],
					"tokenizers": ["", "-"],
					"sql_flags":[true,false]
				 }
			}
}
```

#### 请求行

```
PUT /index
```

#### 请求头

除公共头部外，无特殊请求头部。

#### 请求参数

| 字段名        |  类型  | 位置  |是否必填 |      含义                                      |
|--------------|--------|------|--------|-----------------------------------------------|
| topic_id     | string | body | 是      |修改的 index 属于的 topic ID                      |
| effective    | bool   | body | 是      |index 的开关状态                                |
| rule         | object | body | 否      |索引规则，当 effective 为 true 时必需               |


**平台用户专用参数**


| 字段名 | 类型 | 位置 | 是否必填 | 含义 |
|---------|---------|---------|---------|---------|
| custom_uin | long | body |  否 |  修改的 index 属于的客户 UIN |


rule 内容说明：

|  字段名     |  类型  | 是否必填 |        含义                    |
|------------|--------|---------|-------------------------------|
| full_text  | object | 否      | 全文索引的相关配置              |
| key_value  | object | 否      | kv 索引的相关配置               |

>! 设置 rule 时，full_text、key_value 两者至少要设置一个。

full_text 内容说明：

|  字段名     |  类型  | 是否必填 |        含义                    |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | 是      | 是否大小写敏感              |
| tokenizer | string | 否      | 全文索引的分词符，不允许为空，建议设置为<code>!@#%^&*()-_="', &lt;>/?\|\\;:\n\t\r[]{}</code> |

key_value 内容说明：

|  字段名     |  类型  | 是否必填 |        含义                    |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | 是      | 是否大小写敏感              |
| keys | array(string) | 是      | 需要建索引的 key 的名字            |
| types| array(string) | 是      | 需要建索引 的 key 对应的类型，一一对应，目前支持`long double text` |
| tokenizers| array(string) | 否      | 上面 key 对应的分词符，一一对应，只对`text`类型设置，其他类型为空字符串  |
| sql_flags| array(bool) | 否      | SQL 统计开关数组，默认值：false，表示对应键值不开启 SQL 统计；true：表示对应键值开启 SQL 统计  |

tag 内容说明：

|  字段名     |  类型  | 是否必填 |        含义                    |
|------------|--------|---------|-------------------------------|
| case_sensitive | bool | 是      | 是否大小写敏感              |
| keys | array(string) | 是      | 需要建索引的 key 的名字            |
| types| array(string) | 是      | 上面 key 对应的类型，一一对应，目前支持 `long double text` |
| tokenizers| array(string) | 否      | 上面 key 对应的分词符，一一对应，只对`text`类型设置，其他类型为空字符串  |
| sql_flags| array(bool) | 否      | SQL 统计开关数组，默认值：false，表示对应键值不开启 SQL 统计；true：表示对应键值开启 SQL 统计  |


## 响应

#### 响应示例

```
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 0
```

#### 响应头

除公共响应头部外，无特殊响应头部。

#### 响应参数

无。

## 错误码

参见 [错误码](https://intl.cloud.tencent.com/document/product/614/12402)。

