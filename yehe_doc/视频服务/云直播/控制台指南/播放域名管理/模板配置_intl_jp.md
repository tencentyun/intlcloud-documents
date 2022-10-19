CSSの再生は、デフォルトではオリジナルのビットレートで出力されます。再生ビットレートを制限または設定する場合は、再生ドメイン名に対してトランスコーディングテンプレートとの関連付けを行う必要があります。ここでは、再生ドメイン名及びトランスコーディングテンプレートの関連付けとその解除の方法を説明します。

## 注意事項
- テンプレートの設定は完了して約5分 ～ 10分後に反映されます。
- トランスコーディングテンプレートを指定すると、バックグラウンドで各ビットレートに対応する再生アドレスが生成されます。ユーザーは再生アドレスを選択して呼び出せるようになります。画面が引き伸ばされて変形するのを避けるため、プッシュの初期解像度は、できる限りオリジナルのアスペクト比に近づけます。
- H.265はH.264ほどの互換性がないため、プレーヤーがH.265エンコードをサポートせず、再生に失敗した場合は、 [トランスコーディングテンプレート](https://intl.cloud.tencent.com/document/product/267/31071) を設定し、H.264エンコードにトランスコーディングして再生してください。
- 新しいビットレートのアドレスに初めてアクセスする時は、最初にそのリンクにアクセスしたユーザーは読込みに時間がかかると感じてしまうかもしれませんが、特に問題ありません。
- 1つのドメイン名を複数のトランスコーディングテンプレートに関連を付けることができます。関連を付けると、再生ビットレートは、設定したトランスコーディングテンプレートに基づきトランスコーディングを行います。
- トランスコーディングテンプレートは最大**50個**まで設定できます。



##  前提条件
-  [CSSコンソール](https://console.cloud.tencent.com/live)にログインし、 [再生ドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)を追加していること。
- [トランスコーディングテンプレートを作成](https://intl.cloud.tencent.com/document/product/267/31071)または[アダプティブ・ビットレートテンプレート](https://cloud.tencent.com/document/product/267/78369)を作成していること。

[](id:conect)
## トランスコーディングテンプレートとの関連付け
1. [**ドメイン名管理**](https://console.cloud.tencent.com/live/domainmanage)に入り、設定する**再生ドメイン名**または右側の**管理**をクリックして、ドメイン名詳細画面に進みます。
2. **テンプレート設定**タグを選択し、**トランスコーディング設定**タグの右上側の**編集**をクリックします。
3. トランスコーディング設定テンプレートを選択し、当該ドメイン名配下の再生アドレスに対して、テンプレートに設定するエンコード方法とビットレートを指定します。
4. **保存**をクリックして設定を完了します。

![](https://qcloudimg.tencent-cloud.cn/raw/2d8cb5be76debfbd04d60329891c5830.png)

[](id:descript)
## トランスコーディング再生アドレスの説明
トランスコーディングテンプレート設定後、再生URLにトランスコーディングテンプレート名を追加する必要があります。接続方法は、**再生アドレス_トランスコーディングテンプレート名**です。トランスコーディングテンプレート名を接続しなかった場合、オリジナルライブストリーミングのコンテンツを再生します。再生アドレスの詳細については、 [再生設定](https://intl.cloud.tencent.com/document/product/267/31058)をご参照ください。

**例：**再生ドメイン名に関連付けられたトランスコーディングテンプレートの名前を**hd**とすれば、オリジナル再生アドレスが次になります：
<pre>
http://domain/AppName/StreamName.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
トランスコーディングしたビデオを取得して再生するには、新しい再生アドレスを生成する必要があります。具体的には、以下のとおりになります：
<pre>
http://domain/AppName/<b style="color:yellow;">StreamName_hd</b>.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName_hd</b>+hex(time))&txTime=hex(time)
</pre>
[](id:Untie)

## トランスコーディングテンプレートとの関連付けの解除
1. **[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)**に入り、設定する再生ドメイン名または右側の**管理**をクリックして、ドメイン名詳細画面に進みます。
2. **テンプレート設定**タグを選択し、**トランスコーディング設定**を選択します。
3. 右側の**編集**をクリックし、対応するテンプレートのチェックを外します。
4. **保存**をクリックし、テンプレートとドメイン名の関連付けを解除します。
![](https://qcloudimg.tencent-cloud.cn/raw/ff6e5f8038124c95fb29d0ffb5745890.png)

>? テンプレートを削除する場合は、テンプレートとの関連付けを解除した後、**機能テンプレート**>[**トランスコーディング設定**](https://console.cloud.tencent.com/live/config/transcode)に入り、削除を実施しててください。詳しくは、[テンプレート削除](https://intl.cloud.tencent.com/document/product/267/31071#delect)をご参照ください。


## アダプティブ・ビットレートテンプレートとの関連付け

1. [**ドメイン名管理**](https://console.cloud.tencent.com/live/domainmanage)に入り、設定したい**再生ドメイン名**または右側の**管理**をクリックしてドメイン名詳細画面に入ります。
2. **テンプレート設定**タグを選択し、**アダプティブ・ビットレート設定**タグの右上側の**編集**をクリックします。
3. アダプティブ・ビットレート設定テンプレートを選択し、当該ドメイン名配下の再生アドレスに対して、アダプティブ・ビットレートテンプレートに設定するサブストリームの情報を指定します。
4. **保存**をクリックして設定を完了します。
![](https://qcloudimg.tencent-cloud.cn/raw/df2db1fd5b8f9beb5eda4eb989557c51.png)

## アダプティブ・ビットレート再生アドレスの説明
アダプティブ・ビットレートテンプレートを設定した後、アダプティブ・ビットレートはHLSプロトコルとWebRTCプロトコルをサポートするようになります。これらの2プロトコルのアダプティブ・ビットレートアドレスの接続方法は異なります。詳しくは、 [再生設定](https://intl.cloud.tencent.com/document/product/267/31058)をご参照ください。
**HLSアダプティブ・ビットレートアドレスの接合方法：**
**例：**再生ドメイン名に関連付けられたトランスコーディングテンプレートの名前を**autobitrate**とすれば、オリジナル再生アドレスが次になります：

<pre>
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
トランスコーディングしたビデオを取得して再生するには、新しい再生アドレスを生成する必要があります。具体的には、以下のとおりになります：
<pre>
http://domain/AppName/<b style="color:yellow;">StreamName_autobitrate</b>.m3u8?txSecret=Md5(key+<b style="color:yellow;">StreamName_autobitrate</b>+hex(time))&txTime=hex(time)
</pre>
**WebRTCアダプティブ・ビットレートアドレスの接続方法：**
**例：**アダプティブ・ビットレートテンプレートに次のサブテンプレートがあるとします。サブテンプレート1は名前がtest1で、ビットレートが200です。サブテンプレート2は名前がtest2で、ビットレートが300です。サブテンプレート3は名前がtest3で、ビットレートが400です。
では、WebRTCアダプティブ・ビットレートアドレスが以下になります：

webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)&tabr_bitrates=test3,test2,test1&tabr_start_bitrate=test1&tabr_control=auto。

## アダプティブ・ビットレートテンプレートとの関連付けの解除
1. **[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)**に入り、設定する再生ドメイン名または右側の**管理**をクリックして、ドメイン名詳細画面に進みます。
2. **テンプレート設定**タグを選択し、**アダプティブ・ビットレート設定**を選択します。
3. 右側の**編集**をクリックし、対応するテンプレートのチェックを外します。
4. **保存**をクリックし、テンプレートとドメイン名の関連付けを解除します。
![](https://qcloudimg.tencent-cloud.cn/raw/872b71589554e8d89abf50db40f75777.png)

>? テンプレートを削除する場合は、テンプレートとの関連付けを解除した後、**機能テンプレート**>[**トランスコーディング設定**](https://console.cloud.tencent.com/live/config/transcode)に入り、削除を実施しててください。詳しくは、[テンプレート削除](https://intl.cloud.tencent.com/document/product/267/31071#delect)をご参照ください。