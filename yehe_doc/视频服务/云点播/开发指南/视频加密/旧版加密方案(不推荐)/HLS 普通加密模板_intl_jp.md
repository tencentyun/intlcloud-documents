VODトランスコードプラットフォームがビデオに対してHLS共通暗号化を実行すると、復号キーを取得するためのURLがM3U8ビデオファイルの`EXT-X-KEY`タグに書き込まれます。詳細については、[HLS共通暗号化](https://intl.cloud.tencent.com/document/product/266/33968)をご参照ください。

HLS共通暗号化テンプレートには、`definition`（一意のテンプレートID）と`get_key_url`（復号キーを取得するためのURL）パラメータが含まれています。<!--api HLS共通暗号化テンプレートを追加、変更またはクエリーする必要がある場合は、次のHLS共通暗号化テンプレート管理APIをご参照ください。

* [HLS共通暗号化テンプレートの作成](https://intl.cloud.tencent.com/document/product/266/35167)
* [HLS共通暗号化テンプレートの更新](https://intl.cloud.tencent.com/document/product/266/35168)
* [HLS共通暗号化テンプレートのクエリー](https://intl.cloud.tencent.com/document/product/266/35169)

>?HLS共通暗号化テンプレート管理は、VOD API 2017インターフェースのみを提供しています。
