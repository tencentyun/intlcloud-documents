### JNI方式でAPIを使用すると次のような不具合が発生した場合、どうすればいいですか。

```
Exception in thread "main" java.lang.UnsatisfiedLinkError:
com.tls.tls_sigcheck.tls_gen_signature_ex2(Ljava/lang/String;Ljava/lang/String;Ljava/lang/String;)I
        at com.tls.tls_sigcheck.tls_gen_signature_ex2(Native Method)
        at Demo.main(Demo.java:31)
```

動的ライブラリパスが正しくないという原因を排除した後、コード内のpackageパスが正しいかどうかを確認してください。JNIの動的ライブラリのコンパイル時にインターフェース名がpackageパスを介して生成されるため、tls_sigcheck.java内のpackageパスを変更したコンパイルをしないでください。そうでない場合、上記の不具合が発生する可能性があります。

### JNI方式でAPIを使用すると次のような不具合が発生した場合、どうすればいいですか。

```
Exception in thread "main" java.lang.UnsatisfiedLinkError: *** Can't load IA 32-bit *** on a AMD 64-bit platform
```

それはJVMと動的ライブラリが一致しないことです。32ビットJVMの場合、32ビットの動的ライブラリを使用して読み込んでください。


### userSigの生成方法は。
詳細については、[UserSigの生成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

### userSigの有効期間は。

UserSigはIMログイン認証の重要な証明書として、デフォルトの有効期間は180日です。有効期間を変更するにはオリジナルなインターフェースしか使用できません。他のインターフェースやツールでは有効期間を変更することはできません。UserSigの有効期間は最大50年に設定できます。アカウントのセキュリティのためには、UserSigの有効期間を2ヶ月に設定することをお勧めします。詳細については、[UserSigの生成](https://intl.cloud.tencent.com/document/product/1047/34385)をご参照ください。

### アカウントは削除できますか。

- **Professional Edition**のアカウントは削除できません。今後アカウントを使用しない場合、Rest APIを使用して**アカウントログイン状態の無効化インターフェース**を呼び出し、アカウント所有者のログイン状態を無効化することができます。
- **体験版**のアカウントは削除できます。Rest APIを介して**アカウント削除インターフェース**を呼び出して使用しないアカウントを削除することができます。**削除後、そのユーザのデータは復元できません**ので、十分注意してください。

### ログイン時はエラー70009が表示されましたが、どうしますか。

パブリックキーとプライベートキーが一致するかどうかを確認してください。UserSigの生成にはIM Demoのプライベートキーを使用しないでください。
