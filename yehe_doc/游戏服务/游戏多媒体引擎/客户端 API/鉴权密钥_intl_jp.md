
開発者がTencent Cloud Gaming Multimedia Engineのデバッグやアクセスを行いやすいように、すべてのプラットフォームに適用する認証キーの技術ドキュメントについて説明します。


## 音声キーのバッグクラウドデプロイ
Tencent Cloud Gaming Multimedia Engineは、リアルタイム音声とオフライン音声の認証に使われる認証キーを提供しています。このドキュメンテーションはバックグラウンドデプロイソリューションです。
認証に使用されるサインの作成プロセスは、**平文**、**キー**と**アルゴリズム**に関わっています。

### 平文
平文は、下記フィールドのネットワークバイトオーダーの組み合わせです。

|フィールドの説明    | タイプ/長さ| 値の定義/備考|
| ---------------- |-------------------|--------------|
| cVer				|unsigned char(1)	|バージョン番号、入力する数値：1		|
| wOpenIDLen		|unsigned short(2)	|ユーザーアカウントの長さ|
| strOpenID|wOpenIDLen|ユーザーアカウントのID文字|
| dwSdkAppid		|unsigned (4)	|開発者のSDKappid		|
| dwReserved1		|unsigned int(4)		|入力する数値：0				|
| dwExpTime		|unsigned int(4)		|期限が切れる時刻（現在の時間+有効期間［単位：秒、300秒を推奨］）|
| dwReserved2		|unsigned int(4)		|入力する値：-1または0xFFFFFFFF|
| dwReserved3		|unsigned int(4)		|入力する数値：0				|
| wRoomIDLen		|unsigned short(2)	|ユーザーが参加するルーム番号の長さ。オフラインボイスサービスの場合、0を入力してください				|
| strRoomID|wRoomIDLen|ユーザーは入室するルームの番号の文字|

### キー
Tencent Cloud GMEコンソールで関連する権限キーを取得します。

### アルゴリズム
TEA対称暗号化アルゴリズムです。
全体としては、初期にはクライアントにデプロイし、後期にはゲームAppのバックグラウンドにデプロイすることをお勧めします。

|ソリューション     | メリット        | デメリット|
| ------------- |-------------|-------------| 
| バックグラウンドデプロイ    |安全性が高い|バックグラウンドでの開発と結合テストが必要|
| クライアントデプロイ     |迅速にアクセスする|安全性が低い|

#### バックグラウンドデプロイの使い方
バックグラウンドで暗号化の文字列を生成してから、クライアントにデリバーします。クライアントは下記ケースに適用されています。API:EnterRoomを呼び出し入室する時に、暗号化した文字列を入室パラメータのauthBufferフィールドに発送します。




### 暗号化アルゴリズムに関する詳細状況
- キー：APPIDは認証キーのmd5値に対応し、長さが16バイトである
- 暗号化アルゴリズム：TEA暗号化
- 暗号化ベース及びその例：添付ファイル [authbuffer.zip](https://main.qcloudimg.com/raw/c8be793e20c85114499f52e0f8c29190.zip)

>!コンソールで暗号鍵を変更した後、15分間～1時間以内に有効となります。頻繁な交換はお勧めしません。



#### 暗号化の方法	
1.　平文の数字をネットワークバイトオーダーに変換します。
2.　平文を順序付け（平文フィールドの宣言順）で1つの文字列につなぎ合わせます。
3. teaで接続文字列を暗号化し、symmetry_encrypt関数から出力される文字列が権限暗号化文字列です。

>!2進列を16進法に変換する必要はありません。


## サンプルコード
C++言語の場合、認証キーのサンプルコードは次のとおりです：
```C++
unsigned char pInBuf[512]={0};
    xel::byte_writer bw(pInBuf, sizeof(pInBuf));
    
    char cVer = 1;
    unsigned short wOpenIDLen = (unsigned short)strlen((const char *)strOpenID);
        if (wOpenIDLen > 127) wOpenIDLen = 127;
    unsigned short wRoomIDLen = (unsigned short)strlen((const char *)strRoomID);
        if (wRoomIDLen > 127) wRoomIDLen = 127;
    
    bw.write_byte(cVer);
    bw.write_int16(wOpenIDLen);
    bw.write_bytes(strOpenID, wOpenIDLen);
    bw.write_int32(dwSdkAppId);
    bw.write_int32(0 /*dwRoomID*/);
    bw.write_int32(expTime);
    bw.write_int32(nAuthBits);
    bw.write_int32(0 /*dwAccountType*/);
    bw.write_int16(wRoomIDLen);
    bw.write_bytes(strRoomID, wRoomIDLen);
    
    int pInLen = bw.bytes_write();
    
        unsigned char pEncryptOutBuf[512] = { 0 };
    int iEncrptyLen = 0;
    
        symmetry_encrypt((const unsigned char*)pInBuf, pInLen, (const unsigned char*)key, (unsigned char*)pEncryptOutBuf, &iEncrptyLen);
```

JavaおよびGo言語のサンプルコードも用意されています。[クリックしてダウンロードします>>](https://dldir1v6.qq.com/hudongzhibo/QCloud_TGP/GME/pubilc/authbuffer_go_java.zip)。

