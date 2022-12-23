CSSの再生は、デフォルトではオリジナルのビットレートで出力されます。再生ビットレートを制限または設定する場合は、再生ドメイン名に対してトランスコーディングテンプレートとの関連付けを行う必要があります。ここでは、再生ドメイン名の下でテンプレートの関連付けとその解除の方法を説明します。

## 注意事項
- テンプレート設定の完了後、約5分 - 10分経ってから有効になります。
- トランスコードテンプレートを指定すると、バックエンドがビットレートに対応する各再生アドレスを生成し、ユーザーは選択して呼び出せるようになります。プッシュの初期解像度は、画面が引き伸ばされて変形するのを避けるため、できる限りオリジナルの比率に近づけます。
- H.265はH.264ほどの互換性がないため、プレーヤーがH.265コードをサポートしておらず、再生に失敗した場合は、 [トランスコードテンプレート](https://intl.cloud.tencent.com/document/product/267/31071) を設定し、H.264コードにトランスコードして再生することができます。
- 新しいビットレートのアドレスに初めてアクセスする時は、接続をトリガーした1人目のアクセスユーザーはローディング時間が幾分長いと感じるかもしれませんが、これは正常です。
- 1つのドメイン名を複数のトランスコードテンプレートに関連付けでき、その後、再生ビットレートは、設定した該当のトランスコードテンプレートに基づきトランスコーディングを行います。
- トランスコードテンプレートの設定数量の上限は**50個**です。

##  前提条件
-  [CSSコンソール](https://console.cloud.tencent.com/live)にログインし、 [再生ドメイン名](https://intl.cloud.tencent.com/document/product/267/35970)の追加が完了していること。
- [トランスコードテンプレートを作成](https://intl.cloud.tencent.com/document/product/267/31071)または[アダプティブ・ビットレートテンプレート](www.tencentcloud.com/document/product/267/50271)を作成していること。

## トランスコードテンプレート
[](id:conect)
### トランスコードテンプレートの関連付け
1. [**ドメイン名管理**](https://console.cloud.tencent.com/live/domainmanage)に入り、設定したい**再生ドメイン名**または右側の**管理**をクリックしてドメイン名詳細画面に入ります。
2. **テンプレート設定**タグを選択し、**トランスコーディング設定**タグの右上側の**編集**をクリックします。
3. 個々のトランスコーディング設定テンプレートを選択し、当該ドメイン名での再生アドレスのために、テンプレート設定のエンコード方式とビットレートを指定します。
4. **OK**をクリックすれば完了です。

![](https://qcloudimg.tencent-cloud.cn/raw/2d8cb5be76debfbd04d60329891c5830.png)

[](id:descript)
### トランスコーディング再生アドレスの説明
トランスコードテンプレート設定後、再生URLにトランスコードテンプレート名を追加する必要があり、接合方式は、**再生アドレス_トランスコードテンプレート名**です。トランスコードテンプレート名を接合しないと、再生されるのは初期のライブストリーミングのコンテンツになります。再生アドレス関連のより詳細な内容については、 [再生設定](https://intl.cloud.tencent.com/document/product/267/31058)をご参照ください。

**例：**再生ドメイン名に関連付けたトランスコードテンプレート名は **hd**、初期再生アドレスは次のとおりとします：
<pre style="color:white">
http://domain/AppName/StreamName.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
トランスコーディング後のビデオを取得して再生したい場合は、次のように新しい再生アドレスを改めて作成してください：
<pre style="color:white">
http://domain/AppName/<b style="color:yellow;">StreamName_hd</b>.flv?txSecret=Md5(key+<b style="color:yellow;">StreamName_hd</b>+hex(time))&txTime=hex(time)
</pre>
[](id:Untie)

### トランスコードテンプレートのバインド解除
1. **[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)**に入り、設定する再生ドメイン名または右側の**管理**をクリックして、ドメイン名詳細画面に進みます。
2. **テンプレート設定**タグを選択し、**トランスコーディング設定**を選択します。
3. 右側の**編集**をクリックし、対応するテンプレートのチェックを外します。
4. **OK**をクリックし、テンプレートとドメイン名の関連付けを解除します。
![](https://qcloudimg.tencent-cloud.cn/raw/ff6e5f8038124c95fb29d0ffb5745890.png)

>? テンプレートを削除する場合は、テンプレートとの関連付けを解除した後、**機能設定**>[**CSSトランスコード**](https://console.cloud.tencent.com/live/config/transcode)に入り、削除を実行してください。詳しくは、[テンプレート削除](https://intl.cloud.tencent.com/document/product/267/31071#delect)をご参照ください。


## アダプティブ・ビットレートテンプレート
### アダプティブ・ビットレートテンプレートとの関連付け

1. [**ドメイン名管理**](https://console.cloud.tencent.com/live/domainmanage)に入り、設定したい**再生ドメイン名**または右側の**管理**をクリックしてドメイン名詳細画面に入ります。
2. **テンプレート設定**タグを選択し、**アダプティブ・ビットレート設定**タグの右上側の**編集**をクリックします。
3. アダプティブ・ビットレート設定テンプレートを選択し、当該ドメイン名配下の再生アドレスに対して、アダプティブ・ビットレートテンプレートに設定するサブストリームの情報を指定します。
4. **OK**をクリックすれば完了です。
![](https://qcloudimg.tencent-cloud.cn/raw/df2db1fd5b8f9beb5eda4eb989557c51.png)

### アダプティブ・ビットレート再生アドレスの説明
アダプティブ・ビットレートテンプレートを設定した後、アダプティブ・ビットレートはHLSプロトコルとWebRTCプロトコルのみをサポートし、これらの2プロトコルのアダプティブ・ビットレートアドレスの接合方法は異なります。詳しくは、 [再生設定](https://intl.cloud.tencent.com/document/product/267/31058)をご参照ください。
**HLSアダプティブ・ビットレートアドレスの接合方法：**
**例：**再生ドメイン名に関連付けられたトランスコードテンプレートの名前を**autobitrate**とすれば、オリジナル再生アドレスは次のようになります：

<pre style="color:white">
http://domain/AppName/StreamName.m3u8?txSecret=Md5(key+<b style="color:yellow;">StreamName</b>+hex(time))&txTime=hex(time) 
</pre>
トランスコーディング後のビデオを取得して再生したい場合は、次のように新しい再生アドレスを改めて作成してください：
<pre style="color:white">
http://domain/AppName/<b style="color:yellow;">StreamName_autobitrate</b>.m3u8?txSecret=Md5(key+<b style="color:yellow;">StreamName_autobitrate</b>+hex(time))&txTime=hex(time)
</pre>
**WebRTCアダプティブ・ビットレートアドレスの接合方法：**
**例：**アダプティブ・ビットレートテンプレートに次のサブテンプレートがあるとします。サブテンプレート1は名前がtest1で、ビットレートが200です。サブテンプレート2は名前がtest2で、ビットレートが300です。サブテンプレート3は名前がtest3で、ビットレートが400です。
つまり、WebRTCアダプティブ・ビットレートアドレスは以下のとおりになります：
<pre style="color:white">
webrtc://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)&tabr_bitrates=test3,test2,test1&tabr_start_bitrate=test1&tabr_control=auto。
</pre>

### アダプティブ・ビットレートテンプレートとの関連付けの解除
1. **[ドメイン名管理](https://console.cloud.tencent.com/live/domainmanage)**に入り、設定する再生ドメイン名または右側の**管理**をクリックして、ドメイン名詳細画面に進みます。
2. **テンプレート設定**タグを選択し、**アダプティブ・ビットレート設定**を選択します。
3. 右側の**編集**をクリックし、対応するテンプレートのチェックを外します。
4. **OK**をクリックし、テンプレートとドメイン名の関連付けを解除します。
![](https://qcloudimg.tencent-cloud.cn/raw/872b71589554e8d89abf50db40f75777.png)

>? テンプレートを削除する場合は、テンプレートとの関連付けを解除した後、**機能テンプレート**>[**トランスコーディング設定**](https://console.cloud.tencent.com/live/config/transcode)に入り、削除を実施しててください。詳しくは、[テンプレート削除](https://intl.cloud.tencent.com/document/product/267/31071#delect)をご参照ください。
