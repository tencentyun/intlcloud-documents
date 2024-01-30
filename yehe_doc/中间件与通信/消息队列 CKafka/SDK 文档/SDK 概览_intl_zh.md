消息队列 CKafka 版支持多语言 SDK，客户端可以通过 VPC 网络和公网访问两种方式接入 CKafka 并收发消息。两种接入方式对应的协议说明如下：

| 网络 | VPC 网络                                                     | 公网域名接入                                         |
| :--- | ------------------------------------------------------------ | ---------------------------------------------------- |
| 协议 | <li>PLAINTEXT</li><li>SASL_PLAINTEXT</li><li>SASL_SSL（专业版支持）</li> | <li>SASL_PLAINTEXT</li><li>SASL_SSL（专业版支持）</li> |

各语言 SDK 的使用方式如下：
<table>
<thead>
<tr>
<th>SDK 类型</th>
<th>文档</th>
</tr>
</thead>
<tbody><tr>
<td>Java SDK</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/597/40056">VPC 网络接入</a></li><li><a href="https://intl.cloud.tencent.com/document/product/597/40057">公网 SASL_PLAINTEXT 方式接入</a></li><li><a href="https://intl.cloud.tencent.com/document/product/597/43838">公网 SASL_SSL 方式接入</a></li>
<li><a href="https://intl.cloud.tencent.com/document/product/597/46795">VPC 网络 SASL_SCRAM 方式接入</a></li></td>
</tr>
<tr>
<td>Python SDK</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/597/40452">VPC 网络接入</a></li><li><a href="https://intl.cloud.tencent.com/document/product/597/40453">公网 SASL_PLAINTEXT 方式接入</a></li><li><a href="https://intl.cloud.tencent.com/document/product/597/43839">公网 SASL_SSL 方式接入</a></li></td>
</tr>
<tr>
<td>Go SDK</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/597/40059">VPC 网络接入</a></li><li><a href="https://intl.cloud.tencent.com/document/product/597/40060">公网 SASL_PLAINTEXT 方式接入</a></li></td>
</tr>
<tr>
<td>PHP SDK</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/597/40062">VPC 网络接入</a></li><li><a href="https://intl.cloud.tencent.com/document/product/597/40063">公网 SASL_PLAINTEXT 方式接入</a></li></td>
</tr>
<tr>
<td>C++ SDK</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/597/40065">VPC 网络接入</a></li><li><a href="https://intl.cloud.tencent.com/document/product/597/40066">公网 SASL_PLAINTEXT 方式接入</a></li></td>
</tr>
<tr>
<td>Node.js SDK</td>
<td><li><a href="https://intl.cloud.tencent.com/document/product/597/40449">VPC 网络接入</a></li><li><a href="https://intl.cloud.tencent.com/document/product/597/40450">公网 SASL_PLAINTEXT 方式接入</a></li></td>
</tr>
</tbody></table>
