## 現象の説明[](id:symptom)
SSHでLinux CVMへの正常なリモートログインができず、VNC方式でログインすると、システムの起動失敗が確認され、下図のように「Welcome to emergency mode」というメッセージが表示されます。
![](https://qcloudimg.tencent-cloud.cn/raw/dea541a48d2a01503c1dbbc85b0d396f.png)


## 考えられる原因
`/etc/fstab`の設定が不適切であることが原因という可能性があります。
例えば、`/etc/fstab`においてディスクがデバイス名で自動的にマウントされるように設定されている場合も、CVMを再起動するとデバイス名が変わってしまい、システムが正常に起動しなくなることがあります。


## 解決方法
[処理手順](#ProcessingSteps)を参照して`/etc/fstab`設定ファイルを修復し、サーバーを再起動してから検証します。


## 処理手順[](id:ProcessingSteps)

インスタンスにアクセスし、この問題を処理する方法は2つあります。

<dx-tabs>
::: 方法1：VNCを使用したログイン（推奨）[](id:useVNC)
1. [VNCを使用してLinuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32494)します。
2. VNCインターフェースに進み、[現象の説明](#symptom)のようなインターフェースが表示されたら、rootアカウントのパスワードを入力し、**Enter**を押してサーバーにログインしてください。
 - 入力されたパスワードは、デフォルトでは表示されません。
 - アカウントのパスワードをお持ちでない場合、または忘れてしまった場合は、方法2を参照して処理してください。
3. [](id:Step3)以下のコマンドを実行し、`/etc/fstab`ファイルのバックアップを取ります。ここでは、`/home`ディレクトリへのバックアップを例に取ります。
```shellsession
cp /etc/fstab /home
```
4. 以下のコマンドを実行し、VIエディタを使用して`/etc/fstab`ファイルを開きます。
```shellsession
vi /etc/fstab
```
5. 下図に示すように、**i**を押して編集モードに入り、カーソルを設定エラーの行の先頭に移動させ、`#`を入力して行の設定についてコメントアウトします。
<dx-alert infotype="explain" title="">
設定エラーを特定できない場合は、システムディスク以外のマウントされているすべてのディスクの設定についてコメントアウトし、サーバーが正常な状態に戻った後に[ステップ8](#Step7)を参照して設定することをお勧めします。
</dx-alert>
<img src="https://qcloudimg.tencent-cloud.cn/raw/1c238789186d7f24c0244e0307bc3a22.png"/>
6. [](id:Step6)**Esc**を押して**:wq** と入力した後、**Enter**を押して設定を保存し、エディタを終了します。
7. コンソールからインスタンスを再起動し、正常に起動、ログインできるかどうかを検証します。
<dx-alert infotype="explain" title="">
コンソールからインスタンスを再起動します。具体的な手順については、[インスタンスの再起動](https://intl.cloud.tencent.com/document/product/213/4928)をご参照ください。
</dx-alert>
8. [](id:Step8)ログインに成功した後、ディスクの自動マウントの設定が必要な場合は、[/etc/fstabファイルの設定](https://intl.cloud.tencent.com/document/product/362/40001)を参照し、対応する設定を行ってください。

:::
::: 方法2：レスキューモードの使用[](id:useRescue)
1. [レスキューモードの使用](https://intl.cloud.tencent.com/document/product/213/46157)を参照し、インスタンスレスキューモードに入ります。
<dx-alert infotype="notice" title="">
[レスキューモードの使用によるシステム修復](https://intl.cloud.tencent.com/document/product/213/46157#.E4.BD.BF.E7.94.A8.E6.95.91.E6.8F.B4.E6.A8.A1.E5.BC.8F.E8.BF.9B.E8.A1.8C.E7.B3.BB.E7.BB.9F.E4.BF.AE.E5.A4.8D)手順の中の`mount`と`chroot`の関連コマンドを実行し、業務そのものにアクセスできることを確認する必要があります。
</dx-alert>
2. 方法1の[ステップ3](#Step3) - [ステップ6](#Step6)に従って、`/etc/fstab`ファイルの修復を行います。
3. [レスキューモードの終了](https://intl.cloud.tencent.com/document/product/213/46157#.E9.80.80.E5.87.BA.E6.95.91.E6.8F.B4.E6.A8.A1.E5.BC.8F)を参照し、インスタンスのレスキューモードを終了します。
4. インスタンスがレスキューモードを終了すると、シャットダウン状態になります。[インスタンスの起動](https://intl.cloud.tencent.com/document/product/213/38168)を参照してシステムを起動し、起動後に正常にログインできることを確認してください。
5. ログインに成功した後、ディスクの自動マウントの設定が必要な場合は、[/etc/fstabファイルの設定](https://intl.cloud.tencent.com/document/product/362/40001)を参照し、対応する設定を行ってください。

:::
</dx-tabs>







