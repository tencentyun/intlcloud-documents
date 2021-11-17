サーバーでのビデオアップロードのシナリオを実現させるために、VODではGo SDKを提供しています。アップロードのフローは、[サーバーからのアップロードガイド](https://intl.cloud.tencent.com/document/product/266/33912)をご参照ください。

## 統合方式

### go getを使用してインポート
```json
go get -u github.com/tencentcloud/tencentcloud-sdk-go
go get -u github.com/tencentyun/cos-go-sdk-v5
go get -u github.com/tencentyun/vod-go-sdk
```

### ソースコードパッケージによるインストール
プロジェクトの中にソースコードを直接インポートする必要がある場合は、ソースコードを直接ダウンロードしてプロジェクトにインポートし、使用することができます。

* [Githubからアクセス](https://github.com/tencentyun/vod-go-sdk)
* [クリックしてGo SDKをダウンロード](https://github.com/tencentyun/vod-go-sdk/archive/master.zip)

##  シンプルビデオアップロード
### アップロードオブジェクトの初期化
Tencent Cloud APIキーを使用して、VodUploadClientインスタンスを初期化します。

```
import (
	"github.com/tencentyun/vod-go-sdk"
)

client := &vod.VodUploadClient{}
client.SecretId = "your secretId"
client.SecretKey = "your secretKey"
```

### アップロードリクエストのオブジェクト作成
```
import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
)

req := vod.NewVodUploadRequest()
req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
```

### アップロードの呼び出し
アップロードメソッドを呼び出し、アクセスポイントリージョンおよびアップロードリクエストを渡します。
```
rsp, err := client.Upload("ap-guangzhou", req)
if err != nil {
    fmt.Println(err)
    return
}
fmt.Println(*rsp.Response.FileId)
fmt.Println(*rsp.Response.MediaUrl)
```

>?アップロード方法は、ファイルのサイズに応じて、通常アップロードとマルチパートアップロードが自動的に選択されます。マルチパートアップロードの各手順を気にすることなく、マルチパートアップロードを行うことができます。

## 高度な機能
### カバーの付加
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    req.CoverFilePath = common.StringPtr("/data/video/Wildlife-cover.png")
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
    fmt.Println(*rsp.Response.CoverUrl)
}
```

### タスクフローの指定
まず、[タスクフローテンプレートの作成](https://intl.cloud.tencent.com/document/product/266/14058)、およびテンプレートに対する命名を行います。タスクフロー時に、このタスクフローテンプレート名を使用して`Procedure`パラメータを設定すれば、アップロード成功後、タスクフローを自動的に実行することができます。
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    req.Procedure = common.StringPtr("Your Proceducre Name")
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
}
```

### サブアプリケーションのアップロード
[サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987)IDを渡します。アップロード成功後、リソースは具体的なサブアプリケーションにのみ属します。
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    req.SubAppId = common.Uint64Ptr(101)
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
}
```

### ストレージリージョンの指定
[コンソール](https://console.cloud.tencent.com/vod)で目標ストレージリージョンがアクティブ化されているか確認します。アクティブ化されていない場合は、[アップロードストレージ設定](https://intl.cloud.tencent.com/document/product/266/18874)をご参照ください。最後に、`StorageRegion`の属性によって、ストレージリージョンの [英語の略称](https://intl.cloud.tencent.com/document/product/266/9760)を設定します。
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    req.StorageRegion = common.StringPtr("ap-chongqing")
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
}
```

### パート同時実行数の指定
パート同時実行数は、大きなファイルに対応するもので、複数のパートに分割すると同時にアップロードするものです。パート同時アップロードのメリットは、1個のファイルのアップロードを素早く完了させられることで、SDKはファイルのサイズを基に、通常アップロードとパートアップロードを自動的に選択します。ユーザーは、パートアップロードの各手順に気を遣う必要もなく、パートでのアップロードを実現できます。こうしてファイルの同時パート数は、`ConcurrentUploadNumber`パラメータによって指定します。
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    req.ConcurrentUploadNumber = common.Uint64Ptr(5)
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
}
```

### 一時的な証明書の使用によるアップロード
一時的な証明書の関連キー情報を渡し、一時的な証明書を使用して身分を検証し、アップロードします。
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "Credentials TmpSecretId"
    client.SecretKey = "Credentials TmpSecretKey"
    client.Token = "Credentials Token"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
}
```


### アップロードのプロキシ設定
アップロードのプロキシ設定では、関係するプロトコルおよびデータはいずれもプロキシ経由で処理します。開発者はプロキシを参照しながら、ファイルを自社インターネットかたテンセントクラウドにアップロードします。
```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
    "net/http"
    "net/url"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    proxyUrl, _ := url.Parse("your proxy url")
	client.Transport = &http.Transport{
		Proxy: http.ProxyURL(proxyUrl),
	}
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/Wildlife.mp4")
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
}
```

### アダプティブビットレートストリーミング（ABS）ファイルのアップロード
このSDKでアップロードをサポートするABS形式のパッケージにはHLSとDASHがあります。manifest（M3U8またはMPD）で引用するメディアファイルは、必ず相対パスとし（URLおよび絶対パスは不可）、同時にmanifestと同じクラスのディレクトリまたは下の階層のディレクトリに置く必要があります（`../`は使用不可）。SDKのアップロードインターフェースを呼び出す時に、`MediaFilePath`パラメータにmanifest を入力すると、SDKが関連するメディアファイルリストを解析し、一緒にアップロードされます。

```
package main

import (
	"github.com/tencentcloud/tencentcloud-sdk-go/tencentcloud/common"
	"github.com/tencentyun/vod-go-sdk"
	"fmt"
)

func main() {
    client := &vod.VodUploadClient{}
    client.SecretId = "your secretId"
    client.SecretKey = "your secretKey"
    
    req := vod.NewVodUploadRequest()
    req.MediaFilePath = common.StringPtr("/data/video/prog_index.m3u8")
    
    rsp, err := client.Upload("ap-guangzhou", req)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(*rsp.Response.FileId)
    fmt.Println(*rsp.Response.MediaUrl)
    fmt.Println(*rsp.Response.CoverUrl)
}
```

## インターフェースの説明
アップロードクライアントクラス`VodUploadClient`

| 属性名      | 属性説明                   | タイプ      | 入力必須   |
| --------- | ---------------------- | ------- | ---- |
| SecretId   | Tencent Cloud APIキーID。        | String | はい    |
| SecretKey | Tencent Cloud API Key。 | String  | はい   |

アップロードリクエストクラス`VodUploadRequest`

| 属性名      | 属性説明                   | タイプ&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; |入力必須   |
| --------- | ---------------------- | ------- | ---- |
| MediaFilePath   | アップロード予定のメディアファイルパス。ローカルパスにする必要があります。URLはサポートしていません。| Stringポインタ | はい    |
| MediaType   | アップロード予定のメディアファイルタイプ。選択可能なタイプの詳細は、[メディアアップロードの概要](https://intl.cloud.tencent.com/document/product/266/9760)をご参照ください。MediaFilePathに拡張子が付いている場合は入力不要です。        | Stringポインタ | いいえ    |
| MediaName   | アップロード後のメディアの名前。入力しない場合は、デフォルトでMediaFilePathのファイル名を採用します。      | Stringポインタ | いいえ    |
| CoverFilePath   | アップロード予定のカバーファイルパス。ローカルパスにする必要があります。URLはサポートしていません。 | Stringポインタ | いいえ    |
| CoverType   | アップロード予定のカバーファイルタイプ。選択可能なタイプの詳細は、[メディアアップロードの概要](https://intl.cloud.tencent.com/document/product/266/9760)をご参照ください。CoverFilePathに拡張子が付いている場合は入力不要です。        | Stringポインタ | いいえ    |
| Procedure   | アップロード後に自動的に実行させたいタスクフロー名。このパラメータは、タスクフローの作成（[API方式](https://intl.cloud.tencent.com/zh/document/product/266/33897) または[コンソール方式](https://console.cloud.tencent.com/vod/video-process/taskflow)）時にユーザーが指定します。具体的な内容は、[タスクフロー概要](https://intl.cloud.tencent.com/document/product/266/33931)をご参照ください。       | Stringポインタ | いいえ    |
| ExpireTime   | メディアファイルの期限。表記形式はISO 8601規格に準拠します。詳細については、[ISO日時表記形式の説明](https://intl.cloud.tencent.com/document/product/266/11732)をご参照ください。        | Stringポインタ | いいえ    |
| ClassId   | カテゴリーID。メディアのカテゴリー管理に使用します。[カテゴリー作成](https://intl.cloud.tencent.com/document/product/266/35325) インターフェースによってカテゴリーを作成し、カテゴリーIDを取得することができます。        |  int64ポインタ | いいえ    |
| SourceContext   | ソースコンテキスト。ユーザーリクエスト情報のパススルーに使用します。アップロードコールバックインターフェースは、このフィールドの値を戻します。最長250文字。        | Stringポインタ | いいえ    |
| SubAppId   | VOD [サブアプリケーション](https://intl.cloud.tencent.com/document/product/266/33987)ID。サブアプリケーションの中のリソースにアクセスしたい場合は、このフィールドにサブアプリケーションIDを入力します。アクセスしない場合、この項目は入力不要です。        | uint64ポインタ | いいえ    |
| StorageRegion   | ストレージリージョン。ストレージを予定/希望するリージョンを指定します。このフィールドにはストレージリージョンの[英語の略称](https://intl.cloud.tencent.com/document/product/266/9760)を入力します。        | Stringポインタ | いいえ    |
| ConcurrentUploadNumber   | パート同時実行数。大きなファイルを対象にパートアップロードする時に有効となります。        | Integer | いいえ    |

アップロードレスポンスクラス `VodUploadResponse`

| 属性名      | 属性説明                   | タイプ      |
| --------- | ---------------------- | ------- |
| Response   | アップロードの結果情報を戻します。        | struct |
| Response.FileId   | メディアファイルの一意の標識。        | String ポインタ |
| Response.MediaUrl | メディア再生アドレス。 | String ポインタ  |
| Response.CoverUrl | メディアカバーアドレス。 | String ポインタ  |
| Response.RequestId | 一時的なリクエストID。リクエストごとに返されます。問題を特定する時はその回のリクエストのRequestIdを提供する必要があります。 | Stringポインタ  |

アップロードメソッド `VodUploadClient.Upload(region string, request *VodUploadRequest)`

| パラメータ名      | パラメータの説明                   | タイプ      | 入力必須   |
| --------- | ---------------------- | ------- | ---- |
| region   | アクセスポイントリージョン。どのリージョンのVODサーバーにリクエストするかであり、ストレージリージョンとは異なります。具体的な内容は、サポートする[リージョンリスト](https://intl.cloud.tencent.com/document/product/266/34113)をご参照ください。        | String | はい    |
| request   | アップロードリクエスト。        | VodUploadRequest ポインタ | はい    |

## エラーコードリスト

| ステータスコード         | 意味               |
| ----------- | ----------------- |
| InternalError       | 内部エラー。 |
| InvalidParameter.ExpireTime       | パラメータ値のエラー：期限。 |
| InvalidParameterValue.CoverType       | パラメータ値のエラー：カバーのタイプ。     |
| InvalidParameterValue.MediaType       | パラメータ値のエラー：メディアタイプ。           |
| InvalidParameterValue.SubAppId       | パラメータ値のエラー：サブアプリケーションID。              |
| InvalidParameterValue.VodSessionKey       | パラメータ値のエラー：VODセッション。              |
| ResourceNotFound       | リソースがありません。              |
