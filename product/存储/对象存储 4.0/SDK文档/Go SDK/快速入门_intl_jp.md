## 開発準備

### 関連するリソース
オブジェクト保存COSのXML Go SDKリソースのダウンロードアドレス：[XML Go SDK](https://github.com/tencentyun/cos-go-sdk-v5)。詳しい情報については、[COS Go SDK API](https://godoc.org/github.com/tencentyun/cos-go-sdk-v5) ドキュメントを参照してください

### 環境依存関係

[Golang](https://golang.org/doc/install/source?spm=a2c4g.11186623.2.11.168ec486fb1eQK) Goコンパイル動作環境のダウンロードとインストールに用いられます。Goのインストール完了後、システム変数GOPATHを新たに作成し、またそれをご利用のコードディレクトリにディレクトしてください。
>?文章に記載されているSecretId、SecretKey、Bucketなどの名称の意味と取得方式については、[COS用語情報](https://cloud.tencent.com/document/product/436/7751)を参照してください。

### SDKインストール

下記のコマンドを実行してCOS Go SDKをインストールします：
```
 go get -u github.com/tencentyun/cos-go-sdk-v5/
```

## クイックスタート
本節は、COS Go SDKにより一般的操作を速やかに行う方法を紹介します。例えば、ユーザー側初期化、バケットの作成、ファイルのアップロードとダウンロード。
各APIは[example](https://github.com/tencentyun/cos-go-sdk-v5/tree/master/example)ディレクトリにおいて関連の使用例があります。
### ユーザー側初期化

COSドメイン名によりCOS GOユーザー側のClient構造を生成します。

#### 方法のプロトタイプ
```Go
func NewClient(uri *BaseURL, httpClient *http.Client) *Client
```
####　リクエスト例
```go
//<bucketname>、<appid>と<region>を実際の情報に変更します
//例えば：http://test-1253846586.cos.ap-guangzhou.myqcloud.com
u, _ := url.Parse("http://<bucketname>-<appid>.cos.<region>.myqcloud.com")
b := &cos.BaseURL{BucketURL: u}
client := cos.NewClient(b, &http.Client{
	Transport: &cos.AuthorizationTransport{
		//ユーザーのアカウント暗号鍵情報を記入し、もしくは環境変数に設定して良いです
		SecretID:  os.Getenv("COS_SECRETID"),                         
		SecretKey: os.Getenv("COS_SECRETKEY"),                      
	},                                 
})
```
#### パラメータ説明
```go
type AuthorizationTransport struct {
	SecretID     string
	SecretKey    string
	SessionToken string
	//署名の期限切れ時間
	Expire time.Duration         
}
```
#### 戻り結果の説明
返されるClientはService、バケットとオブジェクト構造を含みます。これらの構造はそれぞれのAPI関数の呼び出しに用いられます。説明の簡素化に向け、SDK APIドキュメント例はClient初期化のプロセスを省略します。

### バケットの作成

```Go
package main
import (
	"context"
	"io/ioutil"
	"net/http"
	"net/url"
	"os"
	"time"
	
	"github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
	//<bucketname>、<appid>と<region>を実際の情報に変更します
	//例えば：http://test-1253846586.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<bucketname>-<appid>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
			//事実通りにアカウントと暗号鍵を記入し、もしくは環境変数に設定して良いです
			SecretID:  os.Getenv("COS_SECRETID"),
			SecretKey: os.Getenv("COS_SECRETKEY"),
		},
	})
	
	_, err := c.Bucket.Put(context.Background(), nil)
	if err != nil {
		panic(err)
	}
}
```

### ファイルのアップロード

```Go
package main
import (
	"context"
	"net/url"
	"os"
	"strings"
	"net/http"

	"github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
	//<bucketname>、<appid>と<region>を実際の情報に変更します
	//例えば：http://test-1253846586.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<bucketname>-<appid>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
            //事実通りにアカウントと暗号鍵を記入し、もしくは環境変数に設定して良いです
			SecretID:  os.Getenv("COS_SECRETID"),
			SecretKey: os.Getenv("COS_SECRETKEY"),
		},
	})
    //オブジェクトキー（Key）は、バケットにおけるオブジェクトの唯一の識別子です。
	//例えば、オブジェクトのアクセスドメイン名` bucket1-1250000000.cos.ap-guangzhou.myqcloud.com/test/objectPut.go `において、オブジェクトキーはtest/objectPut.goです
	name := "test/objectPut.go"
	//Local file
	f := strings.NewReader("test")

	_, err := c.Object.Put(context.Background(), name, f, nil)
	if err != nil {
		panic(err)
	}
}
```

### ファイルのダウンロード

```Go
package main

import (
	"context"
	"fmt"
	"net/url"
	"os"
	"io/ioutil"
	"net/http"

	"github.com/tencentyun/cos-go-sdk-v5"
)

func main() {
	//<bucketname>、<appid>と<region>を実際の情報に変更します
	//例えば：http://test-1253846586.cos.ap-guangzhou.myqcloud.com
	u, _ := url.Parse("http://<bucketname>-<appid>.cos.<region>.myqcloud.com")
	b := &cos.BaseURL{BucketURL: u}
	c := cos.NewClient(b, &http.Client{
		Transport: &cos.AuthorizationTransport{
			//事実通りにアカウントと暗号鍵を記入し、もしくは環境変数に設定して良いです
			SecretID:  os.Getenv("COS_SECRETID"),
			SecretKey: os.Getenv("COS_SECRETKEY"),
		},
	})
    //Object key
	name := "test/hello.txt"
	resp, err := c.Object.Get(context.Background(), name, nil)
	if err != nil {
		panic(err)
	}
	bs, _ := ioutil.ReadAll(resp.Body)
	resp.Body.Close()
	fmt.Printf("%s\n", string(bs))
}
```

