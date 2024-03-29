## 機能の説明
- 第三者がビデオURLを取得して、長期的に使用することができないように、ビデオURLの有効期限を指定できます。
- 第三者がビデオURLを取得して視聴人数の制限なく配布することができないように、ビデオURLで再生可能な最大IP数を指定できます。
- ビデオURLでのプレビュー時間の指定をサポートし、プレビュー機能を実現します。
- `KEY` を使用してビデオURLに署名し、URLに署名結果を含めることができます。ユーザーキーを開示しない限り、他のユーザーはビデオURLを偽造することができません。
- CDNノードは、ビデオURLのパラメータと署名を検査し、ビデオ再生リクエストを制御します。リクエストが検査に不合格となった場合は、403レスポンスコードが返されます。
- サポートするファイルタイプ：MP4、TS、M3U8、FLV、AAC、MOV、WMV、AVI、MP3、RMVB、MKV、MPG、3GP、WEBM、M4V、ASF、F4V、WAV、MPEG、VOB、RM、WMA、DAT、M4A、MPD、M4S。

>?Keyリンク不正アクセス防止の有効化については、[リンク不正アクセス防止の設定](https://intl.cloud.tencent.com/document/product/266/14060)をご参照ください。

## リンク不正アクセス防止URLの生成方法
- VODでのビデオにはすべて**ビデオオリジナルURL**が存在します。リンク不正アクセス防止が有効になっていない場合は、ビデオオリジナルURLを使用して、ビデオを再生することができます。
- Keyリンク不正アクセス防止を有効にすると、ビデオオリジナルURLは再生できなくなり、この場合、ビデオの**リンク不正アクセス防止URL**を生成する必要があります。

リンク不正アクセス防止URLの生成ルールは、オリジナルURLの末尾に、QueryStringの形式でリンク不正アクセス防止パラメータを追加することです。形式は次のとおりです。
```
http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4?t=[t]&exper=[exper]&rlimit=[rlimit]&us=[us]&sign=[sign]
```
リンク不正アクセス防止URLの各パラメータの定義と値の取得方法について、以下で詳細に説明します。

#### リンク不正アクセス防止パラメータ
| パラメータ名 | 入力必須 | 説明                                                         |
| ------ | ---- | ------------------------------------------------------------ |
| `KEY`    | 必須    | Keyリンク不正アクセス防止を有効にする場合に入力するキーです。アルファベットの大文字小文字（a～Z）または数字（0～9）で構成され、長さは8～20文字とする必要があります。コンソールで【KEY生成】をクリックして生成することを推奨します。具体的な操作手順については、 [リンク不正アクセス防止の設定](https://intl.cloud.tencent.com/document/product/266/14060) をご参照ください。 |
| `Dir`    | 必須   | ビデオオリジナルURLのPATHのファイル名を削除した部分のパスです。オリジナルURLが`http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4`であれば、再生パスは`/dir1/dir2/` となります |
| `t`      | 必須   | <li>再生アドレスの期限切れのタイムスタンプであり、16進数小文字のUnix時間の形式で表示されます<br><li>期限切れ後、このURLは無効になり、403レスポンスコードが返されます。デバイス間に時間差が存在することを考慮し、リンク不正アクセス防止URLの実際の有効期限は、通常、指定の有効期限より5分長くなります。つまり、300秒の許容誤差時間が追加されます<br><li>期限切れまでのタイムスタンプの時間は、ビデオを完全に再生できる充分な時間を確保することを推奨します |
| `exper`  | 必須ではない   | <li>プレビュー時間。単位は秒。10進法で表示されます。空のまま、または0を入力するとプレビューは無効になります（つまり、完全なビデオが返されます）<br><li>プレビュー時間はビデオのオリジナルの時間を超えないようにしてください。超えてしまうと、再生に失敗する可能性があります |
| `rlimit` | 必須ではない   | <li>再生可能な最大端末IP数。10進法で表示され、最大値は9です。空のままにした場合、制限はありません<br><li>URLを1人しか再生できないように制限する場合は、モバイル端末のIPがネットワークから切断して再度アクセス時に変更される可能性があるため、rlimitを厳密に1に制限しないことを推奨します（3に設定するなど）|
| `us`     | 必須ではない   | <li>リンクID。リンクの一意性を高めるため、リンク不正アクセス防止URLのランダム化に使用されます<br><li>リンク不正アクセス防止URLを生成するときは毎回 、ランダムなus値を指定することを推奨します|
| `sign`   | 必須   | <li>リンク不正アクセス防止の署名。32文字の長さの16進数で表示され、リンク不正アクセス防止URLの有効性の検証に使用されます<br><li>署名検証に失敗すると、403レスポンスコードが返されます。 [署名の計算式](#formula)については、以下で説明します |


#### [](id:formula)署名の計算式
```
sign = md5(KEY + Dir + t + exper + rlimit + us)
```

式の`+`は文字列のスプライスを意味し、オプションのパラメータを空白の文字列にすることができます。

## リンク不正アクセス防止URLの生成例
VODにビデオがあり、ビデオのオリジナル再生URLが`http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4`で、Keyリンク不正アクセス防止を有効にし、生成されたキーが`24FEQmTzro4V5u3D5epW`、生成されたランダム文字列が`72d4cd1101`であり、次の条件を満たす必要がある場合。
1. このビデオのためにリンク不正アクセス防止URLを生成し、URLの有効期限を2018年01月31日20:00（Unix時間では1517400000）とします。
2. プレビューURLを生成し、プレビュー時間をビデオの最初の5分間（オリジナルのビデオの時間は5分より長いこと）とします。
3. URLで再生可能なIP数を最大で3つの異なるIPに制限し、端末でこのURLの再生を許可します。

「ビデオ再生アドレス有効期限の制御」、「ビデオ再生アドレスでの最大再生許可IP数」と「ビデオ再生許可時間の制御」について、それぞれのリンク不正アクセス防止URLの生成方法を、以下に説明します。

### 例1：再生アドレス有効期限の制御
#### ステップ1：リンク不正アクセス防止パラメータの確定

| パラメータ名 | 値                   | 説明                                               |
| ------ | ---------------------- | -------------------------------------------------- |
| `KEY`    | `24FEQmTzro4V5u3D5epW` | Keyリンク不正アクセス防止を有効にする時に選択したキー                  |
| `Dir`    | `/dir1/dir2/`          | 元の再生URLのPATHから`myVideo.mp4`を除いた残りの部分 |
| `t`      | `5a71afc0`             | 期限切れタイムスタンプ（例えば1517400000）は16進数で結果が表されます             |
| `us`     | `72d4cd1101`           | 生成されたランダム文字列                                   |


#### ステップ2：署名の計算

```
sign = md5("24FEQmTzro4V5u3D5epW/dir1/dir2/5a71afc072d4cd1101") = "3d8488faeb37d52d6bf63b63c1b171c3"
```

#### ステップ3：リンク不正アクセス防止URLの生成
リンク不正アクセス防止パラメータをビデオオリジナルURLのQueryStringにスプライスし、ビデオリンク不正アクセス防止URLを取得します。
```
http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4?t=5a71afc0&us=72d4cd1101&sign=3d8488faeb37d52d6bf63b63c1b171c3
```

### 例2：再生アドレスでの最大再生可能IP数
#### ステップ1：リンク不正アクセス防止パラメータの確定

| パラメータ名 | 値                   | 説明                                               |
| ------ | ---------------------- | -------------------------------------------------- |
| `KEY`    | `24FEQmTzro4V5u3D5epW` | Keyリンク不正アクセス防止を有効にする時に選択したキー                  |
| `Dir`    | `/dir1/dir2/`          | 元の再生URLのPATHから`myVideo.mp4`を除いた残りの部分 |
| `t`      | `5a71afc0`             | 期限切れタイムスタンプ（例えば1517400000）は16進数で結果が表されます             |
| `rlimit` | `3`                    | URLの再生を許可するIPを最大3つに制限                  |
| `us`     | `72d4cd1101`           | 生成されたランダム文字列                                   |

#### ステップ2：署名の計算
```
sign = md5("24FEQmTzro4V5u3D5epW/dir1/dir2/5a71afc0372d4cd1101") = "c5214f0d5961b13acd558b4957c4dfc5"
```

#### ステップ3：リンク不正アクセス防止URLの生成
リンク不正アクセス防止パラメータをビデオオリジナルURLのQueryStringにスプライスし、ビデオリンク不正アクセス防止URLを取得します。
```
http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4?t=5a71afc0&rlimit=3&us=72d4cd1101&sign=c5214f0d5961b13acd558b4957c4dfc5
```

### 例3：再生許可時間の制御
#### ステップ1：リンク不正アクセス防止パラメータの確定

| パラメータ名 | 値                   | 説明                                               |
| ------ | ---------------------- | -------------------------------------------------- |
| `KEY`    | `24FEQmTzro4V5u3D5epW` | Keyリンク不正アクセス防止を有効にする時に選択したキー                  |
| `Dir`    | `/dir1/dir2/`          | 元の再生URLのPATHから`myVideo.mp4`を除いた残りの部分 |
| `t`      | `5a71afc0`             | 期限切れタイムスタンプ（例えば1517400000）は16進数で結果が表されます             |
| `exper`  | `300`                  | 最初の5分間、つまり300秒のプレビュー                                 |
| `us`     | `72d4cd1101`           | 生成されたランダム文字列                                   |

#### ステップ2：署名の計算

```
sign = md5("24FEQmTzro4V5u3D5epW/dir1/dir2/5a71afc030072d4cd1101") = "547d98c4b91e81b5ea55c95cef63223f"
```

#### ステップ3：リンク不正アクセス防止URLの生成
リンク不正アクセス防止パラメータをビデオオリジナルURLのQueryStringにスプライスし、ビデオリンク不正アクセス防止URLを取得します。
```
http://example.vod2.myqcloud.com/dir1/dir2/myVideo.mp4?t=5a71afc0&exper=300&us=72d4cd1101&sign=547d98c4b91e81b5ea55c95cef63223f
```

## Keyリンク不正アクセス防止の生成と検証のツール
VODはKeyリンク不正アクセス防止URLの生成ツールと検証ツールを提供し、開発者はそれらツールを使用して迅速かつ正確に要件に適合するリンク不正アクセス防止URLを生成し検証することができます。

- [Keyリンク不正アクセス防止生成ツール](https://vods.cloud.tencent.com/referer/gen_video_url.html)
- [Keyリンク不正アクセス防止検証ツール](https://vods.cloud.tencent.com/referer/check_sign.html)

## 注意事項
- この機能はオプションであり、デフォルトでは有効ではありません。
- この機能を有効にした後は、ビデオオリジナルURLでは直接再生できなくなるため、ルールに従い、有効なリンク不正アクセス防止URLを生成する必要があります。
- キー`KEY`は、大文字および小文字のアルファベット（a～Z）または数字（0～9）で構成され、長さは8～20文字とする必要があります。
- リンク不正アクセス防止URLが期限切れである場合、または署名が合格しない場合は、ビデオを再生できず、403レスポンスコードが返されます。
- リンク不正アクセス防止URLのQueryStringのパラメータは、`t`、`exper`、`rlimit`、`us`、`sign`の順に出現する必要があり、順序が正しくない場合は、ビデオを再生することができません。
- プレビュー機能を使用する場合、プレビュー時間はビデオ時間よりも短いことを確認する必要があり、ビデオ時間より長い場合は、ビデオを再生することができません。
- プレビューではビデオの形式に対する厳格な要件（例えばH.264のみ。ビデオメタ情報はビデオファイルのヘッダーに含まれている必要がある等）があり、形式要件に適合しないオリジナルビデオをプレビューすると異常が発生するおそれがあります。プレビュー機能を設定する前に、VODトランスコード機能を使用して、トランスコードすることをお勧めします（トランスコード後の形式がすべてプレビュー形式の要件に適合するようにします）。
