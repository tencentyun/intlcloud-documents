## 現象の説明
VNCを使用してCVMにログインすると、システムに正常にアクセスできず、「Cannot allocate memory」というエラー情報が表示されます。下図のとおりです。
![](https://main.qcloudimg.com/raw/0a31fdd909701c27c9923b2fff24668a.png)

## 考えられる原因[](id:PossibleCauses)
システム内に複数のラージページメモリが存在することが原因と考えられます。ラージページメモリはデフォルトで2048KBを占有し、`/etc/sysctl.conf`のラージページメモリの数に基づいて計算されます。以下の図は例で、1280ラージページメモリは2.5Gに相当します。インスタンスの構成は低めでも、2.5Gがまだラージページメモリプール(Huge Pages pool)に割り当てられている場合、システムには使用可能なメモリがなくなり、再起動後にシステムに入れなくなります。
![](https://main.qcloudimg.com/raw/1978a0b2a85fc828674f720c108c48a3.png)


## 解決方法
1. [処理手順](#ProcessingSteps)を参照して、プロセス総数が限度を超えていないかどうか確認してください。 
2. ラージページのメモリ構成を確認し、適切な構成に変更します。


## 処理手順[](id:ProcessingSteps)
1. [ログエラーfork：Cannot allocate memory](https://intl.cloud.tencent.com/document/product/213/40502)を参照して、プロセス数が限度を超えていないかどうか確認してください。プロセス数が限度を超えていない場合は、次の手順に進んでください。
2. シングルユーザーモードでCVMにログインします。[詳細については、Linux CVMを設定してシングルユーザーモードに入る](https://intl.cloud.tencent.com/document/product/213/34819)をご参照ください。
3. 以下のコマンドを実行して、[考えられる原因](#PossibleCauses)を参照し、ラージページのメモリ構成を確認します。
```
cat /etc/sysctl.conf | grep hugepages
```
ラージページメモリが複数ある場合は、以下の手順に従って構成を変更してください。
4. 以下のコマンドを実行して、VIMエディタを使用し`/etc/sysctl.conf`構成ファイルを開きます。
```
vim /etc/sysctl.conf
```
5. ** i **を押して編集モードに入り、インスタンスの実際の設定を加味して`vm.nr_hugepages`の設定項目を適切な値まで減らします。
6. **Esc**を押して**:wq**と入力し、次に**Enter**を押してVIMエディタを保存して終了します。
7. 以下のコマンドを実行して、直ちに設定を有効にします。
```
sysctl -p
```
8. 構成の完了後、CVMを再起動すればログインを再開できます。
