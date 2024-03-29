## イメージとは何ですか。
Tencent Cloudイメージは、Cloud Virtual Machine（CVM）インスタンスの起動に必要なすべての情報を提供します。必要なイメージを指定した場合、このイメージから必要な任意の数のインスタンスを起動できます。必要に応じて任意の複数の異なるイメージからインスタンスを起動することもできます。わかりやすく言えば、イメージとはつまり、CVMの「インストールディスク」です。

## イメージタイプ
Tencent Cloud は、次のタイプのイメージを提供します。
- **パブリックイメージ：**すべてのユーザーが使用可能です。大部分の主流オペレーティングシステムをカバーしています。
- **カスタムイメージ：**実行中のインスタンスから作成するか、外部ソースからインポートできます。
- **共有イメージ：**その他のユーザーによって共有されるイメージです。インスタンスを作成するためにのみ使用されます。

イメージタイプの詳細については [イメージタイプの概要](https://intl.cloud.tencent.com/document/product/213/4941)をご参照ください。

## イメージの課金方法[](id:mirrorBilling)
使用したイメージに対して課金される場合があります。課金の詳細については、[課金概要](https://intl.cloud.tencent.com/document/product/213/2179)をご参照ください。

## イメージを利用したデプロイと手動デプロイ

<table style="width:717px;">
<thead>
<tr>
<th style="width:85px;height:45px;position:relative;font-weight:700;" valign="top"><div style="position:absolute;width:1px;height:102px;top:0;left:0;background-color: #d9d9d9;transform: rotate(-55deg);transform-origin:top;"></div><div style="position:relative;left:30px">方式</div><div style="position:relative;left:-10px">比較項目</th>
<th><strong>イメージデプロイ</strong></th>
<th><strong>手動デプロイ</strong></th>
</tr>
</thead>
<tbody><tr>
<td>デプロイ時間</td>
<td>3分間 ～ 5分間</td>
<td>1日 ～ 2日</td>
</tr>
<tr>
<td>デプロイのプロセス</td>
<td>成熟したサービスマーケットソリューションまたはすでに使われているソリューションに基づき、迅速に適切なCVMを作成します。</td>
<td>適切なオペレーティングシステム、データベース、アプリケーションソフトウェア、プラグインなどを選択します。インストールおよびデバッグが必要です。</td>
</tr>
<tr>
<td>セキュリティ</td>
<td>パブリックイメージとカスタムイメージは、Tencent Cloud によってテストおよび監査されています。共有イメージのソースは、ユーザーが自分で選別する必要があります。</td>
<td>開発デプロイメンバーのレベルへの依存。</td>
</tr>
<tr>
<td>適用ケース</td>
<td>パブリックイメージ：パブリックイメージ：Tencent Cloudが提供する初期化されたコンポーネントをを含む正規版のOSです。<br>カスタムイメージ：既存のCVMと同じソフトウェア環境を迅速に作成します。または環境のバックアップを実行します。<br>共有イメージ：その他のユーザーの既存のCVMと同じソフトウェア環境を迅速に作成します。</td>
<td>基本設定を提供せずに、自分で CVM を構成します。</td>
</tr>
</tbody></table>

## イメージアプリケーション
 - **特定のソフトウェア環境のデプロイ**
共有イメージ、カスタムイメージを使用すると、特定のソフトウェア環境を迅速に作成する助けになります。自ら行なう環境設定、ソフトウェアのインストールなどの煩雑で時間がかかる作業を回避し、サイト構築、アプリケーションの開発、可視化管理など複数の個別化ニーズを満たします。「開けばすぐに使える」CVMは、時間の節約になり便利です。
 - **ソフトウェア環境の一括デプロイ**
すでに環境をデプロイしたCVMインスタンスでイメージを作成し、CVMインスタンスをバッチ作成する際、そのイメージをオペレーティングシステムに使用し、CVMインスタンスの作成が完了すると、それまでのCVMインスタンスと一致するソフトウェア環境が得られます。これらにより、ソフトウェア環境を一括デプロイする目的を達成します。
 - **サーバーランタイム環境のバックアップ**
CVM インスタンスのイメージを作成して、実行中の環境をバックアップできます。ソフトウェア環境が破損しCVM インスタンが正常に動かなくなってしまった場合、このイメージを使用して環境を回復できます。

## イメージのライフサイクル

下図はカスタムイメージのライフサイクルをまとめたものです。新しいカスタムイメージを作成あるいはインポート後に、ユーザーはそれを新しいインスタンスの起動に使用することができます（ユーザーは既存のパブリックイメージからインスタンスを起動することもできます）。カスタムイメージが同じアカウントのその他のリージョンにコピーされると、そのリージョンで独立したイメージになることができます。ユーザーはカスタムイメージを、その他のユーザーと共有することもできます。
![](https://qcloudimg.tencent-cloud.cn/raw/fc696f071652956e00c62c273fc5dde3.png)

