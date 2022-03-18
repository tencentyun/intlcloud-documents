このドキュメントでは、Mac が Microsoft Remote Desktop経由でWindows CVMにログインする時に発生する可能性のある一般的な故障現象及び対処方法について説明します。
## 故障について

- Mac が Microsoft Remote Desktop 経由でWindows CVMにログインする時に、「The certificate couldn't be verified back to a root certificate.」というプロンプトが表示されます。
<img src="https://main.qcloudimg.com/raw/070b9c862d6928988768b266461bc816.png" data-nonescope="true" />
- Mac でリモートデスクトップ接続（Remote Desktop Connection）を使用すると、 「接続先のコンピューターのIDを確認できません」というプロンプトが表示されます。

## トラブルシューティング
>? 下記操作は Windows Server 2016 を例として説明します。
>

###  VNC を使用してCVMにログインする

1. [CVMコンソール](https://console.cloud.tencent.com/cvm/index)にログインします。
2. インスタンス管理ページで、対象CVMインスタンスを見つけて、【ログイン】をクリックします。次の図に示すように：
![ログイン](https://main.qcloudimg.com/raw/d9ccf04da21f4ac86d624742c87d5628.png)
3. ポップアップした 「Windowsインスタンスにログインする」ウィンドウで、【その他の方式(VNC）】を選択し、【今すぐログイン】をクリックして、CVMにログインします。
4.ポップアップウィンドウで、左上隅にある「リモートコマンドの送信」を選択し、 **Ctrl-Alt-Delete**  をクリックして、システムログインインターフェースに入ります。次の図に示すように：
![](https://main.qcloudimg.com/raw/5064251ea86085326e86884a1c13ef6b.png)

### インスタンスのローカルグループポリシーの変更

1. OSインターフェースで、 <img src="https://main.qcloudimg.com/raw/330624bafb194914948c8ebd9e47334d.png" style="margin: 0;">をクリックして、 **gpedit.msc**を入力し、**Enter**キーを押して、「ローカルグループポリシーエディター」を開きます。
>?  「Win+R」ショートカットを使用して実行インターフェースを開くこともできます。
>
2. 左側のナビゲーションツリーで、【コンピューターの構成】>【管理用テンプレート】>【Windowsコンポーネント】>【リモートデスクトップサービス】>【リモートデスクトップ セッションホスト】>【セキュリティ】を選択し、【 リモート (RDP) 接続に特定のセキュリティ レイヤーの使用を必要とする】をダブルクリックします。

3. 開いた 「リモート (RDP) 接続に特定のセキュリティ レイヤーの使用を必要とする」ウインドウで、【有効】を選択し、かつ【セキュリティレイヤー】を【RDP】に設定します。

4. 【OK】をクリックし、設定を完了します。
5.インスタンスを再起動して、接続が成功したかどうかを再試行します。接続が失敗した場合に、 [チケットを送信](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=7&source=0&data_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8CVM&level3_id=142&radio_title=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%99%BB%E5%BD%95%E4%B8%8D%E4%B8%8A&queue=15&scene_code=12686&step=2) してフィードバックしてください。
