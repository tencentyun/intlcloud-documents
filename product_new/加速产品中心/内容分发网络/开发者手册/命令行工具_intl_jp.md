## 呼び出し前の準備

コマンドラインスクリプトを使ってsectIdとecomkeyを構成してAPIを呼び出す必要があります。テンセントクラウドにログインして移動します。[クラウドAPIキー](https://console.cloud.tencent.com/capi)APIを呼び出す必要のある事務総長と事務局の鍵を見るには、それらの安全を確保してください。
![](//mc.qcloudimg.com/static/img/f449efa9f3904c24894f50376bd406f6/image.png)

## 指令.

命令行はpython scriptです。[ダウンロードする.](https://github.com/zz-mars/CDN_API_DEMO/blob/master/Qcloud_CDN_API/python/QcloudCdnTools_V2.py).

### 使用前準備

上記のpythonスクリプトを使用するには、要求ライブラリをインストールする必要があります。以下のコマンドを使用してください。

```
pip install requests
```

スクリプトを直接実行することができます。現在サポートしているAPIリストはあなたに提供します：
![](https://mc.qcloudimg.com/static/img/813c521d24602315a8ddd18c644f56a6/2.png)

### 照会ドメイン詳細情報

#### すべてのドメインの詳細情報を調べる

以下のコマンドを用いて呼び出す[CdnHostsについて](https://intl.cloud.tencent.com/doc/api/231/3937)APIはappIdの下のすべてのドメインの詳細情報を調べる：

```
python QcloudCdnTools_V2.py DescribeCdnHosts -u xxxxxx -p xxxxxxx
```

##### パラメータ記述

+ -秘書を代表する。
+ -pは事務局鍵を表す。

##### 結果例

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

#### ドメイン調査に基づく詳細情報

以下のコマンドを用いて呼び出す[GetHostInfoByHost](https://intl.cloud.tencent.com/doc/api/231/3938)APIは、指定ドメインの詳細情報を調べる：

```
python QcloudCdnTools_V2.py GetHostInfoByHost -u xxxxx -p xxxxxxx --hosts www.test.com --hosts www.test2.com
```

##### パラメータ記述

+ -秘書を代表する。
+ -pは事務局のキーワードを表します。
+ --hostsはクエリのドメインを表しています。あなたは使用することができます--host一度に複数のドメインを調べることができます。APIパラメータには2つのブレーク番号が必要ですので注意してください。

##### 結果例

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

#### ドメインIDに基づいてドメイン詳細情報を問い合わせる.

以下のコマンドを用いて呼び出す[GetHostInfoById](https://intl.cloud.tencent.com/doc/api/231/3939)APIは、指定されたIDを有するドメインの詳細情報を問い合わせる：

```
python QcloudCdnTools_V2.py GetHostInfoById -u xxxxx -p xxxxxxx --ids 1234
```

##### パラメータ記述

+ -秘書を代表する。
+ -pは事務局のキーワードを表します。
+ --idはクエリのドメインのIDを表しています。a-idを使って複数のドメインを一度に照会することができます。APIパラメータには2つのブレーク番号が必要ですので注意してください。

##### 結果例

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

### 刷新とプリフェッチ

#### 刷新URL

以下のコマンドを用いて呼び出す[CdnUrlを刷新](https://intl.cloud.tencent.com/doc/api/231/3946)指定URLを刷新するためのAPI：

```
python QcloudCdnTools_V2.py RefreshCdnUrl -u xxxxx -p xxxxxxx --urls http://xxxxxxxtang.sp.oa.com/test.php --urls http://www.test.com/1.html
```

##### パラメータ記述

+ -秘書を代表する。
+ -pは事務局のキーワードを表します。
+ --URLは更新するURLを表しています。a-URLを使って複数のURLを一度に検索することができます；
+ URLパラメータの前にhttp：//またはhttps：//プレフィクスを追加しなければなりません；
+ 各ユーザは1日あたり10，000個のURLしか更新できず，更新ごとに最大1，000個のURLの提出が許可されている.

##### 結果例

```json
[
    {
        u'log_id': 220332,
        u'count': 1
    }
]
```

log_idは更新のために提出されたジョブのIDを表します。このIDを使ってジョブの実行状態を問い合わせることができます。countはそのために更新を提出するURLの数を表します。

#### カタログを刷新中である

以下のコマンドを用いて呼び出す[CdnDirを再刷新](https://intl.cloud.tencent.com/doc/api/231/3947)指定ディレクトリを刷新するためのAPI：

```
python QcloudCdnTools_V2.py RefreshCdnDir -u xxxxx -p xxxxxxx --dirs http://www.test.com/abc/
```

##### パラメータ記述

+ -秘書を代表する。
+ -pは事務局のキーワードを表します。
+ --dirsは更新するURLを表しています。a-dirsを使って複数のURLを一度に検索することができます；
+ dirsパラメータの前にhttp：//またはhttps：//プレフィクスを追加しなければなりません；
+ 各ユーザーは1日100ディレクトリしか更新できず、更新ごとに最大20ディレクトリの提出が許可されている。

##### 結果例

```json
request is success.
```

#### 更新結果を照会する

更新結果を以下のコマンドで問い合わせることができる：

```
python QcloudCdnTools_V2.py GetCdnRefreshLog -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-08-15 --endDate 2016-08-16
```

##### パラメータ記述

- -秘書を代表する。
- -pは事務局のキーワードを表します。
- startDateはクエリの開始日であり，endDateはクエリの終了日である.startDateはendDateよりも早くなければならない.

##### 結果例

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

状態は更新作業の状態である.%1は完了したことを示しており，このAPIを用いて更新URLやディレクトリの記録を問い合わせることができる.

### ドメイン配置

#### キャッシュ構成を修正

以下のコマンドを用いて呼び出す[UpdateCache]キャッシュの期限切れ時間構成を修正するためのAPI：

```
python QcloudCdnTools_V2.py UpdateCache -u xxxxx -p xxxxxxx --hostId 1234 --cache [[0,\"all\",1000],[1,\".jpg;.js\",2000],[2,\"/www/html\",3000],[3,\"/index.html;/test/*.jpg\",3000]]
```

##### パラメータ記述

+ -秘書を代表する。
+ -pは事務局のキーワードを表します。
+ hostIdは，キャッシュの期限切れ配置を修正しようとするドメインのIDである；
+ キャッシュはターゲットキャッシュの構成です。注意してください。ダブルリード番号を変更する必要があります。

**キャッシュ期限切れ配置**
1つのドメインのキャッシュの期限切れ構成は、複数のキャッシュの期限切れプロファイルから構成され、各エントリは、キャッシュタイプ、マッチングルール、構成の期限切れ時間(秒単位)の3つのパラメータに分けられる。CDNは、3つのタイプを提供する：

+ 0：すべてのタイプ。これはすべてのファイルが一致していることを意味する。これはデフォルトのキャッシュ配置である。
+ 1：ファイルタイプ。これは、ファイル拡張子に基づいてマッチングを行うことを意味する。例えば：.jpg；.png；
+ 2：フォルダタイプ。これはディレクトリに基づいてマッチングを行うことを意味する。例えば：/abc；/def；

##### 結果例

```json
request is success.
```

#### ドメインの修正項目

以下のコマンドを用いて呼び出す[UpdateCdnProject](https://intl.cloud.tencent.com/doc/api/231/3935)ドメインの所属項目を修正するためのAPI：

```
python QcloudCdnTools_V2.py UpdateCdnProject -u xxxxx -p xxxxxxx --hostId 1234 --projectId 0
```

ドメインの項目を修正する際には、項目のIDを知る必要があります。移動してください[項目管理](https://console.cloud.tencent.com/project)チェック項目ID.デフォルト項目のIDは0.

##### パラメータ記述

+ -秘書を代表する。
+ -pは事務局のキーワードを表します。
+ hostIdはその項目を修正するドメインのIDである；
+ projectIdは目標項目IDである.

##### 結果例

```json
request is success.
```

#### 修正域配置

以下のコマンドを用いて呼び出す[UpdateCdnConfig]APIは、キャッシュの期限切れ構成、ホットリンク保護、ホストソース、全パスキャッシュなどのドメイン構成を修正するために使用される：

```
python QcloudCdnTools_V2.py UpdateCdnConfig -u xxxxx -p xxxxxxx --hostId 1234 --projectId 0 --cacheMode custom --cache [[0,\"all\",1023448]] --refer [1,[\"www.baidu.com\",\"www.qq.com\"]] --fwdHost www.test.org --fullUrl off
```

##### パラメータ記述

+ -秘書を代表する。
+ -pは事務局のキーワードを表します。
+ hostIdはその構成を修正しようとするドメインのID；
+ projectIdは修正すべき項目のID；
+ cacheModeは、上位キャッシュ構成を有効にするか否かを指定する；
+ キャッシュはキャッシュの期限切れ構成です。UpdateCache上の説明を参照してください；
+ 参考にするのは熱リンク保護構成、
+ fwdHostはシンクソース構成；
+ FullUrlは全パスキャッシュを有効にするかどうかを指定する。全パスキャッシュを有効にすることは禁止パラメータのスクリーニングを意味する；

**ホットリンク保護構成説明書**
ホットリンク保護は、2つのフィールドから構成される。第1のフィールドは、参照のタイプを指定する：

+ 0：ホットリンク保護を配置しない；
+ 1：ブラックリスト配置
+ 2：ホワイトリストを配置する。

第2のフィールドは、特定の名前リストである。

##### 結果例

```json
request is success.
```

##### ドメイン管理

#### 添加域

以下のコマンドを用いて呼び出す[AddCdnHost](https://intl.cloud.tencent.com/doc/api/231/1406)CDN加速ドメインのAPIを追加：

```
python QcloudCdnTools_V2.py AddCdnHost -u xxxxx -p xxxxxxx --host www.test.com --projectId 0 --hostType cname --origin 1.1.1.1
```

##### パラメータ記述

+ -秘書を代表する。
+ -pは事務局のキーワードを表します。
+ ホストは追加する加速ドメインを代表しています。このドメインは工信部が記録しなければならず、以前は騰訊雲CDNに接続されていませんでした。
+ projectIdは、その中にドメインの項目を付加するIDです。中で項目IDをチェックすることができます。[項目管理](https://console.cloud.tencent.com/project)
+ hostTypeは接続方法であり，“cname”は自分のソースを，“ftp”はFTPソースを表す(この場合，ソースサーバパラメータは無視される).
+ 原点はオリジナルサーバの構成。

##### 結果例

```
request is success.
```

#### ドメインをオフラインにする

以下のコマンドを用いて呼び出す[オフラインホスト](https://intl.cloud.tencent.com/doc/api/231/1403)指定ドメインのCDN加速サービスを停止するためのAPI：

```
python QcloudCdnTools_V2.py OfflineHost -u xxxxx -p xxxxxxx --hostId 1234
```

##### パラメータ記述

+ -秘書を代表する。
+ -pは事務局のキーワードを表します。
+ 状態が「アクティブ」であるフィールドに対しては，Offline命令を呼び出すことに成功するしかない.
+ hostIdはオフラインになるドメインのIDです。GetHostInfoByHostを使ってドメインIDを取得することができます。

##### 結果例

```json
request is success.
```

#### オンライン生成ドメイン

以下のコマンドを用いて呼び出す[オンラインホスト](https://intl.cloud.tencent.com/doc/api/231/1402)指定ドメインのCDN加速サービスを活性化するためのAPI：

```
python QcloudCdnTools_V2.py OnlineHost -u xxxxx -p xxxxxxx --hostId 1234
```

##### パラメータ記述：

- -秘書を代表する。
- -pは事務局のキーワードを表します。
- 状態が「閉じる」フィールドだけが「オンライン」命令を呼び出すことに成功する.
- hostIdはオフラインになるドメインのIDです。GetHostInfoByHostを使ってドメインIDを取得することができます。

##### 結果例

```json
request is success.
```

#### 削除域

以下のコマンドを用いて呼び出す[DeleteCdnHost](https://intl.cloud.tencent.com/doc/api/231/1396)指定ドメインのAPIを削除する：

```
python QcloudCdnTools_V2.py DeleteCdnHost -u xxxxx -p xxxxxx -hostId 1234
```

##### パラメータ記述：

- -秘書を代表する。
- -pは事務局のキーワードを表します。
- 削除コマンドは、状態が「閉じる」状態のフィールドを呼び出すことに成功することしかできません；
- hostIdはオフラインになるドメインのIDです。GetHostInfoByHostを使ってドメインIDを取得することができます。

### 原木

#### ログ取得ダウンロードリンク

指定ドメインのCDNログを取得するために、以下のコマンドを使用してGenerateLogList APIを呼び出し、リンクをダウンロードする：

```
python QcloudCdnTools_V2.py GenerateLogList -u xxxxx -p xxxxxxx --hostId 1234
```

##### パラメータ記述

- -秘書を代表する。
- -pは事務局のキーワードを表します。
- hostIdは，そのログがリンクをダウンロードしたドメインのIDを調べることである；
- 30日間の毎日ログのダウンロードリンクを獲得します。

##### 結果例

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

リンクフィールドがない場合は，当日ログデータが生成されていないことを示す.

### 消費データを照会する

#### クエリ上位100個のURL

以下のコマンドを用いて呼び出す[GetCdnStatTop]API問合せトラフィック/帯域消費が最も高いドメインまたはプロジェクトの上位100個のURL：

```
python QcloudCdnTools_V2.py GetCdnStatTop -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-08-15 --endDate 2016-08-15 --statType bandwidth --projects 0 --hosts test.com
```

##### パラメータ記述

- -秘書を代表する。
- -pは事務局のキーワードを表します。
- StartDateはクエリの開始時間である.たとえば，8/15/2016は問合せの実際の開始時間が8/15/2016 00：00：00であることを示している.
- endDateはクエリの終了時間であり、例えば、8/15/2016はクエリの実際の終了時間が8/15/2016 23：55：00であることを示している；
- Projectsはチェックすべき項目のIDです。複数のIDを入力することができます；
- ホストはクエリのドメインです。そのドメインの属する項目にパラメータを渡さなければなりません。そうでないとエラーになります。
- statTypeは整列化方法であり，帯域は消費する帯域，流量はトラヒックである.

##### 結果例

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

値は消耗値である.トラヒックと帯域の測定単位はそれぞれByteとbpsである.

#### クエリ状態コード統計情報

以下のコマンドを用いて呼び出す[GetCdnStatusCode]ドメインやプロジェクトの状態コードの統計情報を問い合わせるためのAPI：

```
python QcloudCdnTools_V2.py GetCdnStatusCode -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-08-15 --endDate 2016-08-15 --projects 0 --hosts test.com
```

##### パラメータ記述

- -秘書を代表する。
- -pは事務局のキーワードを表します。
- StartDateはクエリの開始時間である.たとえば，8/15/2016は問合せの実際の開始時間が8/15/2016 00：00：00であることを示している.
- endDateはクエリの終了時間であり、例えば、8/15/2016はクエリの実際の終了時間が8/15/2016 23：55：00であることを示している；
- Projectsはチェックすべき項目のIDです。複数のIDを入力することができます；
- Hostsはクエリのドメインです。そのドメインの属する項目にパラメータ(項目)を渡さなければなりません。そうでないとエラーになります。複数のドメインを入力することができます。

##### 結果例

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

#### 詳細消費統計データを調べる

以下のコマンドを用いて呼び出す[DescribeCdnHostDetailedInfo]APIはドメインやプロジェクトを参照するための詳細な消費統計情報：

```
python QcloudCdnTools_V2.py DescribeCdnHostDetailedInfo -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-05-08 --endDate 2016-08-15 --projects 0 --hosts www.test.com --statType bandwidth
```

##### パラメータ記述

- -秘書を代表する。
- -pは事務局のキーワードを表します。
- StartDateはクエリの開始時間である.たとえば，8/15/2016は問合せの実際の開始時間が8/15/2016 00：00：00であることを示している.
- endDateはクエリの終了時間であり、例えば、8/15/2016はクエリの実際の終了時間が8/15/2016 23：55：00であることを示している；
- Projectsはチェックすべき項目のIDです。複数のIDを入力することができます；
- ホストはクエリのドメインです。そのドメインに属する項目にパラメータ(項目)を伝達しなければなりません。そうでないとエラーになります。複数のドメインを入力することができます。
- statTypeは問合せのための消費タイプであり，トラヒックはトラヒック(バイト単位)であり，帯域は消費する帯域(bps単位)である.

##### 結果例

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

期間は時間粒度であり，問合せ時間範囲によって異なり，1日から3日までの問合せ時間範囲は5分，4日から7日の時間範囲は1時間，8日以上の時間範囲は1日である.

#### 照会消費統計

以下のコマンドを用いて呼び出す[DescribeCdnHostInfo]APIはドメインやプロジェクトを参照するための消費統計情報：

```
python QcloudCdnTools_V2.py DescribeCdnHostInfo -u xxxxxxxxxxxx -p xxxxxxxxxxxx --startDate 2016-08-15 --endDate 2016-08-15 --projects 0 --hosts www.test.com --statType bandwidth
```

##### パラメータ記述

- -秘書を代表する。
- -pは事務局のキーワードを表します。
- StartDateはクエリの開始時間である.たとえば，8/15/2016は問合せの実際の開始時間が8/15/2016 00：00：00であることを示している.
- endDateはクエリの終了時間であり、例えば、8/15/2016はクエリの実際の終了時間が8/15/2016 23：55：00であることを示している；
- Projectsはチェックすべき項目のIDです。複数のIDを入力することができます；
- ホストはクエリのドメインです。そのドメインに属する項目にパラメータ(項目)を伝達しなければなりません。そうでないとエラーになります。複数のドメインを入力することができます。
- statTypeは問合せのための消費タイプであり，トラヒックはトラヒック(バイト単位)であり，帯域は消費する帯域(bps単位)である.

##### 結果例

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

問合せの結果，指定された時間範囲内の総消費を示す.HOST_TYPEは接続ドメインのタイプ，cnameはソース，ftpはFTPの原点，cosはCOSの原点を表す.