>### JNI 方式使用 API 出现下面的问题该如何处理？
>
>```
>Exception in thread "main" java.lang.UnsatisfiedLinkError:
>com.tls.tls_sigcheck.tls_gen_signature_ex2(Ljava/lang/String;Ljava/lang/String;Ljava/lang/String;)I
>        at com.tls.tls_sigcheck.tls_gen_signature_ex2(Native Method)
>        at Demo.main(Demo.java:31)
>```
>
>排除动态库路径不正确的因素后，请确认代码中 package 路径是否正确，因为 JNI 动态库在编译时，接口的名称都是通过 package 路径生成的，所以不要尝试修改 tls_sigcheck.java 中的 package 路径自行编译，如此会导致上述问题。
>
>### JNI 方式使用 API 出现下面问题该如何处理？
>
>```
>Exception in thread "main" java.lang.UnsatisfiedLinkError: *** Can't load IA 32-bit *** on a AMD 64-bit platform
>```
>
>典型的 JVM 与动态库不匹配，请32位 JVM 使用32位动态库进行加载。
>
>
>### 如何生成 UserSig？
>详情请参见 [生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)。
>
>### UserSig 有效期是多久？
>
>UserSig 作为即时通信 IM 登录鉴权的重要凭证，默认有效期为180天，只能通过原生接口修改有效期，其他接口与工具不能修改有效期。UserSig 有效期最长可以设置为50年，为了您的帐号安全建议将 UserSig 有效期设置为两个月。详情可参阅 [生成 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385)。
>
>### 帐号是否可以删除？
>
>- **专业版**中的帐号不允许删除，如果您无需继续使用某个帐号，您可以通过 Rest  API 调用 [帐号登录状态失效接口](https://intl.cloud.tencent.com/document/product/1047/34957) 使该帐号所有者的登录状态失效。
>- **体验版**中的帐号支持删除，您可以通过 Rest  API 调用 [帐号删除接口](https://intl.cloud.tencent.com/document/product/1047/34955) 删除不再使用的帐号，**删除后该用户的数据将无法恢复**，请谨慎处理。
>
>### 登录报错70009？
>请检查公私钥是否匹配，请不要使用即时通信 IM Demo 的私钥来生成 UserSig。
>
>### IM 账号未导入出现下面问题该如何处理？
>- **加群失败，可能传参等问题造成未导入成功，报错10019？**
>请求的 UserID 不存在，请检查 MemberList 中的所有 Member_Account 是否正确。
>- **发送消息和更新资料权限不足，报错10007？**
>操作权限不足（例如 Public 群组中普通成员尝试执行踢人操作，但只有 App 管理员才有权限；或者非群成员操作）。
>- **消息发送方或接收方 UserID 无效或不存在，报错 20003？**
>消息发送方或接收方 UserID 无效或不存在，请检查 UserID 是否已导入即时通信 IM。
>
>>?账号需客户自行生成，使用导入接口决定将哪些账号导入到 IM 中，只有导入之后才能正常使用。
