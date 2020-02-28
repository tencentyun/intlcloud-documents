## 呼び出しの準備

コマンドラインスクリプトを使用してAPIを呼び出すには、SecretIdとSecretKeyを構成する必要があります。Tencent Cloudにログインし、【TencentCloud API】(https://console.cloud.tencent.com/capi)に入ると、APIの呼び出しに必要なSecretIdとSecretKeyを確認できます。キーを大切に保管してください。
![](//mc.qcloudimg.com/static/img/f449efa9f3904c24894f50376bd406f6/image.png)



## 使用の説明

コマンドラインがPythonスクリプトで、【ダウンロードに進む】(https://github.com/zz-mars/CDN_API_DEMO/tree/master/Qcloud_CDN_API/python)。

### 使用の準備

上記のPythonスクリプトを使用する場合、requests ライブラリをインストールする必要があります。次のコマンドを使用できます。

```
pip install requests
```

スクリプトを直接実行でき、現在サポートされているインターフェースのリストが表示されます。
![](https://mc.qcloudimg.com/static/img/813c521d24602315a8ddd18c644f56a6/2.png)
インターフェース機能の説明については、【API概要】(<https://intl.cloud.tencent.com/document/api/228/31719>)を参照してください。

### ドメイン名詳細のクエリー

#### すべてのドメイン名詳細のクエリー

1. 次のコマンドを使用して、[DescribeCdnHosts](<https://intl.cloud.tencent.com/document/product/228/3937>) インターフェースを呼び出して、APPID 配下のすべてのドメイン名詳細情報をクエリーできます。

```
python QcloudCdnTools_V2.py DescribeCdnHosts -u xxxxxx -p xxxxxxx
```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。

3. 結果の例

```josn
{
    u'total': 1,
    u'hosts': [
        {
            u'origin': u'8.8.8.8',
            u'enable_overseas': u'no',
            u'disabled': 0,
            u'create_time': u'2016-07-2610: 34: 09',
            u'seo': u'off',
            u'message': u'\u90e8\u7f72\u4e2d',
            u'id': 279950,
            u'cache': [
                {
                    u'type': 0,
                    u'unit': u'd',
                    u'rule': u'all',
                    u'time': 2592000
                },
                {
                    u'type': 1,
                    u'unit': u's',
                    u'rule': u'.php;.jsp;.asp;.aspx',
                    u'time': 0
                }
            ],
            u'middle_resource': -1,
            u'fwd_host_type': u'default',
            u'readonly': 0,
            u'fwd_host': u'www.test.com',
            u'service_type': u'media',
            u'project_id': 0,
            u'refer': {
                u'list': [                  
                ],
                u'type': 0,
                u'null_flag': 0
            },
            u'status': 4,
            u'update_time': u'2016-08-1220: 36: 58',
            u'ssl_expire_time': None,
            u'deleted': u'no',
            u'ssl_type': 0,
            u'ssl_deploy_time': None,
            u'app_id': 1251991073,
            u'host': u'www.test.com',
            u'bucket_name': u'',
            u'host_id': 279950,
            u'pid_config': None,
            u'cache_mode': u'simple',
            u'furl_cache': u'on',
            u'host_type': u'cname',
            u'owner_uin': 78976504,
            u'cname': u'www.test.com.cdn.dnsv1.com'
        }
        ...
    ]
}
```

#### ドメイン名によるドメイン名詳細のクエリー

1. 次のコマンドを使用して、[GetHostInfoByHost](<https://intl.cloud.tencent.com/document/product/228/3938>) インターフェースを呼び出して、指定されたドメイン名に対応する詳細をクエリーできます。

```
python QcloudCdnTools_V2.py GetHostInfoByHost -u xxxxx -p xxxxxxx --hosts www.test.com --hosts www.test2.com
```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- --hosts はクエリーするドメイン名を示します。一度に複数件をクエリーできます、いずれも--hostsを使用します。インターフェースパラメータには2本の横線が必要です。

3. 結果の例

```json
{
    u'total': 2,
    u'hosts': [
        {
            u'origin': u'8.8.8.8',
            u'enable_overseas': u'no',
            u'disabled': 0,
            u'create_time': u'2016-07-2610: 34: 09',
            u'seo': u'off',
            u'message': u'\u5df2\u5f00\u542f',
            u'id': 1234,
            u'cache': [
                {
                    u'type': 0,
                    u'unit': u'd',
                    u'rule': u'all',
                    u'time': 2592000
                },
                {
                    u'type': 1,
                    u'unit': u's',
                    u'rule': u'.php;.jsp;.asp;.aspx',
                    u'time': 0
                }
            ],
            u'middle_resource': -1,
            u'fwd_host_type': u'default',
            u'readonly': 0,
            u'fwd_host': u'www.test.com',
            u'service_type': u'media',
            u'project_id': 0,
            u'refer': {
                u'list': [                 
                ],
                u'type': 0,
                u'null_flag': 0
            },
            u'status': 5,
            u'update_time': u'2016-08-1220: 36: 58',
            u'ssl_expire_time': None,
            u'deleted': u'no',
            u'ssl_type': 0,
            u'ssl_deploy_time': None,
            u'app_id': 1251991073,
            u'host': u'www.test.com',
            u'bucket_name': u'',
            u'host_id': 279950,
            u'pid_config': None,
            u'cache_mode': u'simple',
            u'furl_cache': u'on',
            u'host_type': u'cname',
            u'owner_uin': 78976504,
            u'cname': u'www.test.com.cdn.dnsv1.com'
        },
        ...
    ]
}
```

#### ドメイン名 IDに基づくドメイン名詳細のクエリー

1. 次のコマンドを使用して、[GetHostInfoById](<https://intl.cloud.tencent.com/document/product/228/3939>) インターフェースを呼び出して、IDに対応するドメイン名詳細をクエリーできます。

```
python QcloudCdnTools_V2.py GetHostInfoById -u xxxxx -p xxxxxxx --ids 1234
```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- --ids は、クエリーするドメイン名のIDを示します。複数のIDを一度にクエリーできます、いずれも--idsを使用します。インターフェースパラメータには2本の横線が必要です。

3. 結果の例

```json
{
    u'total': 1,
    u'hosts': [
        {
            u'origin': u'8.8.8.8',
            u'enable_overseas': u'no',
            u'disabled': 0,
            u'create_time': u'2016-07-2610: 34: 09',
            u'seo': u'off',
            u'message': u'\u5df2\u5f00\u542f',
            u'id': 1234,
            u'cache': [
                {
                    u'type': 0,
                    u'unit': u'd',
                    u'rule': u'all',
                    u'time': 2592000
                },
                {
                    u'type': 1,
                    u'unit': u's',
                    u'rule': u'.php;.jsp;.asp;.aspx',
                    u'time': 0
                }
            ],
            u'middle_resource': -1,
            u'fwd_host_type': u'default',
            u'readonly': 0,
            u'fwd_host': u'www.test.com',
            u'service_type': u'media',
            u'project_id': 0,
            u'refer': {
                u'list': [                 
                ],
                u'type': 0,
                u'null_flag': 0
            },
            u'status': 5,
            u'update_time': u'2016-08-1220: 36: 58',
            u'ssl_expire_time': None,
            u'deleted': u'no',
            u'ssl_type': 0,
            u'ssl_deploy_time': None,
            u'app_id': 1251991073,
            u'host': u'www.test.com',
            u'bucket_name': u'',
            u'host_id': 279950,
            u'pid_config': None,
            u'cache_mode': u'simple',
            u'furl_cache': u'on',
            u'host_type': u'cname',
            u'owner_uin': 78976504,
            u'cname': u'www.test.com.cdn.dnsv1.com'
        }
    ]
}
```

### 更新予熱

#### URL更新

1. 次のコマンドを使用して、[RefreshCdnUrl](<https://intl.cloud.tencent.com/document/product/228/3946>) インターフェースを呼び出して、指定されたURLを更新できます。

```
python QcloudCdnTools_V2.py RefreshCdnUrl -u xxxxx -p xxxxxxx --urls http://xxxxxxxtang.sp.oa.com/test.php --urls http://www.test.com/1.html
```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- --urls は、更新するURLを示します。一度に複数件をクエリーでき、いずれも--urlsを使用します。
- urls パラメータの前にhttp：//またはhttps：//のプレフィックスを追加する必要があります。
- 各ユーザーは1日に更新できるURLは10,000件までで、一度にサブミットできる更新は1000件までです。

3. 結果の例

```json
[
    {
        u'log_id': 220332,
        u'count': 1
    }
]

```

log_idはサブミットする更新タスクのIDであり、このIDに基づいて対象更新タスクの実行状態をクエリーできます。countは今回サブミットするURL更新の件数です。

#### ディレクトリの更新

1. 次のコマンドを使用して、[RefreshCdnDir](<https://intl.cloud.tencent.com/document/product/228/3947>) インターフェースを呼び出して、指定されたディレクトリを更新できます。

```
python QcloudCdnTools_V2.py RefreshCdnDir -u xxxxx -p xxxxxxx --dirs http://www.test.com/abc/

```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- --dirs は、更新するURLを示します。一度に複数件のURLをクエリーでき、いずれも--dirsを使用します。
- dirs パラメータの前にhttp：//またはhttps：//のプレフィックスを追加する必要があります。
- 各ユーザーは1日に更新できるディレクトリは100件までで、一度にサブミットできる更新は20件までです。

3. 結果の例

```json
request is success.

```

#### 更新履歴のクエリー

1. 1.次のコマンドを使用して、更新履歴をクエリーできます。

```
python QcloudCdnTools_V2.py GetCdnRefreshLog -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-08-15 --endDate 2016-08-16

```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- startDate はクエリーの開始日であり、endDateはクエリー終了日です。startDateはendDateよりも小さい必要があります。

3. 結果の例

```json
{
    u'total': 2,
    u'logs': [
        {
            u'status': 1,
            u'complete_time': u'2016-08-1510: 39: 16',
            u'url_list': [
                u'http: //www.test.org/1.html'
            ],
            u'app_id': 1251991073,
            u'datetime': u'2016-08-1510: 39: 14',
            u'host': u'www.test.org',
            u'project_id': 0,
            u'type': 0,
            u'id': 1234
        },
		...
	]
}

```

statusが更新状態であり、1 が更新完了を示します。URL更新、ディレクトリ更新の履歴はすべてこのインターフェースを介してクエリーできます。

### ドメイン名の構成

#### キャッシュ構成の変更

1. 次のコマンドを使用して、[UpdateCache] インターフェースを呼び出して、キャッシュの期限切れ設定を変更できます。

```
python QcloudCdnTools_V2.py UpdateCache -u xxxxx -p xxxxxxx --hostId 1234 --cache [[0,\"all\",1000],[1,\".jpg;.js\",2000],[2,\"/www/html\",3000]]

```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- hostIdは、キャッシュの期限切れ構成の変更が必要なドメイン名IDです。
- cache cacheはターゲットキャッシュの構成です。二重引用符はエスケープする必要があることに注意してください。

 **キャッシュ期限切れの設定**
ドメイン名のキャッシュ期限切れ構成は、複数件のキャッシュ期限切れ設定で構成されます。各キャッシュ期限切れ設定に、3つのパラメータがあります。1つ目はキャッシュタイプ、2つ目はマッチングルール、3つ目は設定された期限切れ時間で、単位が秒です。CDNには次の3つのタイプがあります。

- 0：すべてのタイプ。マッチングするすべてのファイルは、デフォルトのキャッシュ構成となることを示します。
- 1：ファイルタイプ。ファイルのサフィックスにマッチングすることを示します。マッチング例： .jpg;.png。
- 2：フォルダタイプ。ディレクトリによるマッチングを示します。マッチング例：/abc;/def。

3. 結果の例

```json
request is success.

```

#### ドメインが属するプロジェクトの変更

1. 次のコマンドを使用して、[UpdateCdnProject]インターフェースを呼び出して、ドメイン名が属するプロジェクトを変更できます。

```
python QcloudCdnTools_V2.py UpdateCdnProject -u xxxxx -p xxxxxxx --hostId 1234 --projectId 0

```

ドメイン名が属するプロジェクトを変更するときは、プロジェクトに対応するIDを知る必要があります。【プロジェクト管理】(https://console.cloud.tencent.com/project) で確認できます。デフォルトのプロジェクトIDが0です。

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- hostId は、変更するプロジェクトのドメイン名に対応するIDを表します。
- projectId は、ターゲットプロジェクトのIDです。

3. 結果の例

```json
request is success.

```

#### ドメイン名構成の変更

1. 次のコマンドを使用して、[UpdateCdnConfig] インターフェースを呼び出して、キャッシュ期限切れの設定、防犯リンク、back to origin HOST、フルパスキャッシュなどを含むドメイン名構成を変更します。

```
python QcloudCdnTools_V2.py UpdateCdnConfig -u xxxxx -p xxxxxxx --hostId 1234 --projectId 0 --cacheMode custom --cache [[0,\"all\",1023448]] --refer [1,[\"www.baidu.com\",\"www.qq.com\"]] --fwdHost www.test.org --fullUrl off

```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- hostId は構成を変更するドメイン名のIDを示します。
- projectIdは、変更するプロジェクトIDを示します。
- cacheMode は高度なキャッシュ設定を有効にするか否かを示します。
- cache はキャッシュの期限切れ設定を示します。UpdateCacheの説明を参照してください。
- refer は、防犯リンク設定を示します。
- fwdHost はback to origin Host設定を示します。
- fullUrl は、フルパスキャッシュが有効になっているかどうかを示し、フルパスキャッシュが有効になっている場合、フィルターパラメータスイッチはオフになり、フルパスキャッシュが有効になっていない場合、フィルターパラメータスイッチはオンになります。

 **防犯リンク設定の説明**
防犯リンクは2つのフィールドで構成され、最初のフィールドは refer のタイプを識別します。

- 0：防犯リンクを設定しない。
- 1：ブラックリストを設定する。
- 2：ホワイトリストを設定する。

 2番目のフィールドは特定のリストです。

3. 結果の例

```json
request is success.

```

### ドメイン名管理

#### ドメイン名の追加

1. 次のコマンドを使用して、[AddCdnHost]インターフェースを呼び出して、CDN加速ドメイン名を追加できます。

```
python QcloudCdnTools_V2.py AddCdnHost -u xxxxx -p xxxxxxx --host www.test.com --projectId 0 --hostType cname --origin 1.1.1.1

```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- host は追加する加速ドメイン名を示します。ドメイン名は、中国工業情報化部にICP申告する必要があり、またTencent Cloud CDNにアクセスしたことがない前提です。
- projecctId はドメイン名の追加先プロジェクトIDを示します【プロジェクト管理】（https://console.cloud.tencent.com/project）に入って、プロジェクトに対応するIDを表示できます。
- hostType はアクセスタイプで、「cname」の場合はユーザー保有オリジンアクセスを意味し、「ftp」の場合はFTPオリジンアクセスを意味します、この場合オリジンサーバーパラメータが無視されます。
- origin はオリジンサーバーの構成を示します。

3. 結果の例

```
request is success.

```

#### ドメイン名のオフライン化

1. 次のコマンドを使用して、[OfflineHost] インターフェースを呼び出して、指定されたドメイン名のCDN加速サービスを無効化できます。

```
python QcloudCdnTools_V2.py OfflineHost -u xxxxx -p xxxxxxx --hostId 1234

```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- 「オン」状態のドメイン名のみは、オフラインコマンドを正常に呼び出せます。
- hostId は、オフラインにするドメイン名のIDを示します。GetHostInfoByHostを使用して、ドメイン名に対応するIDを取得できます。

3. 結果の例

```json
request is success.

```

#### ドメイン名のオンライン化

1. 次のコマンドを使用して、[OnlineHost]インターフェースを呼び出して、指定されたドメイン名のCDN加速サービスを有効化できます

```
python QcloudCdnTools_V2.py OnlineHost -u xxxxx -p xxxxxxx --hostId 1234

```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- 「オフ」状態のドメイン名のみがオンラインコマンドを正常に呼び出すことができます。
- hostId は、オフラインにするドメイン名のIDを示しますGetHostInfoByHostを使用して、ドメイン名に対応するIDを取得できます。

3. 結果の例

```json
request is success.

```

#### ドメイン名の削除

1. 次のコマンドを使用して、[DeleteCdnHost] インターフェースを呼び出して、指定されたドメイン名を削除できます。

```
python QcloudCdnTools_V2.py DeleteCdnHost -u xxxxx -p xxxxxx -hostId 1234

```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- 「オフ」状態のドメイン名のみが削除コマンドを呼び出せます。
- hostId は、オフラインにするドメイン名のIDを示します。GetHostInfoByHostを使用して、ドメイン名に対応するIDを取得できます。

### ログ関連

#### ログダウンロードリンクの取得

1. 次のコマンドを使用して、[GenerateLogList]インターフェースを呼び出して、指定されたドメイン名の CDN ログダウンロードリンクを取得できます。

```
python QcloudCdnTools_V2.py GenerateLogList -u xxxxx -p xxxxxxx --hostId 1234

```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- hostId はクエリーするログダウンロードリンクのドメイン名IDです。
- 最近30日以内の毎日のログダウンロードリンクを取得します。

3. 結果の例

```json
{
    u'now': 1471267882,
    u'list': [
        {
            u'date': u'2016-07-16',
            u'type': 0,
            u'name': u'20160716-test.com'
        },
        {
            u'date': u'2016-07-17',
            u'link': u'http: //log-download.cdn.qcloud.com/20160717/20160717-test.com.gz?st=xYeU1vW6N9UJlSc3hxM0lg&e=1472131882',
            u'type': 1,
            u'name': u'20160717-test.com'
        },
		...
	]
}

```

linkフィールドがない場合は、その日にログデータが生成されなかったことを示します。

 

### 消費のクエリー

#### TOP 100 URLのクエリー 

1. 次のコマンドを使用して、[GetCdnStatTop]インターフェースを呼び出して、ドメイン名またはプロジェクトのTOP 100のトラフィック/帯域幅消費URLをクエリーできます。

```
python QcloudCdnTools_V2.py GetCdnStatTop -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-08-15 --endDate 2016-08-15 --statType bandwidth --projects 0 --hosts test.com

```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- startDate はクエリーの開始時間を示します。2016-08-15に設定されている場合、クエリーの実際の開始時間は2016-08-15 00:00:00です。
- endDate はクエリーの終了時間を示します。2016-08-15に設定されている場合、クエリーの実際の終了時間は2016-08-15 23:55:00です。
- projects はクエリーするプロジェクトIDを示し、複数件をサポートします。
- hosts はクエリーするドメイン名を示します。ドメイン名が属するプロジェクトは、パラメータを渡す必要があります。そうしないと、エラーが発生します。複数件をサポートします。
- statTypeはランキングの根拠であり、bandwidth が帯域幅、flux がトラフィックを示します。

3. 結果の例

```json
{
    u'start_datetime': u'2016-08-15',
    u'url_data': [
        {
            u'name': u'test.com/uploads/20141218/1418891322.jpeg',
            u'value': 877
        },
        {
            u'name': u'test.com/uploads/20141218/1418891825.jpeg',
            u'value': 796
        },
        {
            u'name': u'test.com/uploads/20141218/1418896965.jpeg',
            u'value': 706
        },
		...
	]
}

```

value は消費値です。fluxの単位はByte、bandwidthの単位はbpsです。

#### ステータスコード統計のクエリー

1. 次のコマンドを使用して、[GetCdnStatusCode] インターフェースを呼び出して、ドメイン名やプロジェクトの ステータスコード統計をクエリーできます。

```
python QcloudCdnTools_V2.py GetCdnStatusCode -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-08-15 --endDate 2016-08-15 --projects 0 --hosts test.com

```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- startDate はクエリーの開始時間を示します。2016-08-15に設定されている場合、クエリーの実際の開始時間は2016-08-15 00:00:00です。
- endDate はクエリーの終了時間を示します。2016-08-15に設定されている場合、クエリーの実際の終了時間は2016-08-15 23:55:00です。
- projects はクエリーのプロジェクトIDを示し、複数件をサポートします。
- hostsはクエリーするドメイン名を示します。ドメイン名が属するプロジェクトは、パラメータ（projects）を渡す必要があります。そうしないと、エラーが発生します。複数件をサポートします。

3. 結果の例

```json
[
    {
        u'200': [
            
        ],
        u'206': [
            
        ],
        u'304': [
            
        ],
        u'416': [
            
        ],
        u'404': [
            69,
			69,
            76,
            69,
            66,
            78,
            73,
            71,
            73,
            76,
      		...
     	],
      	u'500':[
          
      	]
    }
]

```



#### 消費統計明細のクエリー

1. 次のコマンドを使用して、[DescribeCdnHostDetailedInfo]インターフェースを呼び出して、ドメイン名またはプロジェクトの消費の詳細をクエリーできます。

```
python QcloudCdnTools_V2.py DescribeCdnHostDetailedInfo -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-05-08 --endDate 2016-08-15 --projects 0 --hosts www.test.com --statType bandwidth

```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- startDate はクエリーの開始時間を示します。2016-08-15に設定されている場合、クエリーの実際の開始時間は2016-08-15 00:00:00です。
- endDate はクエリーの終了時間を示します。2016-08-15に設定されている場合、クエリーの実際の終了時間は2016-08-15 23:55:00です。
- projects はクエリーするプロジェクトIDを示し、複数件をサポートします。
- hostsは、クエリーするドメイン名を示します。ドメイン名が属するプロジェクトは、パラメータ（projects）を渡す必要があります。そうしないと、エラーが発生します。複数件をサポートします。
- statType は指定されたクエリーの消費タイプです。fluxはトラフィックで、単位がByteです。bandwidthは帯域幅で、単位がbpsです。

3. 結果の例

```json
{
    u'start_datetime': u'2016-08-1300: 00: 00',
    u'total_data': [
        35216,
        41875,
        42256,
        34333,
        40868,
        40906,
        38505,
        39487,
        39407,
  		...
  	],
    u'stat_type': u'flux',
    u'end_datetime': u'2016-08-1523: 55: 00',
    u'period': 5
}

```

period は時間の粒度であり、クエリーする時間の期間によって異なり、返された時間粒度も異なります。 1〜3日の明細の時間粒度は5分で、4〜7日の粒度は1時間で、8日以上の時間粒度は1日です。

#### 消費量統計のクエリー

1. 次のコマンドを使用して、[DescribeCdnHostInfo]インターフェースを呼び出して、ドメイン名またはプロジェクトの消費統計をクエリーできます。

```
python QcloudCdnTools_V2.py DescribeCdnHostInfo -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-08-15 --endDate 2016-08-15 --projects 0 --hosts www.test.com --statType bandwidth

```

2. パラメータの説明

- -u はSecretIdを示します。
- -p はSecretKeyを示します。
- startDate はクエリーの開始時間を示します。2016-08-15に設定されている場合、クエリーの実際の開始時間は2016-08-15 00:00:00です。
- endDate はクエリーの終了時間を示します。2016-08-15に設定されている場合、クエリーの実際の終了時間は2016-08-15 23:55:00です。
- projects はクエリーするプロジェクトIDを示し、複数件をサポートします。
- hosts はクエリーするドメイン名を示します。ドメイン名が属するプロジェクトは、パラメータ（projects）を渡す必要があります。そうしないと、エラーが発生します。複数件をサポートします。
- statType は指定されたクエリーの消費タイプです。fluxはトラフィックで、単位がByteです。bandwidthは帯域幅で、単位がbpsです。

3. 結果の例

```json
{
    u'start_datetime': u'2016-08-1300: 00: 00',
    u'stat_type': u'bandwidth',
    u'end_datetime': u'2016-08-1523: 55: 00',
    u'detail_data': [
        {
            u'host_id': u'www.test.com',
            u'host_type': u'cname',
            u'host_name': u'www.test.com',
            u'host_value': 2214
        }
    ],
    u'period': 5
}

```

クエリー結果は指定された時間期間の合計量、host_typeはドメイン名にアクセスするときのタイプです。cnameはユーザー保有オリジンアクセスを示し、ftpはFTPオリジンアクセスを示し、cosはCOSオリジンアクセスを示します。

