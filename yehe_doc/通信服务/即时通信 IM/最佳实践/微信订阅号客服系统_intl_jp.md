ここでは、Node.jsを使用したシンプルで一般的なカスタマーサービスのシナリオのDemoの開発を例に、WeChatサブスクリプションアカウントをTencent Cloud IMに統合する基本的なプロセスについてご説明いたします。
>?例は参考用であり、正式なリリース前に、サーバーの負荷分散、インターフェースの同時制御、永続的な情報の保存などをさらに改善する必要があります。このドキュメントではその最適化操作についての説明はありませんので、開発者は実際の状況に応じて、ご自身で実装してください。

## シナリオのプロセスおよび効果図
このドキュメントのDemoのシナリオの基本的なプロセスは次のとおりです。
1. 顧客がアパレルネットショップのサブスクリプションアカウントから「子供服の新商品の販売開始はいつになりますか？」と問い合わせます。
2. 顧客の問い合わせメッセージはTencent Cloud IMシステムを介してアパレルネットショップのカスタマーサービスに送信されます。
3. カスタマーサービスの担当者が5月になりますので、フォローをよろしくお願いいたします！」と返信すると、このメッセージはTencent Cloud IMシステムとWeChatを介して顧客にプッシュされます。

顧客側の効果図は次のとおりです。
![](https://main.qcloudimg.com/raw/155fe5984115665314d9305c53b0a619.jpg)
カスタマーサービス側の効果図は次のとおりです。
![](https://main.qcloudimg.com/raw/f69848510053e9ee1ebf046854229fd6.png)
シナリオのフローチャートは次のとおりです。
![](https://main.qcloudimg.com/raw/086439320c042ba4f03322b825ec38d1.jpg)

## 注意事項
- メッセージ送信リンクが長いと、メッセージの送受信にかかる時間に影響することがあります。
- 個人登録のサブスクリプションアカウントは、利用者に対し、WeChat公式プラットフォームの【カスタマーサービスメッセージ】インターフェースを使用して自動的にメッセージをプッシュすることはできません。

## 前提条件

- Node.jsを実行できるパブリックネットワーク開発サーバーまたはCVMが準備されていること。
- WeChatサブスクリプションアカウントまたはサービスアカウントが[登録](https://mp.weixin.qq.com/cgi-bin/registermidpage?action=index&lang=zh_CN&token=) されていること。
- 詳細については、 [WeChat公式プラットフォーム開発ドキュメント](https://developers.weixin.qq.com/doc/offiaccount/Basic_Information/Access_Overview.html)をご参照ください。
-  [IMアプリケーションの作成](https://intl.cloud.tencent.com/document/product/1047/34577)が完了していること。
- 事前に、 user0およびuser1などのIMユーザーアカウントが [個別インポート](https://intl.cloud.tencent.com/document/product/1047/34953) または [一括インポート](https://intl.cloud.tencent.com/document/product/1047/34954) されていること。

## 参考ドキュメント

- [APIドキュメント](https://intl.cloud.tencent.com/document/product/1047/34620)
- [サードパーティのコールバック](https://intl.cloud.tencent.com/document/product/1047/34354)
- [WeChatパブリックプラットフォーム開発ガイドライン](https://developers.weixin.qq.com/doc/offiaccount/Getting_Started/Overview.html)
- [Expressフレームワークチュートリアル](https://expressjs.com/zh-cn/)

## 操作手順

### 手順1：開発プロジェクトの作成と依存のインストール

```javascript
npm init -y

// expressフレームワーク
npm i express@latest --save 

// 暗号化モジュール
npm i crypto@latest --save

// xmlパーサー解析ツール
npm i xml2js@latest --save

// httpリクエストの開始
npm i axios@latest --save

// userSigの計算
npm i tls-sig-api-v2@latest --save
```

### 手順2：IMアプリケーション情報の入力とUserSigの計算

<pre><code><span class="hljs-comment">// ------------ IM ------------</span>
<span class="hljs-keyword">const</span> IMAxios = axios.create({
  <span class="hljs-attr">timeout</span>: <span class="hljs-number">10000</span>,
  <span class="hljs-attr">headers</span>: {
    <span class="hljs-string">'Content-Type'</span>: <span class="hljs-string">'application/x-www-form-urlencoded;charset=UTF-8'</span>,
  },
});

<span class="hljs-comment">// IMアカウントシステムにインポートされたユーザーIDマッピングテーブルは、永続的に保存されず、Demoを迅速に検索するためにのみ使用されます。プロダクション環境では、別の技術ソリューションをご使用ください</span>
<span class="hljs-keyword">const</span> importedAccountMap = <span class="hljs-keyword">new</span> <span class="hljs-built_in">Map</span>();
<span class="hljs-comment">// IMアプリケーションおよびApp管理者情報は、<a href="https://console.cloud.tencent.com/im">IMコンソール</a> にログインして取得してください</span>
<span class="hljs-keyword">const</span> SDKAppID = <span class="hljs-number">0</span>; <span class="hljs-comment">// IMアプリケーションのSDKAppIDを入力します</span>
<span class="hljs-keyword">const</span> secrectKey = <span class="hljs-string">''</span>; <span class="hljs-comment">// IMアプリケーションの暗号キーを入力します</span>
<span class="hljs-keyword">const</span> AppAdmin = <span class="hljs-string">'user0'</span>; <span class="hljs-comment">// user0をApp管理者アカウントに設定します</span>
<span class="hljs-keyword">const</span> kfAccount1 = <span class="hljs-string">'user1'</span>; <span class="hljs-comment">// user1をカスタマーサービスアカウントに設定します</span>
<span class="hljs-comment">// REST APIを呼び出す時に使用するUserSigを計算します。詳細については <a href="https://github.com/tencentyun/tls-sig-api-v2-node">Github</a>をご参照ください</span>
<span class="hljs-keyword">const</span> api = <span class="hljs-keyword">new</span> TLSSigAPIv2.Api(SDKAppID, secrectKey);
<span class="hljs-keyword">const</span> userSig = api.genSig(AppAdmin, <span class="hljs-number">86400</span>*<span class="hljs-number">180</span>);
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">'userSig:'</span>, userSig);</code></pre>

### 手順3： URLとTokenの設定
>?このドキュメントはWeChatパブリックプラットフォーム開発ガイドラインを直接参照して作成されています。変更がある場合は、 [アクセスガイド](https://mp.weixin.qq.com/wiki) を基準としてください。

1. サブスクリプションアカウント管理バックエンドにログインします。
2. 【基本設定】を選択し、プロトコルをチェックし、開発者になります。
3. 【設定を変更】をクリックし、関連情報を入力します。
 - URL：サーバーアドレス、WeChatメッセージとイベントを受信するためのインターフェース URL、入力必須パラメータ。
 - Token：任意に入力し、署名を作成するために使用します。このTokenは、安全性を検証するために、インターフェースURLに含まれるTokenと比較されます。必須パラメータ。
 - EncodingAESKey：手動で入力するか、またはランダムに生成され、メッセージボディの暗号化および復号化キーに使用されます。オプションパラメータ。

### 手順4：Webサービス監視ポートを有効にし、WeChatから送信されたToken検証に正確に応答

<pre><code><span class="hljs-keyword">const</span> express = <span class="hljs-keyword">require</span>(<span class="hljs-string">'express'</span>); <span class="hljs-comment">// expressフレームワーク </span>
<span class="hljs-keyword">const</span> crypto =  <span class="hljs-keyword">require</span>(<span class="hljs-string">'crypto'</span>); <span class="hljs-comment">// 暗号化モジュール</span>
<span class="hljs-keyword">const</span> util = <span class="hljs-keyword">require</span>(<span class="hljs-string">'util'</span>);
<span class="hljs-keyword">const</span> xml2js = <span class="hljs-keyword">require</span>(<span class="hljs-string">'xml2js'</span>); <span class="hljs-comment">// xmlパーサー</span>
<span class="hljs-keyword">const</span> axios = <span class="hljs-keyword">require</span>(<span class="hljs-string">'axios'</span>); <span class="hljs-comment">//  httpリクエストの起動</span>
<span class="hljs-keyword">const</span> TLSSigAPIv2 = <span class="hljs-keyword">require</span>(<span class="hljs-string">'tls-sig-api-v2'</span>); <span class="hljs-comment">// userSigの計算</span>

<span class="hljs-comment">// ------------ Webサービス ------------</span>
<span class="hljs-keyword">var</span> app = express();
<span class="hljs-comment">// Token は【サブスクリプションアカウント管理バックエンド】&gt;【基本設定】で設定する必要があります</span>

<span class="hljs-comment">// 80ポートに入るすべてのgetリクエスト</span>を処理します
app.get(<span class="hljs-string">'/'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span><span class="hljs-params">(req, res)</span> </span>{
  <span class="hljs-comment">// ------------ WeChatパブリックプラットフォームにアクセス ------------</span>
  <span class="hljs-comment">// 詳細については <a href="https://developers.weixin.qq.com/doc/offiaccount/Getting_Started/Overview.html">WeChat公式ドキュメント</a> </span>をご参照ください
  <span class="hljs-comment">// WeChatサーバーのGetリクエストからパラメータsignature、timestamp、nonce、echostr</span>を取得します
  <span class="hljs-keyword">var</span> signature = req.query.signature; <span class="hljs-comment">// WeChat暗号化署名</span>
  <span class="hljs-keyword">var</span> timestamp = req.query.timestamp; <span class="hljs-comment">// タイムスタンプ</span>
  <span class="hljs-keyword">var</span> nonce = req.query.nonce; <span class="hljs-comment">// 乱数</span>
  <span class="hljs-keyword">var</span> echostr = req.query.echostr; <span class="hljs-comment">// ランダムな文字列</span>

  <span class="hljs-comment">// token、timestamp、nonceという3つのパラメータを辞書式順序に配列します</span>
  <span class="hljs-keyword">var</span> <span class="hljs-keyword">array</span> = [myToken, timestamp, nonce];
  <span class="hljs-keyword">array</span>.sort();

  <span class="hljs-comment">// 3つのパラメータの文字列を1つの文字列に結合して、 sha1暗号化します</span>
  <span class="hljs-keyword">var</span> tempStr = <span class="hljs-keyword">array</span>.join(<span class="hljs-string">''</span>);
  <span class="hljs-keyword">const</span> hashCode = crypto.createHash(<span class="hljs-string">'sha1'</span>); <span class="hljs-comment">// 暗号化タイプを作成します </span>
  <span class="hljs-keyword">var</span> resultCode = hashCode.update(tempStr,<span class="hljs-string">'utf8'</span>).digest(<span class="hljs-string">'hex'</span>); <span class="hljs-comment">// 渡された文字列を暗号化します</span>

  <span class="hljs-comment">// 開発者は、暗号化後の文字列を取得した後signatureと比較し、このリクエストのソース元がWeChatであることを識別します</span>
  <span class="hljs-keyword">if</span> (resultCode === signature) {
    res.send(echostr);
  } <span class="hljs-keyword">else</span> {
    res.send(<span class="hljs-string">'404 not found'</span>);
  }
});

<span class="hljs-comment">// 80ポートを監視</span>
app.listen(<span class="hljs-number">80</span>);</code></pre>

### 手順5：開発者のサーバー側サービスロジックの実装

- WeChatからプッシュされたフォローイベントを受信したら、 [単一アカウントのインポート](https://intl.cloud.tencent.com/document/product/1047/34953) または [複数アカウントのインポート](https://intl.cloud.tencent.com/document/product/1047/34954) API を呼び出し、アカウントシステムにアカウントをインポートします。
- WeChatからプッシュされたフォローイベントを受信したら、メッセージを受動的に返信します。
- WeChatからプッシュされたフォローキャンセルイベントを受信したら [アカウント削除](https://intl.cloud.tencent.com/document/product/1047/34955) APIを呼び出し、このアカウントをアカウントシステムから削除します。
- WeChatからプッシュされた一般的なメッセージを受信したら、 [シングルチャットメッセージ](https://intl.cloud.tencent.com/document/product/1047/34919) APIを呼び出し、カスタマーサービスアカウントにシングルチャットメッセージを送信します。

```javascript
const genRandom = function() {
  return  Math.floor(Math.random() * 10000000);
}

// wxテキストに返信するxmlを生成します
const genWxTextReplyXML = function(to, from, content) {
  let xmlContent = '<xml><ToUserName><![CDATA[' + to + ']]></ToUserName>'
  xmlContent += '<FromUserName><![CDATA[' + from + ']]></FromUserName>'
  xmlContent += '<CreateTime>' + new Date().getTime() + '</CreateTime>'
  xmlContent += '<MsgType><![CDATA[text]]></MsgType>'
  xmlContent += '<Content><![CDATA[' + content + ']]></Content></xml>';

  return xmlContent;
}

/**
 * IMアカウントシステムにユーザーをインポートします
 * @param {String} userID インポートしたいユーザーID
 */
const importAccount = function(userID) {
  console.log('importAccount:', userID);
  return new Promise(function(resolve, reject) {
    var url = util.format('https://console.tim.qq.com/v4/im_open_login_svc/account_import?sdkappid=%s&identifier=%s&usersig=%s&random=%s&contenttype=json',
      SDKAppID, AppAdmin, userSig, genRandom());
    console.log('importAccount url:', url);
    IMAxios({
      url: url,
      data: {
        "Identifier": userID
      },
      method: 'POST'
    }).then((res) => {
      if (res.data.ErrorCode === 0) {
        console.log('importAccount ok.', res.data);
        resolve();
      } else {
        reject(res.data);
      }
    }).catch((error) => {
      console.log('importAccount failed.', error);
      reject(error);
    })
  });
}

/**
 * IMアカウントシステムからユーザーを削除します
 * @param {String} userID 削除したいユーザーID
 */
const deleteAccount = function(userID) {
  console.log('deleteAccount', userID);
  return new Promise(function(resolve, reject) {
    var url = util.format('https://console.tim.qq.com/v4/im_open_login_svc/account_delete?sdkappid=%s&identifier=%s&usersig=%s&random=%s&contenttype=json',
      SDKAppID, AppAdmin, userSig, genRandom());
    console.log('deleteAccount url:', url);
    IMAxios({
      url: url,
      data: {
        "DeleteItem": [
          {
            "UserID": userID,
          },
        ]
      },
      method: 'POST'
    }).then((res) => {
      if (res.data.ErrorCode === 0) {
        console.log('deleteAccount ok.', res.data);
        resolve();
      } else {
        reject(res.data);
      }
    }).catch((error) => {
      console.log('deleteAccount failed.', error);
      reject(error);
    })
  });
}

/**
 * シングルチャットメッセージ
 */
const sendC2CTextMessage = function(userID, content) {
  console.log('sendC2CTextMessage:', userID, content);
  return new Promise(function(resolve, reject) {
    var url = util.format('https://console.tim.qq.com/v4/openim/sendmsg?sdkappid=%s&identifier=%s&usersig=%s&random=%s&contenttype=json',
      SDKAppID, AppAdmin, userSig, genRandom());
    console.log('sendC2CTextMessage url:', url);
    IMAxios({
      url: url,
      data: {
        "SyncOtherMachine": 2, // メッセージは送信者に同期されていません。メッセージをFrom_Accountに同期させる場合は、SyncOtherMachineに1を入力します。
        "To_Account": userID,
        "MsgLifeTime":60, // メッセージは60秒保存されます
        "MsgRandom": 1287657,
        "MsgTimeStamp": Math.floor(Date.now() / 1000), // 単位は秒。整数である必要があります
        "MsgBody": [
          {
            "MsgType": "TIMTextElem",
            "MsgContent": {
              "Text": content
            }
          }
        ]
      },
      method: 'POST'
    }).then((res) => {
      if (res.data.ErrorCode === 0) {
        console.log('sendC2CTextMessage ok.', res.data);
        resolve();
      } else {
        reject(res.data);
      }
    }).catch((error) => {
      console.log('sendC2CTextMessage failed.', error);
      reject(error);
    });
  });
}

// WeChatのpostリクエストを処理します
app.post('/', function(req, res) {
  var buffer = [];
  // データを受信するために、dataイベントを監視します
  req.on('data', function(data) {
    buffer.push(data);
  });
  // 受信を完了したデータを処理するために、 endイベントを監視します
  req.on('end', function() {
    const tmpStr = Buffer.concat(buffer).toString('utf-8');
    xml2js.parseString(tmpStr, { explicitArray: false }, function(err, result) {
      if (err) {
        console.log(err);
        res.send("success");
      } else {
        if (!result) {
          res.send("success");
          return;
        }
        console.log('wx post data:', result.xml);
        var wxXMLData = result.xml;
        var toUser = wxXMLData.ToUserName; // 受信者のWeChat
        var fromUser = wxXMLData.FromUserName;// 送信者のWeChat
        if (wxXMLData.Event) {  // イベントタイプの処理
          switch (wxXMLData.Event) {
            case "subscribe": // サブスクリプションアカウントのフォロー
              res.send(genWxTextReplyXML(fromUser, toUser, 'フォローしていただき、ありがとうございます、XXはあなたを心より歓迎いたします！'));
              importAccount(fromUser).then(() => {
                // インポート済みユーザーのIDを記録します
                importedAccountMap.set(fromUser, 1);
              });
              break;
            case "unsubscribe": // フォローをキャンセルします
              deleteAccount(fromUser).then(() => {
                importedAccountMap.delete(fromUser);
              });
              res.send("success");
              break;
          }
        } else { // メッセージタイプを処理します
          switch (wxXMLData.MsgType) {
            case "text":
              // テキストメッセージを処理します
              sendC2CTextMessage(kfAccount1, 'WeChatサブスクリプションアカウントからの問い合わせ：' + wxXMLData.Content).then(() => {
                console.log('C2Cメッセージの送信に成功');
              }).catch((error) => {
                console.log('C2Cメッセージの送信に失敗');
              });
              break;
            case "image":
              // 画像メッセージを処理します
              break;
            case "voice":
              // 音声メッセージを処理します
              break;
            case "video":
              // ビデオメッセージを処理します
              break;
            case "shortvideo":
              // ショートビデオメッセージを処理します
              break;
            case "location":
              // 地理的位置の送信を処理します
              break;
            case "link":
              // リンクメッセージのクリックを処理します
              break;
            default:
              break;  
          }
          res.send(genWxTextReplyXML(fromUser, toUser, 'オペレーターにお繋ぎしています、お待ちください'));
        }
      }
    })
  });
});
```

### 手順6：IMサードパーティからのコールバックの登録と処理

<pre><code><span class="hljs-comment">// IMサードパーティからのコールバックの postリクエストを処理します</span>
app.post(<span class="hljs-string">'/imcallback'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">req, res</span>) </span>{
  <span class="hljs-keyword">var</span> buffer = [];
  <span class="hljs-comment">// データを受信するためにdataイベントを監視します</span>
  req.on(<span class="hljs-string">'data'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">data</span>) </span>{
    buffer.push(data);
  });
  <span class="hljs-comment">//　受信を完了したデータを処理するためendイベントを監視します</span>
  req.on(<span class="hljs-string">'end'</span>, <span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-keyword">const</span> tmpStr = Buffer.concat(buffer).toString(<span class="hljs-string">'utf-8'</span>);
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'imcallback'</span>, tmpStr);
    <span class="hljs-keyword">const</span> imData = <span class="hljs-built_in">JSON</span>.parse(tmpStr);
    <span class="hljs-comment">// kfAccount1が送信したメッセージを顧客にプッシュします</span>
    <span class="hljs-keyword">if</span> (imData.From_Account === kfAccount1) {
      <span class="hljs-comment">// メッセージをグループ化し、WeChatの【カスタマーサービスメッセージ】インターフェースを介して指定のユーザーにメッセージをプッシュします</span>
      <span class="hljs-comment">// 注意！個人登録のサブスクリプションアカウントは、このインターフェースの使用が許可されていません、詳細については <a href="https://developers.weixin.qq.com/doc/offiaccount/Message_Management/Service_Center_messages.html">カスタマーサービスメッセージ</a>をご参照ください。</span>
    }

    res.send({
      <span class="hljs-string">"ActionStatus"</span>: <span class="hljs-string">"OK"</span>,
      <span class="hljs-string">"ErrorInfo"</span>: <span class="hljs-string">""</span>,
      <span class="hljs-string">"ErrorCode"</span>: <span class="hljs-number">0</span> <span class="hljs-comment">// 0は発言許可を、1は発言拒否を表します</span>
    });
  });
});</code></pre>

