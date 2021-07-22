お客様のドメイン名がCSSに接続されると、システムでは自動的にCNAMEドメイン名が割り当てられます（サフィックス .liveplay.myqcloud.com を付加）。ドメイン名サービスプロバイダでCNAMEの設定を完了するまで、CNAMEドメイン名に直接アクセスすることはできません。設定が有効になると、すぐにCSSサービスをご利用いただけます。再生ドメイン名とプッシュドメイン名は、どちらもCNAME解析を完了する必要があります。

## 注意事項
- ドメイン名解析プロバイダにアクセスして、CNAMEレコードを設定してください。具体的な操作については、お客様のドメイン名解決プロバイダにお問い合わせください。
- 以下は、Tencent Cloud、Alibaba Cloud、Baidu Cloud、DNSPod、HiChina、およびXinnetでCNAMEドメイン名解析を設定する場合の例であり、操作手順はあくまでも一例です。実際の設定と異なる場合は、それぞれのDNSプロバイダの情報をご参照ください。

## 前提条件
CSSコンソールにログインし、[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)に進んでドメイン名リストを表示し、ドメイン名のCNAMEアドレスを取得します。


## Tencent Cloudの設定方法
DNSプロバイダがTencent Cloudの場合は、下記の手順でCNAMEレコードを追加できます。
1. [ドメイン名サービスコンソール](https://console.cloud.tencent.com/domain)にログインします。
2. CNAMEを追加する必要のあるドメイン名を選択し、【解析】をクリックします。
3. 指定したドメイン名のドメイン名解析ページに進み、【レコードの追加】をクリックします。
4. 新しく追加した列で、ホストレコードとしてドメイン名プレフィックスを入力し、レコードタイプはCNAMEを選択し、レコード値としてCNAMEドメイン名を入力します。
	- レコードタイプ：`CNAME`を選択します。
	- ホストレコード：サブドメイン名のプレフィックスを入力します。再生ドメイン名がplay.myqcloud.comの場合は、 `play` を追加します。メインドメイン名のmyqloud.comを直接解析する必要がある場合は、`@`を入力します。ワイルドカードドメイン名を解決する必要がある場合は、`\*` を入力します。
	- 解析ルート：「デフォルト」を選択することをお勧めします。
	- レコード値：Tencent Cloudコンソールの[【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)のドメイン名に対応するCNAME値を、 `domain.livecdn.liveplay.myqcloud.com` の形式で入力します。
	- TTL：10分間と入力することをお勧めします。
5. 【保存】をクリックすれば完了です。

6. CNAMEが有効であることを検証します。CNAMEの設定が完了してから、約15分後に有効になります。CSS [【Domain Management】](https://console.cloud.tencent.com/live/domainmanage)のドメイン名に対応するCNAME値 ![](https://main.qcloudimg.com/raw/bd92cce6703d3703582c0c2a194fd866.png) が表示されたら、CNAMEは成功です。CNAMEの設定が完了してから長時間経っても成功が表示されない場合は、 [CNAME設定時の問題箇所の特定](https://intl.cloud.tencent.com/document/product/267/32478#.E9.85.8D.E7.BD.AE.E5.AE.8C.E6.88.90-cname-.E5.90.8E.EF.BC.8C.E4.BE.9D.E6.97.A7.E6.98.BE.E7.A4.BA-cname-.E6.9C.AA.E9.85.8D.E7.BD.AE.E6.98.AF.E4.BB.80.E4.B9.88.E5.8E.9F.E5.9B.A0.EF.BC.9F) をご参照ください。


## Alibaba Cloud設定方法
お客様のDNSプロバイダがAlibaba Cloudであり、ドメイン名のICP登録が完了している場合は、次の手順を参照してCNAMEを設定することができます。

1. Alibaba Cloudコンソールにログインし、【クラウド解析DNS】>[【ドメイン名解析】](https://dns.console.aliyun.com/#/dns/domainList)に進みます。
2. CNAMEを追加する必要のあるドメイン名を選択し、【解析設定】をクリックします。
3. 【レコードの追加】を選択し、レコードの追加ページで次の設定を行います。
	-  レコードタイプ： `CNAME`を選択します。
	- ホストレコード：サブドメイン名のプレフィックスを入力します。再生ドメイン名がplay.myqcloud.comの場合は、 `play` を追加します。メインドメイン名のmyqloud.comを直接解析する必要がある場合は、`@`を入力します。ワイルドカードドメイン名を解析する必要がある場合は、`\*` を入力します。
	- 解析ルート：`デフォルト`を選択することをお勧めします。
	-  レコード値：Tencent Cloudコンソールのドメイン名管理ページのドメイン名に対応するCNAME値を、 `domain.livecdn.liveplay.myqcloud.com` の形式で入力します。
	- TTL：10分間`と入力することをお勧めします。
4. 【OK】をクリックすれば完了です。

4. CNAMEが有効であることを検証します。CNAMEは、設定が完了してから約15分後に有効になります。CSS [Domain Management](https://console.cloud.tencent.com/live/domainmanage)のドメイン名に対応するCNAME値 ![](https://main.qcloudimg.com/raw/ca12667bfcfd9716639c27d51f3beed3.png) が表示されたら、CNAMEは成功です。CNAMEの設定が完了してから長時間経っても成功が表示されない場合は、[CNAME設定時の問題箇所の特定](https://intl.cloud.tencent.com/document/product/267/32478#.E9.85.8D.E7.BD.AE.E5.AE.8C.E6.88.90-cname-.E5.90.8E.EF.BC.8C.E4.BE.9D.E6.97.A7.E6.98.BE.E7.A4.BA-cname-.E6.9C.AA.E9.85.8D.E7.BD.AE.E6.98.AF.E4.BB.80.E4.B9.88.E5.8E.9F.E5.9B.A0.EF.BC.9F) をご参照ください。

>このドキュメントの説明は、2019年10月31日のAlibaba Cloudバージョンに基づいています。Alibaba Cloudコンソールが更新されても、このドキュメントは更新されませんので、説明パスに従ってご自身で調整を行ってください。設定が成功しない場合は、 [カスタマサービスに連絡](https://intl.cloud.tencent.com/support)してください。

## Baidu Cloudの設定方法
お客様のドメイン名サービスプロバイダがBaidu Cloudであり、ドメイン名のICP申告が完了している場合は、次の手順を参照してCNAMEを設定することができます。
1. Baidu Cloudコンソールにログインし、[【Domain Management】](https://console.bce.baidu.com/bcd/?_=1550137564099#/bcd/manage/list)を選択し、ドメイン名の管理リストページに進みます。
2. CSSで追加したドメイン名を選択し、操作列で【解析】をクリックしてDNS解析ページに進みます。
3. 解析レコードを追加し、このページで次の設定を行います。
 - ホストレコード：セカンドレベルドメイン名、すなわちドメイン名プレフィックスを入力します。再生ドメイン名がplay.myqcloud.comの場合は、 `play` を追加します。メインドメイン名であるmyqloud.comを直接解析する必要がある場合は、 `@` を入力します。ワイルドカードドメイン名を解析する必要がある場合は、 `\*` を入力します。
 - レコードタイプ：`CNAMEレコード`を選択します。
 - 解析ルート：`デフォルト`を選択することをお勧めします。
 -  レコード値：CSSコンソールのドメイン名管理ページのドメイン名に対応するCNAME値を、 `domain.livecdn.liveplay.myqcloud.com` の形式で入力します。
 - TTL：10分間`と入力することをお勧めします。
4. 【OK】をクリックして送信します。

5. CNAMEが有効であることを検証します。CNAMEは、設定が完了してから約15分後に有効になります。CSSのドメイン名の管理のドメイン名に対応するCNAME値 ![](https://main.qcloudimg.com/raw/bd92cce6703d3703582c0c2a194fd866.png) が表示されたら、CNAMEは成功です。CNAMEの設定が完了してから長時間経っても成功が表示されない場合は、[CNAME設定時の問題箇所の特定](https://intl.cloud.tencent.com/document/product/267/32478#.E9.85.8D.E7.BD.AE.E5.AE.8C.E6.88.90-cname-.E5.90.8E.EF.BC.8C.E4.BE.9D.E6.97.A7.E6.98.BE.E7.A4.BA-cname-.E6.9C.AA.E9.85.8D.E7.BD.AE.E6.98.AF.E4.BB.80.E4.B9.88.E5.8E.9F.E5.9B.A0.EF.BC.9F)をご参照ください。

>このドキュメントの説明は、2019年3月1日のBaidu Cloudバージョンに基づいています。Baidu Cloudコンソールが更新されても、このドキュメントは更新されませんので、説明パスに従ってご自身で調整を行ってください。設定が成功しない場合は、 [カスタマサービスに連絡](https://intl.cloud.tencent.com/support)してください。

## DNSPodでの構成方法
DNSプロバイダがDNSPodの場合は、下記の手順でCNAMEレコードを追加できます。


## HiChinaでの構成方法
DNSプロバイダがHiChinaの場合は、下記の手順でCNAMEレコードを追加できます。



## Xinnetでの設定方法
DNSプロバイダがXinnetの場合は、下記の手順でCNAMEレコードを追加できます。


## CNAMEのアクティブ化状態を確認
DNSプロバイダが異なると、CNAMEが有効になるまでの時間もわずかに異なりますが、通常は30分以内に有効になります。コマンドラインでdigまたはnslookupコマンドを使用して、CNAMEが有効かどうかをクエリーすることもできます。サフィックスが.myqcloud.comのドメイン名を見つけた時にはすでにCNAMEのドメイン名は有効になっています。

