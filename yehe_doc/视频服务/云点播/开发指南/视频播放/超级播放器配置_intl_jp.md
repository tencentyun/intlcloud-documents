Super Playerを使用してVODビデオを再生する場合は、ビデオ**画像コンテンツ**は [アダプティブビットレートストリーミングへのトランスコード](https://intl.cloud.tencent.com/document/product/266/33942) での出力となり、**サムネイル**プレビューは [スプライトイメージ](https://intl.cloud.tencent.com/document/product/266/33940) での出力となります。
ビデオを同時に複数のアダプティブビットレートストリーミングとスプライトイメージに変換して出力する場合は、以下を指定する必要があります。

* どのアダプティブビットレートストリーミングを再生するか。
* どのスプライトイメージを使用してサムネイルにするか。

アダプティブビットレートストリーミングには、解像度の切り替え時に異なる解像度名に対応する複数のサブストリームが含まれます。プレーヤーに表示される各サブストリームの解像度名を指定する場合は、サブストリームの解像度名の命名規則を指定する必要があります。

## プレーヤー設定項目

VODは、**ABSテンプレートID** と**スプライトイメージテンプレートID**を指定することができる、**Super Player設定**を提供しています。また、Super Player設定では、各サブストリームの**解像度命名規則**（LD、SD、HDなど）をカスタマイズすることもできます。

| 設定項目 | 設定方法 | 機能 |
| -- | -- | -- |
| 再生用のアダプティブビットレートストリーミング | アダプティブビットレートストリーミングテンプレートID | プレーヤーで 再生されるコンテンツを制御します |
| サムネイルプレビュー用のスプライトイメージ | スプライトイメージテンプレートID | プログレスバーに表示されるサムネイルを制御します |
| プレーヤー表示用のサブストリームの解像度名 | サブストリーム短辺の長さに対する命名 | 解像度切り替え時の各解像度名を制御します |

## プリセット設定
便利にご使用いただくために、VODは次の2つのプリセット設定を提供します。

<table class="table auto-table"><tbody><tr ><th rowspan="2">設定名</td><th colspan="3">設定項目</td></th>
<tr><th>再生するアダプティブビットレートストリーミング（テンプレートID）はどれか</td><th>使用するスプライトイメージ（テンプレートID）はどれか</td><th>解像度の命名規則（サブストリームの短辺の長さによる命名）</td></tr>
<tr><td>default</td><td>10</td><td>10</td><td rowspan="2"><ul style="margin:0;"><li >240px：LD</li><li>480px：SD</li><li>720px：HD</li><li>1080px：FHD</li><li>1440px：2K</li><li>2160px：4K</li><li>その他：<code>xx</code>p（<code>xx</code>短辺の長さを表します）</li></td></tr>
<tr><td>basicDrmPreset</td><td>12</td><td>10</td>
</tbody></table>

* ビデオコンテンツの暗号化が必要ない場合は、プリセットのタスクフローLongVideoPresetを使用してアダプティブビットレートストリーミングに変換して出力し、その後、プリセットされたSuper Playerを使用してdefaultの再生を設定できます。具体例については、 [アクセスガイド](https://intl.cloud.tencent.com/document/product/266/38098) をご参照ください。
* 暗号化されたコンテンツを再生する必要がある場合は、プリセットのタスクフローSimpleAesEncryptPresetを使用して、アダプティブビットレートストリーミングに変換して出力し、その後、プリセットされたSuper Playerを使用してbasicDrmPresetの再生を設定できます。具体例については [アクセスガイド](https://intl.cloud.tencent.com/document/product/266/38294)をご参照ください。

## カスタマイズ設定
プリセットされたSuper Playerの設定のほかにも、 [コンソール](https://intl.cloud.tencent.com/document/product/266/38261) または [API](https://intl.cloud.tencent.com/document/product/266/37567) を介して設定をカスタマイズすることができます。
カスタマイズされたSuper Playerを使用して再生を設定します。具体例については [アクセスガイド](https://intl.cloud.tencent.com/document/product/266/38098)をご参照ください。

## 使用設定
プリセット設定されたdefault以外の設定を使用してビデオを再生する場合は、 [Super Player署名](https://intl.cloud.tencent.com/document/product/266/38099)を使用し、署名パラメータの`pcfg`パラメータで使用する設定名を指定する必要があります。
Super Player署名を使用してビデオを再生します。具体例については [アクセスガイド](https://intl.cloud.tencent.com/document/product/266/38098)をご参照ください。
