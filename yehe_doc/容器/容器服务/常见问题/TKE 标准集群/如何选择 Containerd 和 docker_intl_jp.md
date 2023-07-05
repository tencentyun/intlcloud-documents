### ランタイムコンポーネントの選択方法は？
コンテナランタイム（Container Runtime）はKubernetes（K8S） の最も重要なコンポーネントの１つであり、イメージとコンテナのライフサイクルを管理します。Kubelet は `Container Runtime Interface (CRI)` を通して、コンテナランタイムと通信し、イメージとコンテナを管理します。

TKE は containerd と docker をランタイムコンポーネントとして選択することをサポートします：
- Containerd 呼び出しチェーンはより短く、コンポーネントが少なく、安定性に優れ、占用するノードリソースがより少ないです。Containerd の選択を推奨します。
- 次の場合、 ランタイムコンポーネントにdocker を選択してください：
 - docker in docker を使用する場合。
 - TKE ノードにおいて docker build/push/save/load 等のコマンドを使用する場合。
 -  docker API を呼び出す場合。
 - docker compose または docker swarm が必要な場合。
 

### Containerd と Docker コンポーネントにおいてよく使われるコマンドはなんですか。
Containerd は docker API と docker CLI をサポートしていませんが、cri-toolコマンドを通してそれに当たる機能を実現できます。

| イメージに関する機能   | Docker         | Containerd      |
|:-------- |:-------------- |:--------------- |
| ローカルイメージリストを表示 | docker images  | crictl images       |
| イメージをダウンロード | docker pull    | crictl pull     |
| イメージをアップロード | docker push     | None             |
| ローカルイメージを削除   | docker rmi     | crictl rmi      |
| イメージ詳細を閲覧   | docker inspect IMAGE-ID | crictl inspecti IMAGE-ID |



| コンテナに関する機能 | Docker         | Containerd     |
|:------ |:-------------- |:-------------- |
| コンテナリストを表示 | docker ps      | crictl ps      |
| コンテナを作成   | docker create  | crictl create  |
| コンテナを起動   | docker start   | crictl start   |
| コンテナを停止   | docker stop    | crictl stop    |
| コンテナを削除   | docker rm     | crictl rm      |
| コンテナ詳細を閲覧 | docker inspect | crictl inspect |
| attach | docker attach  | crictl attach  |
| exec   | docker exec    | crictl exec    |
| logs   | docker logs    | crictl logs    |
| stats  | docker stats   | crictl stats   |


| PODに関する機能 | Docker         | Containerd     |
|:------- |:------ |:--------------- |
| PODリストを表示  | None      | crictl pods     |
| PODの詳細を閲覧 | None      | crictl inspectp |
| PODを実行   | None      | crictl runp     |
| PODを停止   | None      | crictl stopp    |

### 呼び出しチェーンにはにどんな違いがありますか。
- DockerがK8S コンテナとして動作する際、呼び出し関係は以下のようになります。
`kubelet --> docker shim （kubeletプロセスに存在） --> dockerd --> containerd`
- ContainerdがK8S コンテナとして動作する際、呼び出し関係は以下のようになります。
`kubelet --> cri plugin（containerdプロセスに存在） --> containerd`

そのうち dockerd は、 swarm cluster、 docker build 、 docker API といった機能を追加したものの、バグを作り込みました。なお、containerd と比べて、呼び出しが１つ多くなります。


## Streamサービス
>Kubectl exec/logs といったコマンドは、apiserver とコンテナランタイムの間にストリーム転送チャネルを構築する必要があります。
>

###  どのようにContainerd でStreamサービスを設定または使用しますか？
Docker API自体はStreamサービスを提供し、kubelet 内の docker-shim は docker API を通してストリームを転送します。
Containerd のStreamサービスに対して、個別に設定する必要があります。
```
[plugins.cri]
  stream_server_address = "127.0.0.1"
  stream_server_port = "0"
  enable_tls_streaming = false
```

### K8S 1.11より前のバージョンとそれ以降のバージョンにおける設定の違いは？
Containerd のストリームサービスは K8S のバージョンによって、実行時の設定が異なります。
- K8S 1.11より前のバージョン：
Kubelet は stream proxy をせず、リダイレクトのみをします。すなわち、 Kubelet は containerd が公開する ストリームサーバーのアドレスを apiserverに送信し、 apiserver が containerd のストリームサービスに直接アクセスします。このとき、セキュリティのため、Streamサービスのフォワーダーを認証する必要があります。
- K8S 1.11 以降：
 K8S1.11 は [kubelet stream proxy](https://github.com/kubernetes/kubernetes/pull/64006) を導入したため、containerd stream サービスはローカルアドレスの監視のみを行えばよいです。

## その他のちがい
### コンテナログと関連パラメータ

<table>
	<tr>
	<th style="width:10%;">比較項目</th>
	<th>Docker</th>
	<th>Containerd</th>
	</tr>
	<tr>
		<td>保存パス</td>
		<td>
	Docker を K8S コンテナとして実行する際、コンテナログの書き込みは docker によって行われ、<code>/var/lib/docker/containers/$CONTAINERID</code> のようなディレクトリに保存されます。Kubelet は <code>/var/log/pods</code> と <code>/var/log/containers</code> の下に <code>/var/lib/docker/containers/$CONTAINERID</code> ディレクトリ下にあるコンテナログファイルを指すソフトリンクを作成します。
		</td>
		<td>
		Containerd を K8S コンテナとして実行する際、コンテナログの書き込みは Kubelet によって行われ、 <code>/var/log/pods/$CONTAINER_NAME</code> ディレクトリに保存されると同時に、 <code>/var/log/containers</code> ディレクトリにログファイルを指すソフトリンクを作成します。            
		</td>
	</tr>
	<tr>
		<td>設定パラメータ </td>
		<td>
		Dockerの設定ファイルで次を指定します。
		<br>    <code>"log-driver": "json-file",</code> 
		<br>    <code>"log-opts": {"max-size": "100m","max-file": "5"}</code>
		</td>
		<td>
		<ul>
		<li>
		方法１： Kubelet パラメータに次を指定します。<br> <code>--container-log-max-files=5<br> --container-log-max-size="100Mi"</code> <br>
		</li>
		<li>方法2： KubeletConfiguration で次を指定します。<br>    <code>"containerLogMaxSize": "100Mi",</code><br>    <code>"containerLogMaxFiles": 5, </code>
		</li>
		</ul>
		</td>
	</tr>
	<tr>
	<td>コンテナログをデータディスクに保存</td>
	<td>データディスクを 「data-root」（デフォルトは <code>/var/lib/docker</code>）へマウントしてください。</td>
	<td>データディスクのマウントポイント配下のあるディレクトリを指すソフトリンク <code>/var/log/pods</code> を作成します。<br>TKE で　「コンテナとイメージをデータディスクに保存」 を選択すると、自動でソフトリンク <code>/var/log/pods</code> が作成されます。
	</td>
	</tr>
</table>


### CNIネットワーク
| 比較項目      | Docker            | Containerd                                                                                                       |
|:-------- |:---------------------------------------- |:---------------------------------------------------------------------------------------------------------------- |
| CNIの呼出元 | Kubelet 内の docker-shim                    | Containerd 内の cri-plugin（containerd 1.1 以降）                                                                        |
| CNI の設定方法  | Kubelet パラメータ <code>--cni-bin-dir</code> と <code>--cni-conf-dir</code> | Containerd 設定ファイル（toml）：<br> <code>[plugins.cri.cni]</code><br>    <code>bin\_dir = "/opt/cni/bin"</code><br>    <code>conf\_dir = "/etc/cni/net.d"</code> |
