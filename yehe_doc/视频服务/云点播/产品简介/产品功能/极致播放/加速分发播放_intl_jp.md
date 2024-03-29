## 概要
VODは世界中に2800以上のCDNアクセラレーションノードを持ち、世界各地のユーザーが最寄りのノードから必要なメディアコンテンツを取得できるため、異なるキャリア間、リージョン間、越境などの要素によるネットワークの不安定さ、アクセス遅延などの問題を防ぎ、メディアダウンロード速度を効率的に速め、スムーズなメディアコンテンツアクセラレーション体験をユーザーに提供することができます。VODには組み込みのデフォルトドメイン名があり、ドメイン名がないユーザーはプリセットされたドメイン名を使用して、位置情報に基づいて最寄りのリージョンから配信されたリソースを取得することにより、再生用のビデオリソースをすばやく取得し、レイテンシーを効果的に低減できます。また、カスタムドメイン名設定管理、パージとプリフェッチ、CDN使用量統計分析もサポートしています。

<table>
    <tr>
        <th style="width:150px">
            機能               
        </th>
				<th>
           説明
        </th>
    </tr>
 <tr>
        <td>
            ドメイン名管理
        </td>
				<td>
            <li>Tencent Cloudドメイン名またはカスタム再生ドメイン名の使用をサポートしています。</li>
						<li>再生ドメイン名ごとに異なるリンク不正アクセス防止および公開ルールの設定をサポートしています。</li>
        </td>
 </tr>
  <tr>
        <td>
            パージとプリフェッチ
        </td>
				<td>
            <li>VODのメディア資産IDまたはURLに対するCDNキャッシュ更新をサポートしています。キャッシュ更新を実行すると、システムはネットワーク全体のCDNノードからリソースの既存キャッシュを削除します。ユーザーリクエストがノードに到達すると、ノードはオリジンサーバーに戻って対応するリソースをプルしてリクエストを返し、リソースをノードにキャッシュすることで、ユーザーが最新のリソースを取得できるようにします。</li>
						<li>VODのメディア資産IDまたはURLに対するCDNコンテンツプリフェッチをサポートしています。プリフェッチを実行すると、リソースはネットワーク全体のCDNノードに保存されます。ユーザーリクエストがノードに到達すると、リソースを直接取得できるようになるため、応答時間を短縮できます。</li>
        </td>
 </tr>
 <tr>
        <td>
            CDN使用量統計分析
        </td>
				<td>
				<li>CDNのトラフィック、帯域幅、クリック数の統計分析サービスをご提供しています。また、それらはすべて時間、リージョン、キャリアごとに確認することができます。</li>
				<li>メディアファイル粒度の統計分析サービスを提供し、ビデオごとの再生回数および再生トラフィックの確認をサポートしています。</li>
				<li>アクセスドメイン名のアクセス状況を示すCDNログをダウンロードできます。</li>
        </td>
 </tr>
</table>

## 適用ケース
VODアクセラレーション配信再生は、ソーシャルプラットフォーム、eコマース、ビデオプラットフォーム、ニュースサイト、フォーラムなどの、画像やオーディオビデオメディアコンテンツの表示を必要とするほぼすべてのオンラインシーンに適用できます。世界中に分布する大量のCDNアクセラレーションノードにより、複雑なネットワーク環境の中でも高品質なメディアコンテンツアクセスサービスを提供することが可能です。いくつかの適用シーンについてご説明します。

<table>
    <tr>
        <th style="width:150px">
            シーン               
        </th>
				<th>
           説明
        </th>
    </tr>
	 <tr>
        <td>
            ソーシャルプラットフォーム
        </td>
				<td>
				ユーザー層は様々な地域、国にわたる可能性があり、使用するキャリアも、ネットワーク品質も様々です。VODのCDN再生の際に、動的アクセラレーションなどの最適化ポリシーにより、ユーザーに最適なリンクを自動的に探し出して使用することで、スムーズな再生体験を提供することが可能になります。
        </td>
 </tr>
 <tr>
        <td>
            eコマースプラットフォーム
        </td>
				<td>
            ショップは商品の画像、オーディオビデオをアップロードし、顧客は購入・使用後に画像やオーディオビデオをアップロードして評価を行います。VODのCDNアクセラレーション配信により、画像やオーディオビデオを高速でロードすることができ、ユーザーのアクセスおよびショッピング体験をより素晴らしいものにすることができます。
        </td>
 </tr>
 <tr>
        <td>
            ビデオプラットフォーム
        </td>
				<td>
           長時間のビデオが多く、ファイルのボリュームが大きいものが多いため、ネットワークにより高い安定性が求められます。VODのCDN再生により、脆弱なネットワーク環境でも安定したスムーズな視聴が可能になります。
        </td>
 </tr>
  <tr>
        <td>
            ニュースサイト
        </td>
				<td>
            ホットなニュースが大量のユーザーのもとに届くと、トラフィックは瞬く間に爆発的に増加します。ユーザーがニュース画像やオーディオビデオを見るためにオリジンサーバーに直接アクセスすると、オリジンサーバーのクラッシュを引き起こしたり、それによって注目度が薄れてしまったりする場合があります。メディアコンテンツをVODにホストすることで、VOD CDNの世界中のキャッシュノードを介してユーザーがメディアコンテンツをスピーディーに取得でき、スムーズなブラウズ体験を楽しむことができるようになります。
        </td>
 </tr>
</table>

## 使用方法
ドメイン名管理については以下をご参照ください。
- [カスタムドメイン名](https://intl.cloud.tencent.com/document/product/266/35572)
- [ドメイン名管理](https://intl.cloud.tencent.com/document/product/266/14057)
- [CNAMEの設定](https://intl.cloud.tencent.com/document/product/266/42076)
- [デフォルト配信設定](https://intl.cloud.tencent.com/document/product/266/35768)

パージとプリフェッチについては以下をご参照ください。
- [パージとプリフェッチ](https://intl.cloud.tencent.com/document/product/266/33899)

使用量統計分析については以下をご参照ください。
- [使用量の統計](https://intl.cloud.tencent.com/document/product/266/30421)
- [データ分析](https://intl.cloud.tencent.com/document/product/266/30422)
- [ログのダウンロード](https://intl.cloud.tencent.com/document/product/266/7983)
