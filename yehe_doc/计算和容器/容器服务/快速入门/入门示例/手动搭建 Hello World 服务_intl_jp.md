## 操作場面
このドキュメントはコンテナクラスター内のHello WorldのNode.jsバージョンのサービスを迅速に作成する方法を紹介します。その他のDockerイメージを構築するチュートリアルについては、[dockerイメージを構築する方法](https://intl.cloud.tencent.com/document/product/457/9115)をご参照ください。

##  前提条件

- クラスターが作成されました。詳細は、[クラスター作成](https://intl.cloud.tencent.com/document/product/457/30637)をご参照ください。
- ノードにログインしました。そして、このノードにはNode.jsを設置しました。

## 操作手順
### コーディングとイメージ作成
#### アプリケーション作成
1. 次のコマンドを順番に実行して、hellonodeのフォルダを作成して入ります。
```shell
mkdir hellonode
```
```shell
cd hellonode/
```
2. 次のコマンドを実行して、server.jsファイルを新規作成して開きます。
```
vim server.js
```
3. **i**を押して、編集モードに転換し、次の内容をserver.jsに入力します。
```js
var http = require('http');
var handleRequest = function(request, response) {
  console.log('Received request for URL: ' + request.url);
  response.writeHead(200);
  response.end('Hello World!');
};
var www = http.createServer(handleRequest);
www.listen(80);
```
「**Esc**」を押して、 「**:wq**」を入力し、ファイルを保存してリターンします。
4. 次のコマンドを実行して、server.jsファイルを実行します。
```shell
node server.js
```
次は二つの方法を提供して、Hello Worldプログラムをテストします。
 - 再びノードにログインして、次のコマンドを実行します。
```shell
curl 127.0.0.1:80
```
次のように表示されれば、Hello Worldプログラムが成功的に実行されたことを示します。
![](https://main.qcloudimg.com/raw/4b97b9e2fdaee77376b114ef92f90936.png)
 - ローカルブラウザを開き、`IPアドレス：ポート`の形式でアクセスして、ポートは80です。
 次のように表示されれば、Hello Worldプログラムが実行されたことを示します。
![](https://main.qcloudimg.com/raw/1fb82340313ab81dcffd693f9577624d.png)


#### Dockerイメージ作成
>?その他のDockerイメージは[dockerイメージの構築方法](https://intl.cloud.tencent.com/document/product/457/9115)をご参照ください。
>
1. 次のコマンドを順番に実行して、hellonodeフォルダでDockerfileファイルを作成します。
```
cd hellonode
```
```
vim Dockerfile
```
2. **i**を押して、編集モードに転換し、次の内容をDockerfileファイルに入力します。
```shell
FROM node:4.4
EXPOSE 80
COPY server.js .
CMD node server.js
```
「**Esc**」を押して、 「**:wq**」を入力し、ファイルを保存してリターンします。
3. 次のコマンドを実行して、イメージを構築します。
```shell
docker build -t hello-node:v1 .
```
4. <span id="search">次のコマンドを実行して、構築されたhello-nodeイメージを確認します。</span>
```
docker images 
```
結果は次のように表示されれば、hello-nodeイメージが成功的に構築されたことを示し、このIMAGE IDを記録します。下図の通りです：
![](https://main.qcloudimg.com/raw/d5bf4dfa0f805d6f90399c814b3152b1.png)


#### このイメージをqcloudイメージウエアハウスにアップロード
>!イメージアップロードは次の条件を満たす必要があります：
>- [私のイメージ](https://console.cloud.tencent.com/tke2/registry/user/space)でネームスペースを作成しました。
>- [Tencent Cloud registry](https://intl.cloud.tencent.com/document/product/457/9117)にログインしました。その他のイメージ操作は[イメージウエアハウス基本チュートリアル](https://intl.cloud.tencent.com/document/product/457/9117)をご参照ください。

次のコマンドを順番に実行して、イメージをqcloudイメージウエアハウスにアップロードします。
```shell
sudo docker tag IMAGEID ccr.ccs.tencentyun.com/ネームスペース/helloworld:v1
```
```
sudo docker push ccr.ccs.tencentyun.com/ネームスペース/helloworld:v1
```
>?
>- コマンドのIMAGEIDを[イメージ確認](#search)に記録されたIMAGEIDに置き換えてください。
>- コマンドのネームスペースを作成されたネームスペースに置き換えてください。
>
次の結果が表示されれば、イメージが成功的にアップロードされたことを示します。
![](https://main.qcloudimg.com/raw/1aadc58e8663488200e3e34a532642c4.png)


### このイメージでHello Worldサービス作成
>!Hello Worldサービスを作成して使用する前に、必ず次の条件を満たす必要があります：
>- Tencent Cloudアカウント登録済みです。[登録ページ](https://intl.cloud.tencent.com/register)に移動し、関連情報を記入してTencent Cloudアカウントに登録してください。
>- クラスターが作成されました。詳細は、[クラスター作成](https://intl.cloud.tencent.com/document/product/457/30637)をご参照ください。
>
1. Tencent Kubernetes Engineコンソールにログインし、左側のナビゲーションバーで【[ Clusters ](https://console.cloud.tencent.com/tke2/cluster)】を選択します。
2. 「クラスター管理」ページでサービスを作成する必要のあるクラスターIDを選択し、クラスターのロード「Deployment」ページに入って、【 Create】をクリックします。下図の通りです：
![](https://main.qcloudimg.com/raw/bacaf92e14b7c342db6b3179c2ae5e8f.png)
3. 「Create Workload」ページで次の情報によって、ロードの基本情報を設定します。下図の通りです：
![](https://main.qcloudimg.com/raw/e2d083fececab9d1f84dd82f3850537a.png)
 - **ロード名**：作成するロードの名前を入力し、本文はhelloworldを例として説明します。
 - **説明**：ロードについての情報を記入します。
 - **タグ**：key = value、この例ではタグのデフォルト値がk8s-app = **helloworld**です。
 - **ネームスペース**：必要に応じて選択します。
 - **タイプ**：必要に応じて選択します。
 - **ボリューム**：必要に応じてロードのマウントを設定します。詳細は[Volume管理](https://intl.cloud.tencent.com/document/product/457/30678)をご参照ください。
4. 次の情報を参照して「インスタンスコンテナ」を設定します。下図の通りです：
インスタンスコンテナの名前を入力し、本文はhelloworldを例として説明します。
![](https://main.qcloudimg.com/raw/27b651e922b4a3afb925326ed8393bd0.png)
【 Select an image】をクリックして、ポップアップボックスで【My Images 】を選択し、検索ボックス機能でhelloworldイメージを見つけて【Ok】をクリックします。下図の通りです：
![](https://main.qcloudimg.com/raw/86a18f657b75d338ab3c084710c3ba10.png)
主なパラメータ情報は下記の通りです：
 - **イメージバージョン（Tag）**：デフォルト値v1を使用します。
 - **イメージプルポリシー**：次の三つのポリシーを提供し、必要に応じて選択してください。本文は設定しなくてデフォルトポリシーを使用することを例として説明します。
イメージプルポリシーを設定しなくて、イメージバージョンはnullや`latest`の時、Alwaysポリシーを使用し、そうでなければIfNotPresentポリシーを使用します。
    - **Always**：いつもリモートでこのイメージをプルします。
    - **IfNotPresent**：ローカルイメージをデフォルトで使用し、ローカルにこのイメージがない場合、リモートでこのイメージをプルします。
    - **Never**：ローカルイメージだけを使用し、ローカルにこのイメージがない場合、異常を報告します。
5. 「インスタンス数量」では、次の情報によってサービスのインスタンス数量を設定します。次の通りです。
![](https://main.qcloudimg.com/raw/6cc62e4c9118b83f7c4552a55f4c4cf0.png)
 - **手動調整**：インスタンス数量を設定し、本文のインスタンス数量は１に設定します。「＋」や「ー」をクリックして、インスタンス数量をコントロールします。
 - **自動調整**：いずれかの設定条件を満たせば、インスタンス（pod）数量を自動的に調整します。詳細は[サービスの自動的なスケールアウトとスケールイン](https://intl.cloud.tencent.com/document/product/457/32424)をご参照ください。
6.   次の提示によって、ロードのアクセス設定をします。次の通りです。   
![](https://main.qcloudimg.com/raw/57b97c8877fd3ac116c71fad4bf416f2.png)
 - **Service**：「使用」を選択します。
 - **サービスのアクセス方式**：「パブリックネットワークを提供してアクセス」を選択します。
 - **Cloud Load Balancer**：必要に応じて選択します。
 - **ポートマッピング**：TCPプロトコルを選択し、コンテナポートとサービスポートを80に設定します。
 >!サービスのあるクラスターのセキュリティグループはノードネットワークとコンテナネットワークをインターネットにオープンする必要があります。同時に、30000 - 32768ポートをインターネットにオープンする必要もあるし、そうでなければTencent Kubernetes Engineが使用できない問題が発生するかもしれません。詳細は[Tencent Kubernetes Engineセキュリティグループ設定](https://intl.cloud.tencent.com/document/product/457/9084)をご参照ください。
7. 【Create Workload】をクリックして、Hello Worldサービスの作成を完了します。

### Hello Worldサービスにアクセス
次の二つの方式でHello Worldサービスにアクセスできます。

#### Cloud Load Balancer IPでHello Worldサービスにアクセス
1. 左側ナビゲーションバーで【[ Clusters](https://console.cloud.tencent.com/tke2/cluster)】をクリックして、「クラスター管理」ページに入ります。
2. Hello WorldサービスのあるクラスターIDをクリックして、【Servic】>【Service】を選択します。
3. サービス管理のページでhelloworldサービスのCloud Load Balancer　IPをコピーして、次の通りです。
![](https://main.qcloudimg.com/raw/96fb6f94d4d365ce4007ff7961f5e438.png)

#### サービスの名前でHello Worldサービスにアクセス
クラスター内の他のサービスやコンテナはサービスの名前で直接アクセスできます。

### Hello Worldサービス検証
サービスにアクセスする時、次のように表示されれば、Hello Worldサービスが作成されたことになります。
![](https://main.qcloudimg.com/raw/817c981526ac6297c778c1cb154a8d90.png)
コンテナの作成に失敗した場合、[よくある質問](https://intl.cloud.tencent.com/document/product/457/8187)をご参照ください。
