## 操作シナリオ
CBSはクラウド上の拡張可能なストレージデバイスです。ストレージキャパシティを追加するため、ユーザーはCBS作成後、CBS上の既存のデータを失うことなくいつでもサイズを拡張できます。
CBSの拡張完了後、 [パーティションおよびファイルシステムの拡張（Windows）](https://intl.cloud.tencent.com/document/product/362/31601)または[パーティションおよびファイルシステムの拡張（Linux）](https://intl.cloud.tencent.com/document/product/362/31602)を実行し、拡張部分の容量を既存のパーティション内に区分するか、または独立した新しいパーティションにフォーマットする必要があります。
>!MBR形式のパーティションが対応するディスクの最大容量は2TBです。ハードディスクパーティションがMBR形式で2TBを超える拡張が必要な場合、データディスクを再度作成してマウントし、GPTパーティション方法を使用した後、データを新しいディスクにコピーすることを推奨します。

## データディスクの拡張
拡張タイプがデータディスクのCBSの場合、以下の3つの方法で拡張することができます。
>!CVM上に複数の容量およびタイプがすべて同じCBSがマウントされている場合は、 [パーティションデータディスク](#distinguish)操作を参照して区分することができます。拡張するデータディスクを選択後、以下の方法で拡張します。
>

<dx-tabs>
::: CVMコンソールを介した拡張（推奨）[](id:useCVMConsole)
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. 対象のCVMがある行の【その他】>【リソース調整】>【CBS拡張】を選択します。
3. ポップアップされた「CBS拡張」ウィンドウで拡張するデータディスクを選択し、【次のステップ】をクリックします。
4. 「容量の調整」ステップで、対象の容量（現在の容量以上である必要があります）を設定し、【次のステップ】をクリックします。
5. 「パーティションおよびファイルシステムの拡張」の手順で、注意事項を確認し、【調整開始】をクリックすれば完了です。下図のとおりです。
![](https://main.qcloudimg.com/raw/dad3bd1f80569718a74a70df1579c4de.png)
6. 対象のクラウドサービスのオペレーティングシステムタイプに応じて、[パーティションおよびファイルシステムの拡張（Windows）](https://intl.cloud.tencent.com/document/product/362/31601)または[パーティションおよびファイルシステムの拡張（Linux）](https://intl.cloud.tencent.com/document/product/362/31602)を実行し、拡張部分の容量を既存のパーティション内に区分するか、または独立した新しいパーティションにフォーマットする必要があります。
:::
::: CBSコンソールを介した拡張[](id:useCBSConsole)
1. [CBSコンソール](https://console.cloud.tencent.com/cvm/cbs)にログインします。
2. ターゲットCBSの【もっと見る】>【クラウドディスクタイプの調整】を選択します。
3. 必要な新しい容量を選択します（現在の容量以上である必要があります。）。
4. 支払いを完了します。
5. 対象のクラウドサービスのオペレーティングシステムタイプに応じて、 [パーティションおよびファイルシステムの拡張（Windows）](https://intl.cloud.tencent.com/document/product/362/31601)または[パーティションおよびファイルシステムの拡張（Linux）](https://intl.cloud.tencent.com/document/product/362/31602)を実行し、拡張部分の容量を既存のパーティション内に区分するか、または独立した新しいパーティションにフォーマットする必要があります。
:::
::: \sAPI\sを介した拡張[](id:useAPI)
ResizeDiskインターフェースを使用して指定のエラスティックCBSを拡張できます。具体的な操作は[CBS拡張](https://intl.cloud.tencent.com/document/product/362/16310)をご参照ください。
:::
</dx-tabs>



## システムディスクの拡張[](id:useCVMconsole)
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、対象のCVMがある行の【その他】>【リソース調整】>【CBS拡張】を選択します。
2. ポップアップされた「CBS拡張」ウィンドウで拡張するシステムディスクを選択し、【次のステップ】をクリックします。
3. 「容量の調整」ステップで、対象の容量（現在の容量以上である必要があります）を設定し、【次のステップ】をクリックします。
4. 「パーティションおよびファイルシステムの拡張」の手順で、注意事項を確認し、「強制シャットダウンに同意する」を選択した後、【調整開始】をクリックすれば完了です。下図のとおりです。
![](https://main.qcloudimg.com/raw/b3702c6323dfd650665a1293db56b295.png)
5. コンソールの拡張操作完了後、CVMの実際のオペレーティングシステムに応じて[Linuxインスタンスのcloudinit設定を確認](#confirmLinuxConfig)するか、[Windowsインスタンスのcloudinit設定を確認](#confirmwindowsConfig)し、確認結果に基づき、必要に応じてパーティションの拡張とファイルシステム操作を行ってください。



## 関連操作
### データディスクのパーティション[](id:distinguish)
CVMが実際に使用するオペレーティングシステムに基づいて確認方法を選択できます。
<dx-tabs>
::: Linux
1. [Linuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5436)。
2. 以下のコマンドを実行して、CBSとデバイス名の間の対応関係を確認します。
```
ls -l /dev/disk/by-id
```
返された結果は、次のように示されます。
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)
そのうち、`disk-xxxx`はCBSのIDで、[CBSコンソール](https://console.cloud.tencent.com/cvm/cbs)に進み確認できます。
:::
::: Windows

1. [Windowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5435)。
2. <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-6px 0px">を右クリックして、【実行】を選択します。
3. 「実行」ウィンドウで`cmd`と入力して**Enter**を押します。
4. 以下のコマンドを実行して、CBSとデバイス名の間の対応関係を確認します。
```
wmic diskdrive get caption,deviceid,serialnumber
```
または、次のコマンドを実行します。
```
wmic path win32_physicalmedia get SerialNumber,Tag
```
返された結果は、次のように示されます。
![](https://main.qcloudimg.com/raw/e91aa2f938ddda304844d7ac28840859.png)
そのうち、`disk-xxxx`はCBSのIDで、[CBSコンソール](https://console.cloud.tencent.com/cvm/cbs)に進み確認できます。
:::
</dx-tabs>

### インスタンスのcloudinit設定を確認する
CVMが実際に使用するオペレーティングシステムに基づいて確認方法を選択できます。
<dx-tabs>
::: \sLinux\sインスタンス\scloudinit\s設定[](id:confirmLinuxConfig)を確認します
拡張操作の完了後、[Linuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5436)して、`/etc/cloud/cloud.cfg`にgrowpartおよびresizefsの設定項目が含まれているかどうか確認します。
 - 含まれる場合、その他の操作の必要はありません。次のように示されます。
![](https://main.qcloudimg.com/raw/03d38f34651d317176c50f1ed3a03f30.png)
    - **growpart**：パーティションをディスクサイズに拡張します。
    - **resizefs**：`/`パーティションファイルシステムを調整してパーティションサイズに拡張します。
 - 含まない場合、対象のクラウドサービスのオペレーティングシステムタイプに応じて、手動でファイルシステムとパーティションを拡張する必要があります。[パーティションおよびファイルシステムの拡張（Linux）](https://intl.cloud.tencent.com/document/product/362/31602)を実行し、拡張部分の容量を既存のパーティションに区分するか、新しい独立したパーティションにフォーマットする必要があります。
:::
::: \sWindows\sインスタンス\scloudinit\s設定[](id:confirmwindowsConfig)を確認します
拡張操作の完了後、 [Windowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5435)して、`C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf\cloudbase-init.conf` のpluginにExtendVolumesPlugin設定項目が含まれているかどうか確認してください。
 - 含まれる場合、その他の操作の必要はありません。
 - 含まない場合、対象のクラウドサービスのオペレーティングシステムタイプに応じて、手動でファイルシステムとパーティションを拡張する必要があります。[パーティションおよびファイルシステムの拡張（Windows）](https://intl.cloud.tencent.com/document/product/362/31601)を実行し、拡張部分の容量を既存のパーティション内に区分するか、新しい独立したパーティションにフォーマットする必要があります。
:::
</dx-tabs>
