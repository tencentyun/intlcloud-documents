## 概要
クラウドディスクはクラウド上の拡張可能なストレージデバイスです。ユーザーは、クラウドディスクの作成後、いつでも容量を拡張して、データを失うことなくストレージ容量を増やすことができます。
クラウドディスクを拡張した後、パーティションとファイルシステムを拡張する必要があります。拡張した容量を既存のパーティションに分割したり、別々の新しいパーティションにフォーマットしたりすることができます。


<dx-alert infotype="notice" title="">
MBRパーティションは、最大2TB の容量のディスクをサポートします。2TBを超える容量のディスクをパーティション分割する場合は、新しいデータディスクを作成してマウントし、GPT パーティション形式を使用してデータを新しいディスクにコピーすることをお勧めします。
</dx-alert>


## データディスクの拡張
クラウドディスクがデータディスクの場合、次の 3 つの方法で拡張することができます。


<dx-alert infotype="notice" title="">
CVMに同じ容量・種類の複数のクラウドディスクが接続されている場合、[データディスクの区分](#distinguish)に示す方法で区分できます。拡張するデータディスクを選択後、次の手順に従ってその容量を拡張します。
</dx-alert>



<dx-tabs>
::: CVMコンソールを介した拡張（推奨）[](id:useCVMConsole)
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index) にログインします。
2. ターゲットCVMの右側にある**さらに**>**リソース調整**>**CBSを拡張**をクリックします。
3. 「CBSを拡張」画面が表示されます。この画面で拡張するデータディスクを選択し、**次へ**をクリックします。
4. 目標容量（現在の容量以上である必要があります）を設定し、**次へ**をクリックします。
5. 注意事項を読み、**変更を開始**をクリックします。下図に示すように：
![](https://staticintl.cloudcachetci.com/yehe/backend-news/rcu7553_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421164941.png)
6. ターゲットCVMのOSに応じて、[パーティションとファイルシステム（Windows）を拡張する](https://intl.cloud.tencent.com/document/product/362/6737)、または[パーティションとファイルシステム（Linux）を拡張する](https://intl.cloud.tencent.com/document/product/362/6738)必要があり、拡張された容量を既存のパーティションに割り当てるか、独立した新しいパーティションにフォーマットします。
:::
::: CBSコンソールを介した拡張[](id:useCBSConsole)
1. [CBSコンソール](https://console.cloud.tencent.com/cvm/cbs)にログインします。
2. ターゲットCBSの右側にある**さらに**>**スケールアウト**をクリックします。
3. 必要な新しい容量を選択します（現在の容量以上である必要があります。）。
4. お支払いをしてください。
5. ターゲットCVMのOSに応じて、[パーティションとファイルシステム（Windows）を拡張する](https://intl.cloud.tencent.com/document/product/362/6737)、または[パーティションとファイルシステム（Linux）を拡張する](https://intl.cloud.tencent.com/document/product/362/6738)必要があり、拡張された容量を既存のパーティションに割り当てるか、独立した新しいパーティションにフォーマットします。
:::
::: API を介した拡張[](id:useAPI)
「ResizeDisk」 API を使用して、指定したクラウドディスクを拡張できます。 詳細については、[ResizeDisk](https://intl.cloud.tencent.com/document/product/362/16310)をご参照ください。

:::
</dx-tabs>



## システムディスクの拡張[](id:useCVMconsole)
1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインし、ターゲットCVMの右側にある**さらに**>**リソース調整**>**CBSを拡張**をクリックします。
2. 「CBSを拡張」画面が表示されます。この画面で拡張するデータディスクを選択し、**次へ**をクリックします。
3. 目標容量（現在の容量以上である必要があります）を設定し、**次へ**をクリックします。
4. 次の拡張方法で拡張操作を完了します。
<dx-tabs>
::: CVMコンソールを介した拡張
<dx-alert infotype="explain" title="">
CVMは、インスタンスをシャットダウンせずにクラウドシステムディスクの拡張をサポートします。
</dx-alert>
 1. **パーティションとファイルシステムの拡張**タブで注意事項を読み、**変更を開始**をクリックします。下図に示すように：
 <img style="width:600px; max-width: inherit;" src="https://staticintl.cloudcachetci.com/yehe/backend-news/rcu7553_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230421164941.png" />
 2. コンソールで容量拡張を完了し、インスタンスにログインしてファイルシステムが自動的に拡張されたかどうかを確認してください。そうでない場合は、[オンラインでのシステムディスクとファイルシステムの拡張](https://intl.cloud.tencent.com/document/product/362/50063) の説明に従ってパーティションとファイルシステムを拡張します。
:::
::: CBSコンソールを介した拡張[](id:useCBSConsole)
1. [CBSコンソール](https://console.cloud.tencent.com/cvm/cbs)にログインします。
2. ターゲットCBSの右側にある**さらに**>**スケールアウト**をクリックします。
3. 必要な新しい容量を選択します（現在の容量以上である必要があります。）。
4. お支払いをしてください。
5. ターゲットCVMのOSに応じて、[パーティションとファイルシステム（Windows）を拡張する](https://intl.cloud.tencent.com/document/product/362/6737)、または[パーティションとファイルシステム（Linux）を拡張する](https://intl.cloud.tencent.com/document/product/362/6738)必要があり、拡張された容量を既存のパーティションに割り当てるか、独立した新しいパーティションにフォーマットします。
:::
:::  APIを介した拡張[](id:useAPI)
ResizeInstanceDisksインターフェースを使用して、指定した非エラスティックディスクを拡張できます。詳細については[ResizeInstanceDisks](https://intl.cloud.tencent.com/document/product/362/16310)をご参照ください。

:::
</dx-tabs>


## 関連する操作
### データディスクの区分[](id:distinguish)
CVM OSに応じてクラウドディスクを確認します。
<dx-tabs>
::: Linux
1. [Linuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5436)します。
2. 次のコマンドを実行して、クラウドディスクとデバイス名の間の対応関係を確認します。
```
ls -l /dev/disk/by-id
```
次の情報が表示されます：
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)
そのうち、`disk-xxxx`はクラウドディスクの IDで、 [CBSコンソール](https://console.cloud.tencent.com/cvm/cbs) に進み確認できます。
:::
::: Windows
1. [Windowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5435)します。
2. <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-6px 0px">を右クリックして、**実行**を選択します。
3. 「実行」ウィンドウで`cmd`と入力して**Enter**を押します。
4. 次のコマンドを実行して、クラウドディスクとデバイス名の間の対応関係を確認します。
```
wmic diskdrive get caption,deviceid,serialnumber
```
または、次のコマンドを実行します。

```
wmic path win32_physicalmedia get SerialNumber,Tag
```
次の情報が表示されます：
![](https://main.qcloudimg.com/raw/e91aa2f938ddda304844d7ac28840859.png)
そのうち、`disk-xxxx`はクラウドディスクの IDで、 [CBSコンソール](https://console.cloud.tencent.com/cvm/cbs) に進み確認できます。
:::
</dx-tabs>

### Cloudinit 構成の確認
CVM OSに応じてクラウドディスクを確認します。
<dx-tabs>
::: Linux インスタンスのCloudinit 構成の確認[](id:confirmLinuxConfig)
ディスク拡張後、[Linuxインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5436)して、`/etc/cloud/cloud.cfg`にgrowpartおよびresizefsの設定項目が含まれているかどうか確認します。
 - 「はい」の場合、その他の操作の必要はありません。下図に示すように：
![](https://main.qcloudimg.com/raw/03d38f34651d317176c50f1ed3a03f30.png)
    - **growpart**：パーティションをディスクサイズまで拡張します。
    - **resizefs**：`/`パーティション内のファイルシステムをパーティションサイズに拡張または調整します。
- 「いいえ」の場合、ターゲットCVMのOSに応じて、手動でファイルシステムとパーティションを拡張する必要があります。[パーティションとファイルシステムの拡張 (Linux)](https://intl.cloud.tencent.com/document/product/362/31602)を実行する必要があり、拡張された容量を既存のパーティションに割り当てるか、独立した新しいパーティションにフォーマットします。
:::
::: Windows インスタンスのCloudinit 構成の確認[](id:confirmwindowsConfig)
ディスク拡張後、 [Windowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/5435) して、 `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf\cloudbase-init.conf`のpluginにExtendVolumesPlugin設定項目が含まれているかどうか確認してください。
 - 「はい」の場合は、マシンを再起動してください。 `cloudbase-init`はボリュームを自動的に拡張し、C パーティションの後ろにある空き領域をCパーティションに追加します。Cパーティション と空き領域の間に他のパーティションがあってはいけないことに注意してください。マシンを再起動したくない場合、Cパーティションと空き領域の間に他のパーティションがある場合、または「cloudbase-init」がサードパーティのセキュリティ ソフトウェアによってブロックされている場合は、次の powershell コマンドを手動で実行する必要があります。
 ```plantext
$DiskOps="@
select disk 0
select volume c
extend
exit
@"
$DiskOps | diskpart.exe | Out-Null
 ```
 - 「いいえ」の場合、ターゲットCVMのOSに応じて、手動でファイルシステムとパーティションを拡張する必要があります。[パーティションとファイルシステムの拡張 (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)を実行する必要があり、拡張された容量を既存のパーティションに割り当てるか、独立した新しいパーティションにフォーマットします。
:::
</dx-tabs>