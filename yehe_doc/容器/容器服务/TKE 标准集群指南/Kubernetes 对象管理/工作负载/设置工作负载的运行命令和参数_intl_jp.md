## 概要

ワークロードを作成する場合は、通常、イメージを使用して、インスタンス内のコンテナが実行するプロセスを指定します。デフォルトでは、イメージはデフォルトのコマンドを実行します。特定のコマンドを実行する必要がある場合、またはイメージのデフォルト値をオーバーライドする必要がある場合は、次の3つの設定を使用してください：
- ワークディレクトリ（workingDir）：現在のワークディレクトリを指定します。
- 実行コマンド（command）：イメージが実行する実際のコマンドをコントロールします。
- コマンドパラメータ（args）：実行コマンドに渡されるパラメータです。

## ワークディレクトリの説明

WorkingDirは、現在のワークディレクトリを指定します。存在しない場合は、自動的に作成されます。指定されていない場合は、コンテナを実行するときのデフォルト値が使用されます。WORKDIRがイメージで指定されていなく、コンソールで指定されていない場合、workingDirはデフォルトで「/」になります。

## コマンドとパラメータの使用

docker runコマンドをTencent Kubernetes Engine（TKE）に適応させる方法については、[docker runパラメータ適応](https://intl.cloud.tencent.com/document/product/457/9883)をご参照ください。
 
Dockerイメージには、イメージ情報の保存に関連するメタデータがあります。実行コマンドとパラメータが指定されていない場合、コンテナはイメージの作成時に提供されたデフォルトのコマンドとパラメータを実行します。Dockerによってネイティブに定義されるフィールドは、「Entrypoint」と「CMD」です。詳細については、Dockerの[Entrypoint説明](https://docs.docker.com/engine/reference/builder/#/entrypoint)および[CMD説明](https://docs.docker.com/engine/reference/builder/#/cmd)をご参照ください。
サービスの作成時にコンテナの実行コマンドとパラメータを入力すると、TKEはイメージの構築時のデフォルトのコマンド（すなわち、「Entrypoint」と「CMD」）をオーバーライドします。そのルールは次のとおりです：

| イメージEntrypoint |イメージCMD|コンテナの実行コマンド|コンテナの実行パラメータ| 最終実行|
| :-------- | :--------| :------ | :-------- | :------ |
| [ls]   | [/home]|  未設定  |未設定    |[ls / home]  |
| [ls]   | [/home]|  [cd]  |未設定    |	[cd]        |
| [ls]   | [/home]|  未設定  |[/data] |[ls / data]  |
| [ls]   | [/home]|  [cd]  |[/data] |[cd / data]  |

> 
>- Docker entrypointはTKEコンソールの実行コマンドに対応し、Docker runのCMDパラメータはTKEコンソールの実行パラメータに対応します。複数の実行パラメータがある場合は、TKEの実行パラメータにパラメータを入力する必要があり、各パラメータは別々の行にあります。
>- [Tencent Kubernetes Engineコンソール](https://console.cloud.tencent.com/tke2)によるコンテナの実行コマンドとパラメータの設定例については、[CommandとArgs](https://intl.cloud.tencent.com/document/product/457/9883#command-.E5.92.8C-args)をご参照ください。 
