## 操作ケース

Tencent Kubernetes Engine（TKE）は、デフォルトですべてのクラスターに基本的な監視機能を提供します。次の方法でTKEの監視データを確認できます。
- [クラスター指標の確認](#check1)
- [ノード指標の確認](#check2)
- [ノード内のPod指標の確認](#check3)
- [ワークロード指標の確認](#check4)
- [ワークロード内のPod指標の確認](#check5)
- [Pod内のContainer指標の確認](#check6)

## 前提条件
コンソールにログインし、【[ Cluster ](https://console.cloud.tencent.com/tke2/cluster?rid=1)】の管理ページへ進んでいます。

## 操作手順

<span id="check1"></span>
### クラスター指標の確認
監視データの確認を必要とするクラスター行では、<img src="https://main.qcloudimg.com/raw/fef90a2f69f50758b30e4c4b5e0bc7de.png" style="margin-bottom: -2px;;"></img>をクリックして、クラスターによって監視される情報ページを確認できます。下図の通りです：
![](https://main.qcloudimg.com/raw/444d1c462cf681ec7456229b25373c3a.png)

<span id="check2"></span>
### ノード指標の確認
以下のアクションを使用して、ノードとMaster&Etcdノードの監視情報を確認できます。
1. 確認を必要とするクラスターID/名称を選択して、クラスターの管理ページへ進みます。
2. **Node Management **を展開して、ノードとMaster&Etcdノードの監視情報を確認できます。
 - **Node**>**Monitoring**を選択して、** Node Monitoring**ページへ進んで監視情報を確認できます。下図の通りです：
![](https://main.qcloudimg.com/raw/c1c1fca1e108f8479b50a895c2d2d0b5.png)
 - **Master & Etcd **>** Monitoring **を選択して、**Master&Etcd監視**ページへ進んで監視情報を確認できます。下図の通りです：
![](https://main.qcloudimg.com/raw/b178510aaf43b2907d64835d7384a5b1.png)

<span id="check3"></span>
### ノード内のPod指標の確認
次の2つの方法を使用して、ノード内のPod指標を確認できます。
1. 確認を必要とするクラスターID/名称を選択して、クラスターの管理ページへ進みます。
2. **Node Management**>** Node**を選択して、ノードリストページへ進みます。
3. 実際のニーズに応じて、ノード内のPod指標の確認方法を選択します。
 - ノードリストからPod指標を確認します。
    1. ** Monitoring**をクリックして、**Node Monitoring**ページへ進みます。
    2. **Pod**をクリックして、確認したいノードとして** Node**を選択すると、ノード内のPodの監視指標比較チャートを確認できます。下図の通りです：
![](https://main.qcloudimg.com/raw/e58301ce2675d2de018a867c31fcfb69.png)
 - ノードの詳細ページでPod指標を確認します。
    1. 確認を必要とするノードID/ノード名を選択して、ノードの管理ページへ進みます。
    2. **Pod Management**タブを選択し、**Monitoring **をクリックして、ノード内のPodの監視指標比較チャートを確認できます。下図の通りです：
![](https://main.qcloudimg.com/raw/269631374cbe8ff955de4d691c53772c.png)

<span id="check4"></span>
### ワークロード指標の確認
1. 確認を必要とするクラスターID/名称を選択して、クラスターの管理ページへ進みます。
2. **Workload **>**Any Workload Type**を選択します。例えば、**Deployment**を選択して、Deployment管理ページへ進みます。
3. **Monitoring**をクリックして、ワークロードの監視情報を確認できます。下図の通りです：
![](https://main.qcloudimg.com/raw/392b8235bb98367b50bc4b20e6ad3118.png)

<span id="target"></span><span id="check5"></span>
### ワークロード内のPod指標の確認
<span id="first"></span>
1. 確認を必要とするクラスターID/名称を選択して、クラスターの管理ページへ進みます。
2. **Workload**>**Any Workload Type**を選択します。例えば、**Deployment**を選択して、Deployment管理ページへ進みます。
3. 確認を必要とするワークロード名称を選択して、ワークロードの管理ページへ進みます。<span id="third"></span>
4. ** Pod Management**タブを選択し、**Monitoring**をクリックして、ワークロード内のすべてのPodの監視指標比較チャートを確認できます。下図の通りです：
![](https://main.qcloudimg.com/raw/bda91f0b0fb55cf87cf7258cc471ae1f.png)

<span id="check6"></span>
### Pod内のContainer指標の確認
1. [ Viewing Pod Metrics in a Workload](#target)の[手順1](#first)-[手順3](#third)を参照して、ワークロードの詳細ページへ進みます。
2. **Pod Management**タブを選択し、** Monitoring **をクリックして、**Pod Monitoring**ページへ進みます。
3. **Container**をクリックして、確認したいPodとして**Pod**を選択すると、Pod内のContainerの監視指標比較チャートを確認できます。下図の通りです：
![](https://main.qcloudimg.com/raw/28b567cd6eda684fbd0076d89bdadd76.png)


