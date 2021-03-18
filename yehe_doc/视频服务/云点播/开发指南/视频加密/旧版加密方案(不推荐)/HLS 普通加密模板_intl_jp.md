VODトランスコードプラットフォームがビデオに対してHLS共通暗号化を実行すると、復号キーを取得するためのURLがM3U8ビデオファイルの`EXT-X-KEY`タグに書き込まれます。詳細については、[HLS共通暗号化](https://intl.cloud.tencent.com/document/product/266/33968)をご参照ください。

HLS共通暗号化テンプレートには、`definition`（一意のテンプレートID）と`get_key_url`（復号キーを取得するためのURL）パラメータが含まれています。
