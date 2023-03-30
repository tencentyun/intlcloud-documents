>### What should I do if the following issue occurs when I use APls with JNI?
>
>```
>Exception in thread "main" java.lang.UnsatisfiedLinkError:
>com.tls.tls_sigcheck.tls_gen_signature_ex2(Ljava/lang/String;Ljava/lang/String;Ljava/lang/String;)I
>        at com.tls.tls_sigcheck.tls_gen_signature_ex2(Native Method)
>        at Demo.main(Demo.java:31)
>```
>
>After ruling out the possibility of an incorrect dynamic library path, check whether the package path in the code is correct. API names are generated through the package path during JNI dynamic library compilation. Therefore, do not compile by modifying the package path in `tls_sigcheck.java`, otherwise, the above issue will occur.
>
>### What should I do if the following issue occurs when I use APls with JNI?
>
>```
>Exception in thread "main" java.lang.UnsatisfiedLinkError: *** Can't load IA 32-bit *** on a AMD 64-bit platform
>```
>
>This indicates a typical mismatch between JVM and the dynamic library. To fix it, use a 32-bit dynamic library to load a 32-bit JVM.
>
>
>### How can I generate a UserSig?
>For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).
>
>### What is the validity period of UserSig?
>
>As an important credential for IM login authentication, UserSig has a default validity period of 180 days, which can only be modified through the native API. Other APIs and tools cannot modify the validity period. The validity period of UserSig can be set to a maximum of 50 years. You are advised to set the validity period to two months for your account security. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).
>
>### Can I delete an account?
>
>- Accounts in the **Pro Edition** cannot be deleted. To deactivate an account, you can call the [v4/im_open_login_svc/kick](https://intl.cloud.tencent.com/document/product/1047/34957) API to invalidate the login state of the account owner.
>- Accounts in the **Free Edition** can be deleted. You can call the [v4/im_open_login_svc/account_delete](https://intl.cloud.tencent.com/document/product/1047/34955) API to delete accounts that are no longer needed. Note that **user data cannot be recovered after accounts are deleted**.
>
>### Why do I encounter error 70009 upon login?
>Check whether the public and private keys match. Do not use the private key of the IM demo to generate UserSig.
>
>### What should I do if the following issues occur when the IM account is not imported?
>- **Error 10019 is reported:**
>The UserID in the request does not exist. Check whether each `Member_Account` in `MemberList` is correct.
>- **Error 10007 is reported:**
>You do not have the operation permissions. (For example, a common member in a public group attempts to remove a member from the group, but only the app administrator has the permission to do so.)
>- **Error 20003 is reported:**
>The UserID of the sender or recipient is invalid or does not exist. Check whether the UserID has been imported into the IM console.
>
>>?You need to generate accounts and import them into IM via an API call. The accounts can be used only after imported.
