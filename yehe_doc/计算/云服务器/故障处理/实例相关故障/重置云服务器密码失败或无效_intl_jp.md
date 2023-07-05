このドキュメントでは、Windows Server 2012 OSを例に、CVMのパスワードのリセットが失敗する、または有効にならない場合の確認方法と対処方法を紹介します。

## 障害の現象

-CVMのパスワードをリセットした後、「システムがビジー状態です。インスタンスパスワードをリセットできませんでした（7617d94c）」というメッセージが表示されます。
- CVMのパスワードをリセットした後、新しいパスワードは有効にならず、ログインパスワードは古いパスワードのままです。


## 考えられる原因
CVMパスワードのリセットが失敗する、または有効にならないのは、次の原因が考えられます。
- CVMのCloudbase-Initコンポーネントが破損、変更、無効化されているか、起動されていません。
- CVMにインストールされているセキュリティソフトウェア（360ウイルス対策ソフトウェアなど）により、関連システムプロセスのコンポーネントがブロックされました。


## トラブルシューティング

パスワードリセットの失敗の考えられる原因に従って、次の2つの確認方法が提供されています。

### Cloudbase-Initサービスを確認する

- [VNCを使用してWindowsインスタンスにログイン](https://intl.cloud.tencent.com/document/product/213/32496)します。
2. OS画面で<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>を右クリックして、【実行】を選択して、【ファイル名を指定して実行】ダイアログボックスで、services.mscと入力し、Enterキーを押して「サービス」ウィンドウを開きます。
3. 下の図に示すように、cloudbase-initサービスが存在しているかを確認します。
![](https://main.qcloudimg.com/raw/2615f5c0e68a31174c16c9a80884455c.png)
 - 存在する場合は、次のステップを実行します。
 - 存在しない場合は、cloudbase-initサービスを再インストールします。操作手順の詳細については、[Windows OSでCloudbase-Initをインストール](https://intl.cloud.tencent.com/document/product/213/32364)をご参照ください。
4. 下の図に示すように、cloudbase-init のプロパティをダブルクリックして開きます。
![](https://main.qcloudimg.com/raw/10702cb2e359d6de36aec4960771c841.png)
5. 【全般】タブで、cloudbase-initの起動タイプが【自動】に設定されているかどうか確認します。
 - 自動に設定されている場合、次のステップに進みます。
 - そうでない場合、cloudbase-initの起動タイプを【自動】に設定します。
6. 【ログイン】タブに切り替え、cloudbase-initのログインアカウントが【ローカルシステムアカウント】に選択されているかどうかを確認します。
 - そうである場合、次のステップを実行します。
 - そうでない場合、cloudbase-initのログインアカウントを【ローカルシステムアカウント】に設定します。
7. 【全般】タブに切り替えて、サービスステータスの【起動】をクリックし、cloudbase-initサービスを手動で起動して、エラーが表示されるかどうかを確認します。
 - エラーが表示される場合、[CVMにインストールされているセキュリティソフトウェアを確認する](#CheckSecuritySoftware)。
 - エラーが表示されない場合、次のステップに進みます。
8. OS画面で <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>を右クリックして、【実行】を選択して、【実行】ダイアログボックスで、**regedit**を入力して、**Enter**キーを押して「レジストリエディター」画面を開きます。
9. 左側のレジストリナビゲーションで、【HKEY_LOCAL_MACHINE】>【SOFTWARE】>【Cloudbase Solutions】>【Cloudbase-Init】ディレクトリの順に展開します。
10. 「LocalScriptsPlugin」レジストリをすべて見つけ、LocalScriptsPluginの値が2になっているかどうかを確認します。
![](https://main.qcloudimg.com/raw/75580b56e3a28fb9e0559372eb33ff11.png)
 - そうである場合、次のステップを実行します。
 - そうでない場合、LocalScriptsPluginの値を2に設定します。
11. OS画面で<img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin: 0;"></img>をクリックして、下の図のように、【このコンピュータ】を選択し、デバイスとドライブにCD-ドライブが読み込まれているかどうかを確認します。
![](https://main.qcloudimg.com/raw/8755719fb39bb5f841f4c32897545233.png)
 - そうである場合、[CVMにインストールされているセキュリティソフトウェアを確認する](#CheckSecuritySoftware)。
 - そうでない場合、デバイスマネージャでCD-ROMドライブを起動します。

<span id="CheckSecuritySoftware"></span>
### CVMにインストールされているセキュリティソフトウェアを確認する

インストールされているセキュリティソフトウェアプログラムを使用してCVMの脆弱性をスキャンし、また、Cloudbase-Initのコアコンポーネントがブロックされていないかを確認します。
- CVMの脆弱性が検出された場合は、修正してください。
- コアコンポーネントがブロックされていることが検出された場合は、ブロックをキャンセルしてください。

CVMパスワードのリセットが失敗する、または有効にならないことを回避するには、セキュリティソフトウェアのホワイトリストと信頼できるファイル領域に次のディレクトリとファイルを追加することをお勧めします。
- セキュリティソフトウェアのホワイトリストに次のディレクトリを追加してください。
```
C:\Windows\System32\WindowsPowerShell\
C:\Program Files\Cloudbase Solutions\Cloudbase-Init\Python\Scripts
C:\Program Files\QCloud
C:\Program Files\Cloudbase Solutions\
```
- 次のファイルを信頼できるファイル領域に追加してください。　　
```
C:\Windows\System32\cmd.exe
C:\Windows\SysWOW64\cmd.exe
```

