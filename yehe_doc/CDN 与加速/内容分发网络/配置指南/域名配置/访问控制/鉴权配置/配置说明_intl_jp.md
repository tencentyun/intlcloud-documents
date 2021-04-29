
## 設定シナリオ
通常、CDNを介して配信されるコンテンツはデフォルトでパブリックリソースであり、ユーザーはURLでコンテンツにアクセスできます。悪意のあるユーザーがコンテンツを盗用して利益を得ることを防ぐために、refererブラックリスト/ホワイトリスト、IPブラックリスト/ホワイトリスト、およびIPアクセス回数制限などのアクセス制御ポリシーに加えて、高度なタイムスタンプ認証を設定することで、盗用から防御することもできます。

> !タイムスタンプのリンク不正アクセス防止を設定した後、クライアントはリクエストを開始するときに設定に従って署名演算を実行して、サーバーに送信する必要があります。CDNノードはサーバーで署名を検証し、検証が正常に完了した場合にパスさせます。

## 設定ガイド
### 設定の確認
[CDNコンソール](https://console.cloud.tencent.com/cdn)にログインし、左側のナビゲーションメニューバーで【ドメイン管理】を選択して、ドメイン名の右側にある【管理】をクリックすると、ドメイン名設定画面に入ります。【アクセス制御】タブで、認証設定を確認できます。認証設定はデフォルトで無効になっています。
![](https://main.qcloudimg.com/raw/1efe407c5a9f2fc8f8837d5b1cdbb3d7.png)

### 設定の変更
#### 1. 設定を変更する
CDNサービスでは、4種類の認証署名計算モデルをご提供します。上記の【認証計算機】を使用して、各種認証方式と設定後の最終的な成果を確認することもできます。アルゴリズムの詳細説明については、 [TypeA](https://intl.cloud.tencent.com/document/product/228/35222)、[TypeB](https://intl.cloud.tencent.com/document/product/228/35223)、[TypeC](https://intl.cloud.tencent.com/document/product/228/35224)、[TypeD](https://intl.cloud.tencent.com/document/product/228/35225) をご参照ください。
![](https://main.qcloudimg.com/raw/ffd60184fa759b4c7a82a5a49634b8c3.png)

#### 2. 設定を無効にする
認証設定スイッチを切り替えて、この機能を無効にすることができます。スイッチがOFFの場合、既存の設定は実稼働環境では有効になりません。次回ONをクリックすると、ネットワーク全体で設定が有効になる前に、先に設定の2回目の確認が行われます。
![](https://main.qcloudimg.com/raw/f892392e86acae153ef7821944888155.png)

#### 3. リージョンの特別な設定
アクセラレーションドメイン名がグローバルアクセラレーション用に設定されており、中国本土内外のアクセラレーションリージョンに異なる認証を設定する場合は、設定の下にある【特別な設定の追加】をクリックして設定できます。
![](https://main.qcloudimg.com/raw/8e6e0e08ef230322f4366a4fa92288e0.png)

> !リージョンの特別な設定が追加された後、現在では削除することはできません。設定をオフにして無効にできます。

## 設定例
ドメイン名`cloud.tencent.com`がグローバルアクセラレーションドメイン名の場合、認証設定は下記のようになります。
![](https://main.qcloudimg.com/raw/1d82f89f383aa35f5d7ae679f19669fb.png)
実際の効果は次のようになります。

1. 中国本土のユーザーが、実際にリソース`http://cloud.tencent.com/1.jpg`にアクセスする場合、直接リクエストを開始できます。
2. 中国本土以外のユーザーが、実際にリソース`http://cloud.tencent.com/1.jpg`にアクセスする場合、リクエストURL形式は`http://cloud.tencent.com/509301d10da7b862052927ed7a947f43/5e561139/1.jpg`となります。


## サンプルコード

各認証の計算方法は、Python Demoを例に、以下に示します。

```
import requests
import json
import sys
import time
import hashlib

def generate_url(category, ts=None):
    url = 'http://www.test.com'              # テストドメイン名
    path = '/1.txt'                                     # アクセスパス
    suffix = '?a=1&b=2'                                 # URLパラメータ
    key = 'abc123456789'                                # 認証キー
    now = int(time.mktime(time.strptime(ts, "%Y%m%d%H%M%S")) if ts else time.time())                # 時間が入力された場合、入力されたtsを使用します。入力されていない場合、現在のtsを使用します。
    sign_key = 'key'                                    # url署名フィールド
    time_key = 't'                                      # url時間フィールド
    ttl_format = 10                                     # 時間の進数、10または16。typeDのみ対応
    if category == 'A':                                 #Type A
        ts = now
        rand_str = '123abc'
        sign = hashlib.md5('%s-%s-%s-%s-%s' % (path, ts, rand_str, 0, key)).hexdigest()
        request_url = '%s%s?%s=%s' % (url, path, sign_key, '%s-%s-%s-%s' % (ts, rand_str, 0, sign))
        print(request_url)
    elif category == 'B':                               #Type B
        ts = time.strftime('%Y%m%d%H%M', time.localtime(now))
        sign = hashlib.md5('%s%s%s' % (key, ts, path)).hexdigest()
        request_url = '%s/%s/%s%s%s' % (url, ts, sign, path, suffix)
        print(request_url)
    elif category == 'C':                               #Type C
        ts = hex(now)[2:]
        sign = hashlib.md5('%s%s%s' % (key, path, ts)).hexdigest()
        request_url = '%s/%s/%s%s%s' % (url, sign, ts, path, suffix)
        print(request_url)
    elif category == 'D':                               #Type D
        ts = now if ttl_format == 10 else hex(now)[2:]
        sign = hashlib.md5('%s%s%s' % (key, path, ts)).hexdigest()
        request_url = '%s%s?%s=%s&%s=%s' % (url, path, sign_key, sign, time_key, ts)
        print(request_url)


if __name__ == '__main__':
    if len(sys.argv) == 1:
        print('usage: python generate_url.py A 20200501000000')
    args = sys.argv[1:]
    generate_url(*args)
```
