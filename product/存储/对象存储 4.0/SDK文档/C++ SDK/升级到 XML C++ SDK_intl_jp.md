JSON C++ SDKとXML C++ SDKのドキュメントを細やかに比較したことがあれば、これが簡単な追加アップデートではないことに気付いたのでしょう。XML C++ SDKは構成、利用可能性と安全性において大いに向上している上、また利便性、構造安定性と送信性能においても大いに改善されています。XML C++ SDKにアップグレードするには、以下の説明に従い、C++ SDKのアップグレードを進めてください。

## 機能比較

XML C++ SDKとJSON C++ SDKの機能比較につき、下表を参照してください：

| 機能           |                              XML C++ SDK                              |                              JSON C++ SDK                              |
| -------------- | :----------------------------------------------------------: | :----------------------------------------------------------: |
| ファイルのアップロード        | ローカルファイル、バイトストリーム、入力ストリームのアップロードに対応します<br>同名ファイルへの上書き<br>簡単なアップロードは最大5GBまで対応します<br>マルチパートアップロードは最大48.82TB（50,000GB）まで対応します | ローカルファイルのアップロードに対応しているが、8M以上のファイルについて、その内容をマルチパートアップロードする必要があります<br>手動で同名ファイルへの上書きをするかを設定する必要があります<br>簡単なアップロードは最大20MBまで対応します<br>マルチパートアップロードは最大64GBまで対応します |
| バケットの基本操作 |            バケットの作成<br>バケットの取得<br>バケットの削除            |                            サポートしません                            |
| バケットACLの操作 |   バケットACLの設定<br>バケットACLの設定の取得<br>バケットACLの設定の削除 |                            サポートしません                            |
| バケットのライフサイクル | バケットのライフサイクルの作成<br>バケットのライフサイクルの取得<br>バケットのライフサイクルの削除 |                            サポートしません                            |
| ディレクトリ操作       |                            APIを独立に提供しません                            |               ディレクトリの作成<br>ディレクトリの照合<br>ディレクトリの削除               |

## アップグレード手順

以下の4つのステップでC++ SDKをアップグレードしてください。

**1. C++ SDKのアップデート**

[XML C++ SDK ](https://github.com/tencentyun/cos-cpp-sdk-v5)はPocoベースでJSON C++ SDKのcurlベースを代替し、[Poco公式サイト](https://pocoproject.org/download.html)からcompleteバージョンのPocoをダウンロードし、また以下のコマンドでPocoのベースとヘッダファイルをインストールします。

```
./configure --omit=Data/ODBC,Data/MySQL
make
make install
```
また、C++ SDK [クイックスタート](https://cloud.tencent.com/document/product/436/12301)ドキュメントを参照し、最適なインストール方式を選択することもできます。

**2. SDK構成ファイルの変更**

XML C++ SDKとJSON C++ SDKの初期化プロセスは同じだが、対応の構成ファイル"config.json"の内容が異なります。XML C++ SDKの設定ファイルにおいて、照合した上、以下の変化内容を変更してください：

- JSON C++ SDKにおける"APPID"構成項目を削除します。
- `ConnectTimeoutInms`は`CurlConnectTimeoutInms`と`CurlGlobalConnectTimeoutInms`を代替し、`ReceiveTimeoutInms`を新たに追加し、Requestベースクラスにおいても対応APIの設定を実装しており、それぞれの操作に応じて変更できます。
- XML C++ SDKの初期化デフォルトパラメータはファイル"cos_sys_config.cpp"において詳しく説明されています。
- JSON C++ SDKとXML C++ SDKの対応するRegionの説明が異なり、詳しくは下側の「バケット名と使用可能な地域の略称の変更」を参照してください。

**3. バケット名称とAvailability Zoneの略称を変更します**

XML C++ SDKのバケット名とAvailability Zone略称はJSON C++ SDKのと異なります。関連の変更が必要です。

**バケット**

XML C++ SDKのバケット名は2つの部分からなります：ユーザーカスタマイズの文字列とAPPID。二者をハイフン「-」でつなぎます。例えば`mybucket1-1250000000`、そのうち`mybucket1`はユーザーカスタマイズの文字列で、`1250000000`はAPPIDです。

>?APPIDはTencent Cloudのアカウントタグの1つで、クラウドリソースの関連付けに用いられます。Tencent Cloudアカウントの登録ができたら、システムは自動でユーザーにAPPIDを発行します。[Tencent Cloudコンソール](https://console.cloud.tencent.com/) 【アカウント情報】を通じてAPPIDを確認できます。

Bucketの設定にあたって、以下のサンプルコードを参照してください：

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
//JSON C++ SDKのAppIDは構成ファイルに記載されています。JSON C++ SDKのBucket定義は：string bucket = "mybucket1";
string bucket = "mybucket1-1250000000";
qcloud_cos::HeadBucketReq req(bucket_name);
qcloud_cos::HeadBucketResp resp;
qcloud_cos::CosResult result = cos.HeadBucket(req, &resp);
```

**バケットのAvailability Zoneの略称Region**

XML C++ SDKバケットの使用可能な地域の略称が変更されました。初期化の際に、バケットの所在地域略称を構成ファイルの`Region`の中に設定してください。JSON C++ SDKとXML C++ SDKにおけるそれぞれ地域の対応関係は次のグラフを参照してください：

| 地域             | XML C++ SDK地域略称      | JSON C++ SDK地域略称 |
| ---------------- | ---------------- | ----------- |
| 北京1区（華北） | ap-beijing-1     | tj          |
| 北京             | ap-beijing       | bj          |
| 上海（華東）     | ap-shanghai      | sh          |
| 広州（華南）     | ap-guangzhou     | gz          |
| 成都（西南）     | ap-chengdu       | cd          |
| 重慶             | ap-chongqing     | なし          |
| シンガポール           | ap-singapore     | sgp         |
| 香港             | ap-hongkong      | hk          |
| トロント           | na-toronto       | ca          |
| フランクフルト         | eu-frankfurt     | ger         |
| ボンベイ             | ap-mumbai        | なし          |
| ソウル             | ap-seoul         | なし          |
| シリコンバレー             | na-siliconvalley | なし          |
| バージニア州         | na-ashburn       | なし          |
| バンコク             | ap-bangkok       | なし          |
| モスクワ           | eu-moscow        | なし          |

**4. APIの変更

XML C++ SDKにアップグレードした後、一部操作のAPIが変更されました。実際のニーズに合わせて変更してください。SDKを使いやすくするためにAPIをカプセル化しました。詳細については、例と[APIドキュメント](https://cloud.tencent.com/document/product/436/12302)を参照してください。

APIには主に以下の変化があります：

**1）独立のディレクトリAPIがありません**

XML SDKでは、独立のディレクトリAPIを提供しなくなりました。COS自体にはフォルダやディレクトリという概念がなく、COSはオブジェクトproject/a.txtをアップロードする原因で、projectフォルダを作成しません。
ユーザーの使用習慣に合わせるため、オブジェクト保存については、コンソール、COS browserなどの図形化ツールにおいて「フォルダ」または「ディレクトリ」の展示方式をシミュレートしています。詳しくは、キー値が`project/`であり、その内容がブランクであるオブジェクトを作成することで実現しています。展示方式につき、従来型フォルダをシミュレートしています。

例えば：アップロードオブジェクト`project/doc/a.txt `の場合、区切り記号`/`は「フォルダ」の展示方式をシミュレートします。コンソールにおいて「フォルダ」projectとdocが見られ、そのうち、docはprojectの下級「フォルダ」であり、またa.txtファイルを含みます。

したがって、適用シナリオが単にファイルをアップロードするだけの場合は、まずフォルダを作成せずに直接アップロードすることができます。用途がフォルダに関わっている場合、フォルダの作成機能を提供する必要があります。パスが'/'で終わる0KBファイルをアップロードして良いです。これでGetBucket APIを呼び出す時、当該ファイルをフォルダとすることができます。

**2）マルチスレッドのアップロードとダウンロード操作**

XML C++ SDKにおいて、マルチスレッドのマルチパートアップロードとダウンロード操作をカプセル化しています。`MultiUploadObjectReq`と`MultiGetObjectReq`APIです。APIの設計と送信性能を最適化しています。

主要な特性は：

- パートサイズを設定してマルチスレッドのアップロードとダウンロードを行うことができます
- `MultiUploadObjectReq`APIはマルチパートアップロードの全てのAPIをカプセル化しており、Init、Upload、CompleteとAbort操作を含みます。

`MultiUploadObjectReq`によりアップロードするサンプルコード：

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
string bucket_name = "alangz-1253960400";
string object_name = "object_key";
string local_file = "/data/test";
qcloud_cos::MultiUploadObjectReq req(bucket_name,object_name, local_file);
req.SetRecvTimeoutInms(1000 * 60);
qcloud_cos::MultiUploadObjectResp resp;
qcloud_cos::CosResult result = cos.MultiUploadObject(req, &resp);
if (result.IsSucc()) {
    std::cout << "MultiUpload Succ." << std::endl;
    std::cout << resp.GetLocation() << std::endl;
    std::cout << resp.GetKey() << std::endl;
    std::cout << resp.GetBucket() << std::endl;
    std::cout << resp.GetEtag() << std::endl;
} else {
    std::cout << "MultiUpload Fail." << std::endl;
    //具体的にどのステップで失敗したかを取得します
    std::string resp_tag = resp.GetRespTag();
    if ("Init" == resp_tag) {
        // print result
    } else if ("Upload" == resp_tag) {
        // print result
    } else if ("Complete" == resp_tag) {
        // print result
    }
}
```

`MultiGetObjectReq`によりダウンロードするサンプルコード：

```cpp
qcloud_cos::CosConfig config("./config.json");
qcloud_cos::CosAPI cos(config);
string bucket_name = "alangz-1253960400";
string object_name = "object_key";
string file_path = "/data/test";
qcloud_cos::MultiGetObjectReq req(bucket_name,object_name, file_path);
qcloud_cos::MultiGetObjectResp resp;
qcloud_cos::CosResult result = cos.GetObject(req, &resp);
```

**3）署名アルゴリズムの変化**

通常は手動で署名を計算する必要がないが、SDKの署名をフロントエンドに返却して使用する場合、署名アルゴリズムの変化に注意してください。署名につき、単回と複数回署名の区別がなくなり、一方、署名の有効期の設定により安全性を確保するようになります。詳しいアルゴリズムについては、[XML署名のリクエスト](https://intl.cloud.tencent.com/document/product/436/7778)ドキュメントを参照してください。

**4）新しいAPI**

XML C++ SDKの新しいAPIを、必要に応じて呼び出すことができます。それは以下を含みます：

- バケットの操作、例えばPutBucketReq、GetBucketReqなど。
- バケットACLの操作、例えばPutBucketACLReq、GetBucketACLReqなど。
- バケットのライフサイクルの操作、例えばPutBucketLifecycleReq、GetBucketLifecycleReqなど。

詳しくはC++ SDK [APIドキュメント](https://cloud.tencent.com/document/product/436/12302)を参照してください。

