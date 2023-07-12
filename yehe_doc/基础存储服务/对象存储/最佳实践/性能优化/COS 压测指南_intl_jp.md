## COSBenchの紹介

COSBenchはIntel社が開発した、オブジェクトストレージ向けの負荷テストツールです。S3プロトコルと互換性を持つオブジェクトストレージとして、Tencent CloudのCloud Object Storage (COS)は、このツールを使用して、読み取り/書き込みの負荷テストを実施できます。


## システム環境

実行環境はCentOS 7.0以降のバージョンを推奨します。ubuntu環境では、予期せぬ問題が発生することがあります。


## 性能に影響する要因

- **コア数**：コアが少なく、有効になっているworkerが多い場合、コンテキストの切替でオーバーヘッドが大量に発生しがちなため、負荷テストに32コアか64コアを推奨します。
- **NIC**：出力トラフィックはNICに制限されるため、大きいファイルのトラフィック負荷テストには10GB以上のNICを推奨します。
- **リクエストするネットワークリンク**：パブリックネットワークのリンクは質にばらつきがあります。また、パブリックネットワークからダウンロードするとき、パブリックネットワーク下りトラフィック料金が発生します。そのため、同じリージョンではプライベートネットワークアクセスを推奨します。
- **テスト時間**：性能テストを実施するとき、比較的安定する値を測定できるように、テスト時間を長めにすることを推奨します。
- **テスト環境**：プログラムが実行するJDKのバージョンは、性能に影響を与えます。例えば、HTTPSのテストで、古いバージョンのクライアントには暗号化アルゴリズムの[GCM BUG](https://bugs.openjdk.java.net/browse/JDK-8201633)、乱数ジェネレータにはロックなどの問題が発生することがあります。


## COSBench 実行手順

1. COSBench GitHubウェブサイトから[COSBench 0.4.2.c4.zip圧縮パッケージをダウンロード](https://github.com/intel-cloud/cosbench/releases/tag/v0.4.2.c4)し、サーバー上で解凍します。
2. 以下のコマンドを実行して、COSBenchの依存パッケージをインストールします。
 - centosの場合、以下のコマンドを実行して、依存パッケージをインストールします：
```
sudo yum install nmap-ncat java curl java-1.8.0-openjdk-devel -y
```
 -ubuntuの場合、以下のコマンドを実行して、依存パッケージをインストールします
```
sudo apt install nmap openjdk-8-jdk 
```
3. s3-config-sample.xmlファイルを編集し、タスクの設定情報を追加します。タスク設定は以下の5段階に分けられています：
   1. init段階：バケットを作成します。
   2. prepare段階：main段階の準備として、workerスレッドを使用し、PUT操作で指定したサイズのオブジェクトをアップロードします。
   3. main段階：workerスレッドがオブジェクトを指定した時間で読み書きします。
   4. cleanup段階：生成されたオブジェクトを削除します。
   5. dispose段階：バケットを削除します。

 設定例を以下に示します：
```shell
<?xml version="1.0" encoding="UTF-8" ?>
<workload name="s3-50M-sample" description="sample benchmark for s3">

  <storage type="s3" config="accesskey=AKIDHZRLB9Ibhdp7Y7gyQq6BOk1997xxxxxx;secretkey=YaWIuQmCSZ5ZMniUM6hiaLxHnxxxxxx;endpoint=http://cos.ap-beijing.myqcloud.com" />

  <workflow>

    <workstage name="init">
      <work type="init" workers="10" config="cprefix=examplebucket;csuffix=-1250000000;containers=r(1,10)" />
    </workstage>

    <workstage name="prepare">
      <work type="prepare" workers="100" config="cprefix=examplebucket;csuffix=-1250000000;containers=r(1,10);objects=r(1,1000);sizes=c(50)MB" />
    </workstage>

    <workstage name="main">
      <work name="main" workers="100" runtime="300">
        <operation type="read" ratio="50" config="cprefix=examplebucket;csuffix=-1250000000;containers=u(1,10);objects=u(1,1000)" />
        <operation type="write" ratio="50" config="cprefix=examplebucket;csuffix=-1250000000;containers=u(1,10);objects=u(1000,2000);sizes=c(50)MB" />
      </work>
    </workstage>

    <workstage name="cleanup">
      <work type="cleanup" workers="10" config="cprefix=examplebucket;csuffix=-1250000000;containers=r(1,10);objects=r(1,2000)" />
    </workstage>

    <workstage name="dispose">
      <work type="dispose" workers="10" config="cprefix=examplebucket;csuffix=-1250000000;containers=r(1,10)" />
    </workstage>

  </workflow>

</workload>
```
**パラメータの説明**
<table>
<thead>
<tr><th>パラメータ</th><th>説明</th></tr>
</thead>
<tbody>
<tr>
<td>accesskey、secretkey</td>
<td>キー情報。サブアカウントキーを使用し、<a href="https://intl.cloud.tencent.com/document/product/436/32972">最小権限ガイド</a>に従うことで、使用上のリスクを低減させることをお勧めします。サブアカウントキーの取得については、<a href="https://intl.cloud.tencent.com/document/product/598/32675">サブアカウントのアクセスキー管理</a>をご参照ください</td>
</tr>
<tr>
<td>cprefix</td>
<td>バケット名のプレフィックス。例えば、examplebucket</td>
</tr>
<tr>
<td>containers</td>
<td>パケット名中の数字の範囲。最後のパケット名はcprefixとcontainersから構成されます。例えば、examplebucket1、examplebucket2</td>
</tr>
<tr>
<td>csuffix</td>
<td>ユーザーのAPPID。APPIDの前に<code>-</code>の記号を付けることに注意してください（例：-1250000000）</td>
</tr>
<tr>
<td>runtime</td>
<td>負荷テストの実行時間</td>
</tr>
<tr>
<td>ratio</td>
<td>読み取りと書き込みの比率</td>
</tr>
<tr>
<td>workers</td>
<td>負荷テストのスレッド数</td>
</tr>
</tbody>
</table>
4. cosbench-start.shファイルを編集します。Java起動行に以下のパラメータを追加して、s3のmd5チェックサム機能を無効にします。
```plaintext
-Dcom.amazonaws.services.s3.disableGetObjectMD5Validation=true
```
![](https://qcloudimg.tencent-cloud.cn/raw/ac010bb86f091d709a0776b4e20a5858.png)
5. cosbenchサービスを起動します。
 - centosの場合、以下のコマンドを実行します：
```plaintext
sudo bash start-all.sh
```
 - ubuntuの場合、以下のコマンドを実行します：
```plaintext
sudo bash start-driver.sh &
sudo bash start-controller.sh &
```
6. 以下のコマンドを実行してタスクをサブミットします。
```plaintext
sudo bash cli.sh submit conf/s3-config-sample.xml
```
さらに、このURL`http://ip:19088/controller/index.html`（ipはユーザーの負荷テストマシンのIPに置き換えます）によって実行状態を確認します。
![](https://main.qcloudimg.com/raw/77f1631fa15141332d123fb472bab7ac.png)
下図に示すように、5段階が表示されます：
![](https://main.qcloudimg.com/raw/3ccb5a60253ceb20c6da9292582c4355.png)
7. 次の例は、所属リージョンが北京リージョン、32コア、プライベートネットワーク帯域幅が17GbpsのCVMで行うアップロードおよびダウンロードパフォーマンステストです。次の2段階が含まれます。
    1. prepare段階：100workerスレッドが50MBのオブジェクトを1000個アップロードします。
    2. main段階：100workerスレッドがオブジェクトの読み書きを300秒実行します。

 上記の段階1と段階2の性能テストを実行した結果は以下のとおりです：
![](https://main.qcloudimg.com/raw/e3ac34b6f8340c5cbc834d4f98ba9341.png)
8. 以下のコマンドを実行して、テストサービスを停止します。
```plaintext
sudo bash stop-all.sh
```
