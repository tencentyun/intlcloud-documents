## 操作シナリオ

TEMで実行されているアプリケーションは、通常、業務上のニーズなどに起因して、パブリックネットワークにアクセスする必要があります。また、ミニプログラムなどのシナリオでは、通常、ホワイトリストにアクセスする必要があります。この場合、パブリックネットワークにアクセスするアプリケーションには、固定パブリックIPが必要です。

上記の要件に基づいて、ここでは、TEMにデプロイされたアプリケーションがパブリックネットワークにアクセスする方法の詳細についてご紹介します。

#### 全体構想：
TEMのアプリケーションはユーザーの環境にデプロイされ、環境はユーザーのVPCに関連付けられます。つまり本質的には、TEMのアプリケーションはユーザーのVPCにデプロイされることになります。VPCにNAT Gatewayを設定し、NAT GatewayにEIPを関連付けることによって、VPC内のアプリケーションがパブリックネットワークにアクセスできるようにすることができます。


#### 操作フロー：
<dx-steps>
- [TEMアプリケーションのデプロイ](#step1)
- [NAT Gatewayインスタンスの作成](#step2)
- [VPCコンソールでNAT Gateway情報を設定](#step3)
- [パブリックネットワークアクセスの検証](#step4)
- [（オプション）パブリックネットワークにアクセスするためのIPを照会](#step5)
</dx-steps>



## 操作手順

### 手順1：TEMアプリケーションのデプロイ[](id:step1)

[環境の作成](https://intl.cloud.tencent.com/document/product/1094/40358)と[アプリケーションの作成](https://intl.cloud.tencent.com/document/product/1094/40362)を参照して、TEMコンソールでアプリケーションをデプロイします。



### 手順2：NAT Gatewayインスタンスの作成[](id:step2)

[NAT Gatewayコンソール](https://console.cloud.tencent.com/vpc/nat?rid=4)にログインし、左側ナビゲーションバーで【NAT Gateway】を選択し、TEMアプリケーションが配置されているリージョンを選択します。【新規作成】をクリックして、NAT Gatewayインスタンスを購入します。
<img src="https://main.qcloudimg.com/raw/c5d87bc70ca058f67bf93e99d68d47f5.png" width="600px">

- **所属ネットワーク**：TEMアプリケーションが配置されている環境のVPCと一致するようにします。
- **Elastic IP**：利用可能なパブリックネットワークElastic IP(EIP)がない場合は、ワンクリックでジャンプして購入します。購入してから、NAT Gatewayの購入ページを更新すると見つかります。



### 手順3：VPCコンソールでNAT Gateway情報を設定[](id:step3)

1. TEMコンソール【[環境](https://console.cloud.tencent.com/tem/env)】ページで、TEMアプリケーションが配置されている環境カードをクリックして、基本環境情報ページに進みます。
2. クラスターネットワークでVPCをクリックして、VPCネットワークの基本情報ページにジャンプします。
		<img src="https://main.qcloudimg.com/raw/6a240ee7d99c77aafba1a3b8340746d3.png" width="450px">
3. 【ルートテーブル】モジュールをクリックして、ルートテーブル設定ページに進みます。
4. ルートテーブルページで【新規作成】をクリックしてルートテーブルを設定します。
      ![](https://main.qcloudimg.com/raw/8a61dab5ac424d7b3654c0f63dd6118e.png)
   - **ターゲット端末**：アクセスするパブリックネットワークのIPアドレスを選択し、CIDR設定をサポートします。例えば、0.0.0.0/0を入力すると、すべてのトラフィックがNAT Gatewayに転送されます
   - **次のタイプにジャンプ**：**NAT Gateway**を選択します。
   - **次にジャンプ**：**手順2**で作成したNAT Gatewayを選択します。

   設定方法の詳細については、[カスタムルートテーブル](https://intl.cloud.tencent.com/document/product/215/35236)をご参照ください。
5. 作成したルートテーブル操作バーの【その他】>【関連サブネット】をクリックし、関連するサブネット内でTEMアプリケーションが配置されている環境に関連するサブネットを選択します
![](https://main.qcloudimg.com/raw/ad7581c40397a2880716995f87838c03.png)


### 手順4：パブリックネットワークアクセスの検証[](id:step4)

1. TEMコンソールの【[アプリケーション管理](https://console.cloud.tencent.com/tem/application?rid=4)】ページでTEMアプリケーションの「ID」をクリックして、アプリケーションインスタンスリストページに進みます。
2. アプリケーションインスタンスの操作バーの【Webshell】をクリックして、Webshel​​lに進みます。
      ![](https://main.qcloudimg.com/raw/1a82ce68a9638c84cf67589d20a92cc3.png)
3. パブリックネットワークにアクセスできるかどうかを検証します。
	![](https://main.qcloudimg.com/raw/74eaf5884506d3880dcf0529df16ea15.png)



###  手順5：（オプション）パブリックネットワークにアクセスするためのIPを照会[](id:step5)

1. TEMコンソール【[環境](https://console.cloud.tencent.com/tem/env)】ページで、TEMアプリケーションが配置されている環境カードをクリックして、基本環境情報ページに進みます。
2. クラスターネットワークでVPCをクリックして、VPCネットワークの基本情報ページにジャンプします。
		<img src="https://main.qcloudimg.com/raw/e0505caec5440515b1fc7c65f4493a2e.png" width="450px">
3. 【NAT Gateway】モジュールをクリックして、NAT Gatewayリストページに進みます。
4. ターゲットNAT Gatewayの「ID」をクリックしてNAT Gatewayの基本情報ページに進み、【関連Elastic IP】タブを選択して、パブリックネットワークにアクセスするためのIPを取得します。


## 追加料金

[NAT Gateway](https://intl.cloud.tencent.com/product/nat)およびEIPを使用すると、料金が発生します。料金の詳細については以下をご参照ください。

- [NAT Gateway料金](https://intl.cloud.tencent.com/document/product/1015/30248)
- [EIP料金](https://intl.cloud.tencent.com/document/product/213/17156)
