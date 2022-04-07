## 操作ケース
KubernetesコマンドラインツールKubectlを使用して、ローカルクライアントマシンからTKEクラスターに接続できます。このドキュメントでは、クラスターに接続する方法について説明します。

## 前提条件
curlソフトウェアをインストールしてください。
OSのタイプに応じて、Kubectlツールを取得する方法を選択してください：
> 実際のニーズに応じて、コマンドラインの「v1.8.13」を、サービスで必要なKubectlバージョンに置き換えます。

- **Mac OS Xシステム**
次のコマンドを実行して、Kubectlツールを取得します：
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.13/bin/darwin/amd64/kubectl
```
- **Linuxシステム**
次のコマンドを実行して、Kubectlツールを取得します：
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.13/bin/linux/amd64/kubectl
```
- **Windowsシステム**
次のコマンドを実行して、Kubectlツールを取得します：
```shell
curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.8.13/bin/windows/amd64/kubectl.exe
```

## 操作手順

<span id="installKubectl"></span>

### Kubectlツールのインストール

1. Kubectlツールをインストールするには、[Installing and Setting up kubectl](https://kubernetes.io/docs/user-guide/prereqs/)をご参照ください。
> 
>- すでにKubectlツールがインストールされている場合は、この手順を無視してください。
>- この手順では、Linuxシステムを例に取ります。

2. 次のコマンドを実行して、実行権限を追加します。
```shell
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```
3. 次のコマンドを実行して、インストール結果をテストします。
```shell
kubectl version
```
次のようなバージョン情報が出力されている場合は、インストールが成功したことを意味します。
```shell
Client Version: version.Info{Major:"1", Minor:"5", GitVersion:"v1.5.2", GitCommit:"08e099554f3c31f6e6f07b448ab3ed78d0520507", GitTreeState:"clean", BuildDate:"2017-01-12T04:57:25Z", GoVersion:"go1.7.4", Compiler:"gc", Platform:"linux/amd64"}
```

###  Kubeconfigの構成

1. TKEコンソールにログインし、左側ナビゲーションバーの【[ Cluster ](https://console.cloud.tencent.com/tke2/cluster?rid=4)】を選択して、クラスター管理ページへ進みます。
2. 接続を必要とする**クラスターID/名称**をクリックして、クラスター詳細ページへ進みます。
3. 左側ナビゲーションバー【 Basic Information】を選択して、「基本情報」ページでは、「クラスターAPIServer情報」モジュールのクラスターのアクセスアドレス、パブリックネットワーク/プライベートネットワークのアクセス状態、Kubeconfigアクセス証明内容などの情報を確認できます。
 - **アクセスアドレス**：クラスターAPIServerのアドレスです。このアドレスをコピーしてブラウザに貼り付けてアクセスすることはできませんので、ご注意ください。
 - **アクセスエントリーの取得**：実際のニーズに応じて設定してください。
	- **パブリックネットワークへのアクセス**：デフォルトでオフします。パブリックネットワークへのアクセスがオンにすると**クラスターapiserverがパブリックネットワークに公開されますので、注意して操作してください**。また、ソース認証を構成する必要があります。デフォルトでは、すべてのソースが拒否されます。単一のIPまたはCIDRをインターネットにオープンするように構成できます。すべてのソースをインターネットにオープンするために`0.0.0.0/0`を構成することは強くお勧めしません。
	- **プライベートネットワークへのアクセス**：デフォルトでオフします。プライベートネットワークへのアクセスをオンにする場合は、サブネットを構成する必要があります。オンが成功すると、構成されたサブネットにIPアドレスがアサインされます。
 - **Kubeconfig**：クラスターのアクセス証明です。コピーやダウンロードできます。
4. 実際の状況に応じて、クラスター証明を構成します。
   構成前に、現在のアクセスクライアントはクラスターのアクセス証明が構成されているかどうかを確認してください：
	- **構成されていない**、即ち`~/.kube/config`ファイルの内容がNULLである場合は、取得したKubeconfigアクセス証明内容を直接コピーして、`~/.kube/config`に貼り付けることができます。クライアントに`~/.kube/config`ファイルがない場合は、直接作成できます。
	- **構成されている**場合は、取得したKubeconfigを指定された場所にダウンロードし、次のコマンドを順に実行して、複数のクラスターのconfigをマージできます。
```
KUBECONFIG=~/.kube/config:~/Downloads/cls-3jju4zdc-config kubectl config view --merge --flatten > ~/.kube/config
```
```
export KUBECONFIG=~/.kube/config
```
	その中で、`~/Downloads/cls-3jju4zdc-config`はクラスターのKubeconfigのファイルパスです。ローカルにダウンロードした後の実際のパスに置き換えてください。


### Kubernetesクラスターへのアクセス
1.  Kubeconfigが構成されると、次のコマンドを順に実行して、contextを確認および切り替えてクラスターにアクセスします。
```
kubectl config get-contexts
```
```
kubectl config use-context cls-3jju4zdc-context-default
```
2.  次のコマンドを実行して、クラスターに正常にアクセスできるかどうかをテストします。
```
kubectl get node
```
接続できない場合は、パブリックネットワークアクセスまたはプライベートネットワークアクセスのエントリーがオンにされているかどうかを確認し、アクセスクライアントが指定されたネットワーク環境にあることを確保してください。

## 関連説明

### Kubectlコマンドラインの説明

Kubectlは、Kubernetesクラスターアクションで使用されているコマンドラインツールです。このドキュメントでは、kubectl構文、一般的なコマンドのアクションについて説明し、一般的な例を示しています。各コマンド（すべてのメインコマンドとサブコマンドを含む）の詳細については、[kubectlのリファレンスドキュメント](https://kubernetes.io/docs/reference/generated/kubectl/kubectl/)を参照するか、または`kubectl help`コマンドを使用してヘルプの詳細を確認してください。kubectlのインストールについては、[Kubectlのインストールツール](#installKubectl)をご参照ください。
