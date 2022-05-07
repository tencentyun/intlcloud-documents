##故障について
SSHを使用してLinuxインスタンスにログインする際、SSHコマンドが「Last login:」関連情報を出力した後にロックされました。


## 考えられる原因
`/etc/profile`ファイルが変更されたことにより、`/etc/profile`内に `/etc/profile`をコールする現象が発生した可能性があります。そうなると、コールが無限ループ状態になり、ログインができなくなります。



## ソリューション
[処理手順](#ProcessingSteps)を参照し、`/etc/profile`ファイルをチェックして修復します。


## 処理手順[](id:ProcessingSteps)
- [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)。
2. 以下のコマンドを実行し、`/etc/profile`ファイルを確認します。
```
vim  /etc/profile
```
3. `/etc/profile`ファイル内に`/etc/profile`関連コマンドが含まれるかどうかをチェックします。
 - 含まれる場合は、次の手順に進んでください。
 - 含まれない場合は、[チケットを提出](https://console.intl.cloud.tencent.com/workorder/category)して連絡し、サポートを受けてください。
4. **i**で編集モードに入り、`/etc/profile`関連コマンドの前に`#`を追加してそのコマンドにコメントします。
5. **Esc**を押して編集モードを終了し、**:wq**を入力して変更を保存します。
6. 再度[SSHを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32501) でログインします。
