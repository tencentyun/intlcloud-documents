TEMアプリケーションが実行失敗状態となった場合、それは少なくとも1つのインスタンスがRunning状態にないことを意味します。ここではよくあるインスタンスのエラー状態をいくつか挙げ、対応するトラブルシューティングをどのように行うかについてご説明します。

## インスタンスのエラー状態

### CrashLoopBackOff

#### 状態の説明
インスタンスのアプリケーション実行に問題があり、コンテナの起動/実行に失敗しました。

#### 対処方法
インスタンスのログを確認し、**ログの内容**によってトラブルシューティングを行います。

![](https://qcloudimg.tencent-cloud.cn/raw/f232dded30fd6e734a7cdd9d6adbdb07.png)

### Error

#### 状態の説明
CrashLoopBackOffと同じように、インスタンスのアプリケーション実行に問題があり、コンテナの起動/実行に失敗したことを表します。

#### 対処方法
インスタンスのログを確認し、**ログの内容**によってトラブルシューティングを行います。

![](https://qcloudimg.tencent-cloud.cn/raw/f232dded30fd6e734a7cdd9d6adbdb07.png)

### Running Unhealthy:Readiness probe failed

#### 状態の説明
アプリケーション設定のReadinessヘルスチェックに失敗しました。

#### 対処方法
**アプリケーションのデプロイ** > **ヘルスチェック**ページで、アプリケーションの**Readinessチェック**の設定が正しいかどうか確認してください。
![](https://qcloudimg.tencent-cloud.cn/raw/0201f789f3433b50d32ba6f5fe2f0f74.png)

### Running Unhealthy:Liveness probe failed

#### 状態の説明
アプリケーション設定のLivenessヘルスチェックに失敗しました。

#### 対処方法
**アプリケーションのデプロイ** > **ヘルスチェック**ページで、アプリケーションの**Livenessチェック**の設定が正しいかどうか確認してください。
![](https://qcloudimg.tencent-cloud.cn/raw/53113c0dcceb186acfeba9388430c4f8.png)

### Running Unhealthy:Readiness check failed according to l4 listener: xxx of CLB xxx. Service: xxx

#### 状態の説明
アプリケーション設定のアクセス設定に接続できません。

#### 対処方法
**アプリケーションの詳細** > **基本情報** > **アクセス設定**ページで、アプリケーション設定の**アクセス設定**のポートとプロトコルが正しいかどうか確認してください。
![](https://qcloudimg.tencent-cloud.cn/raw/9f7d2818b7e57b49ad6f5c25e39ec5b6.png)

### PostStartHookError

#### 状態の説明
アプリケーション設定のPostStartの実行に失敗しました。

#### 対処方法
**アプリケーションのデプロイ** > **起動/停止管理**ページで、アプリケーション設定の**PostStart**が正常に実行可能かどうか確認してください。

![](https://qcloudimg.tencent-cloud.cn/raw/88c7a9bb3124992f4a9573c71ee45e68.png)

### ContainerCreating

#### 状態の説明
インスタンスコンテナの作成に失敗しました。

#### 対処方法
**アプリケーションのデプロイ** > **永続ストレージ**のページで、アプリケーションが存在しないデータボリュームをマウントしていないか確認してください。![](https://qcloudimg.tencent-cloud.cn/raw/828dcb4c0720a5fb7bb4c5439f9a914a.png)

### CreateContainerConfigError

#### 状態の説明
インスタンスコンテナの設定に失敗しました。

#### 対処方法
**アプリケーションのデプロイ** > **環境変数**のページで、アプリケーションが存在しない設定を引用していないか確認してください。

![](https://qcloudimg.tencent-cloud.cn/raw/7b8bac1611cd55a68030df1c2d232a09.png)

### ImagePullBackOff

#### 状態の説明
インスタンスイメージのプルに失敗しました。

#### 対処方法
[TCRコンソール](https://console.cloud.tencent.com/tcr/repository?rid=1)で、アプリケーションに使用しているイメージが存在するか、または誤って削除されていないか確認します。
