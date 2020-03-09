### Why does the following exception occur when I use APIs with JNI?

```
Exception in thread "main" java.lang.UnsatisfiedLinkError:
com.tls.tls_sigcheck.tls_gen_signature_ex2(Ljava/lang/String;Ljava/lang/String;Ljava/lang/String;)I
        at com.tls.tls_sigcheck.tls_gen_signature_ex2(Native Method)
        at Demo.main(Demo.java:31)
```

After ruling out the possibility of an incorrect dynamic library path, check that the package path in the code is correct. API names are generated through the package path during JNI dynamic library compilation. Therefore, do not independently compile by modifying the package path in tls_sigcheck.java, otherwise the preceding problem occurs.

### Why does the following exception occur when I use APIs with JNI?

```
Exception in thread "main" java.lang.UnsatisfiedLinkError: *** Can't load IA 32-bit *** on a AMD 64-bit platform
```

This indicates a typical mismatch between JVM and the dynamic library. To correct it, use a 32-bit dynamic library to load a 32-bit JVM.


### How can I generate UserSig?
For details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

### What is the validity period of UserSig?

As an important credential for IM login authentication, UserSig has a default validity period of 180 days, which can only be modified through the native API. Other APIs and tools cannot modify the validity period. The validity period of UserSig can be set to a maximum of 50 years. We recommend that you set the validity period to 2 months for the security of your account. For more information, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385).

### Can I delete an account?

- Accounts in the **Professional Edition** cannot be deleted. To deactivate an account, you can call the **API for invalidating the account login state** to invalidate the login state of the account owner.
- Accounts in the **Trial Edition** can be deleted. You can call the **API for deleting accounts** to delete accounts that are no longer needed. **Note that user data cannot be restored after accounts are deleted.**

### Why do I encounter error 70009 upon login?

Check that the public and private keys match. Do not use the private key of the IM demo to generate UserSig.
