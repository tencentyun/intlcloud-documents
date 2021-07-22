## 操作シナリオ
プッシュの設定によって、対応するプッシュドメイン名でプッシュアドレスを発行し、ストリームをプッシュアドレスにプッシュして、ライブストリーミングのストリームをCSSサービスへ伝送する、つまりCSSビデオをアップロードすることができます。

## 前提条件
-  [CSSコンソール](https://console.cloud.tencent.com/live)にログイン済みであること。
- プッシュドメイン名を追加していること。

## プッシュアドレスジェネレーター
1. [【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)に入り、設定したいプッシュドメイン名を選択するか、【管理】をクリックし、ドメイン名の詳細ページに入ります。
![](https://main.qcloudimg.com/raw/f57795fb5a6497ff59a1612c5d805ad2.png)
2. 【プッシュ設定】>【プッシュアドレスジェネレーター】を選択し、次のとおり設定を行います。
	1. 有効期限を選択します（例：`2019-10-31 23:59:59）。
	2. カスタマイズされたカスタムストリーム名StreamNameを入力します（例：liveteststream）。
	3. 【プッシュアドレスの発行】をクリックすると、 StreamNameの付いたRTMPプッシュアドレスが発行されます。
![](https://main.qcloudimg.com/raw/a12dc5bb7d739ca7d526f35e9f22e81e.png)
RTMPプッシュアドレスの形式は、
```
rtmp://domain/live/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
そのうち、
		- `domain`：CSSプッシュドメイン名。
		- `AppName`：CSSアプリケーション名。デフォルトはliveで、カスタマイズ可能です。
		- `StreamName`：ライブストリーミングのストリームを識別するために用いる、ユーザー定義のストリーム名。
		- `txSecret`：プッシュ認証を有効にした後に生成される認証文字列。
		- `txTime`：プッシュアドレスのタイムスタンプは、コンソールのストリーミングアドレスの有効時間です。

3. 業務シナリオに応じて [CSSプッシュ](https://intl.cloud.tencent.com/document/product/267/31558)を実装した後、 [ストリーム管理](https://intl.cloud.tencent.com/document/product/267/31068)においてテスト、無効化、削除が行えます。

> 
>- 発行されたプッシュアドレスは、設定された有効期限内は使用可能です。期限が切れた場合、新しいプッシュアドレスを再発行できます。
>- プッシュアドレスが発行されると、CSSプッシュを開始できますが、ライブストリーミングを視聴するには再生アドレスを取得する必要があります。詳細については、[再生設定](https://intl.cloud.tencent.com/document/product/267/31058)をご参照ください。


## プッシュアドレスのサンプルコード
Tencent CloudはPHPおよびJavaのプッシュアドレスのサンプルコードを提供します。サンプルコードを直接参照して、プッシュアドレスのアクセスを完了することができます。具体的な操作は次のとおりです。
1. 【[Domain Management](https://console.cloud.tencent.com/live/domainmanage)】に進みます。
2. プッシュドメイン名を選択するか、右側の【管理】をクリックしてドメイン名詳細ページに進みます。
3. 【プッシュ設定】を選択し、一番下までプルダウンして【プッシュアドレスサンプルコード】タブを表示します。
4. タブ切り替えボタンをクリックして、PHP/Javaサンプルコードを表示します。

**プッシュサンプルコード(PHP)：**
```
/**
    * プッシュアドレスの取得
    * keyと有効期限が渡されない場合、ホットリンク防止のないURLが返されます
    * @param domainプッシュに使用するドメイン名
    *        streamName さまざまなプッシュアドレスを区別するために使用する一意のストリーム名
    *        key セキュリティキー
    *        time 有効期限 sample 2016-11-12 12:00:00
    * @return String url
*/
function getPushUrl($domain, $streamName, $key = null, $time = null){
	if($key && $time){
		$txTime = strtoupper(base_convert(strtotime($time),10,16));
		//txSecret = MD5( KEY + streamName + txTime )
		$txSecret = md5($key.$streamName.$txTime);
		$ext_str = "?".http_build_query(array(
			       "txSecret"=> $txSecret,
			       "txTime"=> $txTime
		));
    }
	return "rtmp://".$domain."/live/".$streamName . (isset($ext_str) ? $ext_str : "");
}
echo getPushUrl("123.test.com","123456","69e0daf7234b01f257a7adb9f807ae9f","2016-09-11 20:08:07");
```
**プッシュサンプルコード(Java)：**
```
package com.test;
import java.io.UnsupportedEncodingException;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;
public class Test {
    public static void main(String[] args) {
        System.out.println(getSafeUrl("txrtmp", "11212122", 1469762325L));
    }
    private static final char[] DIGITS_LOWER =
        {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f'};
    /*
    * KEY+ streamName + txTime
    */
    private static String getSafeUrl(String key, String streamName, long txTime) {
        String input = new StringBuilder().
                            append(key).
                            append(streamName).
                            append(Long.toHexString(txTime).toUpperCase()).toString();
        String txSecret = null;
        try {
            MessageDigest messageDigest = MessageDigest.getInstance("MD5");
            txSecret  = byteArrayToHexString(
                        messageDigest.digest(input.getBytes("UTF-8")));
        } catch (NoSuchAlgorithmException e) {
                e.printStackTrace();
        } catch (UnsupportedEncodingException e) {
                e.printStackTrace();
        }
        return txSecret == null ? "" :
                           new StringBuilder().
                           append("txSecret=").
                           append(txSecret).
                           append("&").
                           append("txTime=").
                           append(Long.toHexString(txTime).toUpperCase()).
                           toString();
        }
    private static String byteArrayToHexString(byte[] data) {
        char[] out = new char[data.length << 1];
        for (int i = 0, j = 0; i < data.length; i++) {
                out[j++] = DIGITS_LOWER[(0xF0 & data[i]) >>> 4];
                out[j++] = DIGITS_LOWER[0x0F & data[i]];
        }
        return new String(out);
    }
}
```
