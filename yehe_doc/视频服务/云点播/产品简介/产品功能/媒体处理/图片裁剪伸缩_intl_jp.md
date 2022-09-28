## 機能概要
VOD画像のリアルタイム処理は、サムネイルとトリミングの2つの操作をサポートし、具体的には次のとおりです。
<melo-data data-src="" data-version="2.1.0"></melo-data><table ><colgroup><col  width="301px"><col  width="301px"></colgroup>
<tbody>
<tr>
<th   colspan="1" rowspan="1" align="" valign=""><p>操作タイプ</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>詳細な操作</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="5" align="" valign=""><p>サムネイル</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>幅、高さなどの比を指定してズームします。</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>>高さ、幅などの比を指定してズームします。</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>長辺，短辺などの比を指定してズームします。</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>短辺、長辺などの比を指定してズームします。</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>幅と高さを指定して強制的にズームします。</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="2" align="" valign=""><p>トリミング</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>内接円をトリミングします。トリミング半径を指定します。</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>矩形をトリミングします。トリミングの幅と高さを指定します。</p></td>
</tr>
</tbody>
</table>

 従来の画像編集に比べ、VODの画像のリアルタイム処理は以下の面で優位性があります。
<melo-data data-src="{}" data-version="2.1.0"></melo-data><table ><colgroup><col  width="201px"><col  width="201px"><col  width="201px"></colgroup>
<tbody>
<tr>
<th   colspan="1" rowspan="1" align="" valign=""><p>次元</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>従来の画像編集</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>VOD-画像のリアルタイム処理</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>処理フロー</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>ダウンロード、編集、アップロードなどの複数の手順が必要で、操作に時間と手間がかかる場面。</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>直接クラウドで画像編集のすべてのフローを完了でき、ダウンロードとアップロードの手順を省きます。</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>操作方法</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>画像編集ソフトの使用はハードルが高く、編集者の画像編集能力には一定の要件があります。</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>URLでリアルタイムに画像編集パラメータを指定することによって、操作に着手する障壁をなくします。</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>アクセス速度</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>クラウドストレージリンクによってダウンロード画像にアクセスおよびダウンロードする速度が遅くなり、ユーザー体験に影響を与えます。</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>VOD CDNによってネットワーク全体で配信を高速化し、超高速で処理後の画像を取得します。</p></td>
</tr>
</tbody>
</table>

## 適用ケース
<melo-data data-src="{}" data-version="2.1.0"></melo-data><table ><colgroup><col  width="301px"><col  width="301px"></colgroup>
<tbody>
<tr>
<th   colspan="1" rowspan="1" align="" valign=""><p>シーン</p></td>
 <th   colspan="1" rowspan="1" align="" valign=""><p>説明</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>ユーザーのプロフィール画像</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>ユーザーのプロフィール画像は一般的に同じ解像度で、円形または四角形の画像です。サムネイルとトリミングを使用して要件を実現します。</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>証明書の写真</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>証明書用の写真を撮影する場合は、トリミングし、証明書自体のみを残す必要がある場合があります。</p></td>
 </tr>
<tr>
<td   colspan="1" rowspan="1" align="" valign=""><p>画像のクローズアップ</p></td>
 <td   colspan="1" rowspan="1" align="" valign=""><p>画像内の重要な位置にクローズアップした場合は、クローズアップした部分をトリミングする必要があります。</p></td>
</tr>
</tbody>
</table>

## 使用方法
[画像のリアルタイム処理](https://intl.cloud.tencent.com/document/product/266/42094)をご参照ください。

