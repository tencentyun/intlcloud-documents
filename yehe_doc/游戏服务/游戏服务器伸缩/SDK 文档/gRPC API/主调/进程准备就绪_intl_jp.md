

#### インターフェースの説明
このインターフェース（ProcessReady）は、サービスの準備完了を通知し、同期メソッドとして使用します。これによりコールバック関数、ポート、ログディレクトリを登録することができます。 
GSEサーバーが受信すると、サーバーインスタンスのステータスがACTIVEに変わり、コールバック関数を登録済みの場合は、1分間に1回onHealthCheckを呼び出します。onHealthCheckが1分以内に戻ってくれば有効です。

#### パラメータの説明

<table>
<thead>
<tr>
<th align="left">パラメータ名</th>
<th>タイプ/値</th>
<th>説明</th>
</tr>
</thead>
<tbody><tr>
<td align="left">onStartGameServerSession</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/1055/37426">std::function &lt;void(tencentcloud::gse::model::gameserversession)&gt; onStartGameServerSession</a></td>
<td>ゲームセッション作成後のコールバック関数</td>
</tr>
<tr>
<td align="left">onProcessTerminate</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/1055/37426">std::function&lt;void()&gt;onProcessTerminate</a></td>
<td>プロセス終了リクエストの通知</td>
</tr>
<tr>
<td align="left">onHealthCheck</td>
<td><a href="https://intl.cloud.tencent.com/zh/document/product/1055/37426">std::function&lt;bool()&gt; onHealthCheck</a></td>
<td>定時ヘルスチェック関数</td>
</tr>
<tr>
<td align="left">port</td>
<td>intタイプ</td>
<td>ゲームプロセスモニターのポート番号</td>
</tr>
<tr>
<td align="left">logParameters</td>
<td>TencentCloud::Gse::Server::LogParameters</a></td>
<td>アップロードが必要なログパス</td>
</tr>
</tbody></table>

#### 戻り値の説明  
- True：成功。
- False：失敗。

エラーメッセージを含む一般的な結果。具体的なタイプはGenericOutcomeです。

#### ユースケース
```
    std::string serverOut("./logs/serverLog.txt");
    std::string serverErr("./logs/serverErr.txt");
    std::vector<std::string> logPaths;
    logPaths.push_back(serverOut);
    logPaths.push_back(serverErr);
    int listenPort = 9090;

    TencentCloud::Gse::Server::ProcessParameters processReadyParameter = TencentCloud::Gse::Server::ProcessParameters(
        std::bind(&GseManager::OnStartGameSession, this, std::placeholders::_1),
        std::bind(&GseManager::OnProcessTerminate, this),
        std::bind(&GseManager::OnHealthCheck, this),
        listenPort, TencentCloud::Gse::Server::LogParameters(logPaths)
        );

    TencentCloud::Gse::GenericOutcome readyOutcome = TencentCloud::Gse::Server::ProcessReady(processReadyParameter);

    if (!readyOutcome.IsSuccess())
    {
        return false;
    }
```




### onStartGameServerSession
#### インターフェースの説明
コールバック関数：1つのゲームセッションをアサインしたことを通知します。 	

#### パラメータの説明

|パラメータ名|タイプ/値|説明|
|:---|---|---|
|ユーザー定義|TencentCloud::Gse::Model::GameServerSession|ゲームセッション情報|

#### 戻り値の説明
パラメータなし。


#### ユースケース
```
void GseManager::OnStartGameServerSession(TencentCloud::Gse::Server::Model::GameServerSession myGameServerSession)
{
    TencentCloud::Gse::GenericOutcome outcome = 
    	TencentCloud::Gse::Server::ActivateGameServerSession();
}
```

### onHealthcheck
#### インターフェースの説明
コールバック関数：ヘルスチェック。1分間に1回チェックし、1分以内に健康状態が回答される必要があります。 

#### パラメータの説明

パラメータなし。


#### 戻り値の説明
- True：成功。
- False：失敗。




#### ユースケース
```
void GseManager::OnHealthCheck()
{
    //プロセスの実際の健康状態に基づき、true or falseを返します
    return true;
}
```

### onProcessTerminate

#### インターフェースの説明
コールバック関数：終了プロセス。

#### パラメータの説明
パラメータなし。

#### 戻り値の説明
- True：成功。
- False：失敗。



#### ユースケース
```
void GseManager::onProcessTerminate()
{
	TencentCloud::Gse::GenericOutcome outcome = 
		TencentCloud::Gse::Server::TerminateGameServerSession();
}   
```
