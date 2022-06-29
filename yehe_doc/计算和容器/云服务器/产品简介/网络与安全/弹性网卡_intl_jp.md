[Elastic Network Interface](https://intl.cloud.tencent.com/products/eni)は、Virtual Private CloudのCVMをバインドする一種のElasticネットワークインターフェースであり、複数のCVMの間で自由にマイグレーションすることができます。ENIはネットワーク管理の設定および信頼性の高いネットワークソリューションの構築に役立ちます。

Elastic NICには、VPC、アベイラビリティーゾーンとサブネットの属性があり、同じアベイラビリティーゾーンのCVMにのみをバインドできます。一台のCVMは複数のENIをバインド可能であり、CVMにバインドできるENIの最大数は、CVMの仕様によって異なります。

## 関連概念

 - **プライマリENIとセカンダリENI：**VPCのCVMで作成されたENIがプライマリENIであり、ユーザーが作成したネットワークカードはセカンダリENIです。プライマリENIはバインドとバインド解除をサポートしませんが、セカンダリENIはバインドとバインド解除をサポートします。
 - **プライマリプライベートIP ：**ENIのプライマリプライベートIP 、ENIが作成される時、システムによってランダムに割り当てられるか、ユーザーによってカスタマイズし、プライマリENIのプライマリプライベートIPを変更できますが、セカンダリENIのプライマリプライベートIP を変更できません。
 - **セカンダリプライベートIP ：**ENI はプライマリ IP 以外にバインドされたセカンダリプライベートIP であり、ENIを作成またはENIを編集する時にユーザーによって設定でき、これらのIPをバインドとバインド解除をサポートします。
 - **EIP：**ENIのプライベートIPと1対1でバインドされます。
 - **セキュリティグループ：**ENIは一つまたは複数のセキュリティグループをバインドできます。
 - **MAC アドレス：**ENI はグローバルに一意のMAC アドレスがあります。

## ユースケース
- **プライベートネットワーク、パブリックネットワーク、管理ネットワーク間の分離**：
重要サービスのネットワーク展開は一般的にデータ転送に使われるプライベートネットワーク、パブリックネットワークと管理ネットワークを分離することを要求します。異なるルーティングポリシーとセキュリティポリシーを使用することにより、データセキュリティとネットワーク分離がを確保します。物理サーバーのように、CVMに異なるサブネットにおける三つのENIをバインドすることにより、三つのネットワーク間の分離を実現できます。
- **信頼性の高いアプリケーションの展開：**
システムアーキテクチャにおける主要コンポーネントの高可用性は、マルチサーバーホットバックアップによって保証されます。Tencent Cloud は柔軟にバインド・バインド解除できるENIとプライベートIPを提供します。keepalivedの災害復帰を設定することにより主要コンポーネントの高可用性デプロイを実現できます。

## 使用制限

CPUとメモリの構成の差異によって、CVMにENIのバインディング数は、単一のENIにプライベートIPのバインディング数と異なり、ENIと単一のENIIPのクォータ数は以下のとおりです：


<dx-alert infotype="notice" title="">
単一のENIにおけるIPのバインディング数はバインディングできるIPの上限を表し、上限に基づいたEIPクォータの提供が約束されないが、アカウントのEIPクォータはEIP使用制限に基づいて提供されます。
</dx-alert>


<dx-tabs>
::: CVMはバインドされたENIクォータをサポートします
<table>
   <tr>
    <th width="6%"  rowspan="2" style = "text-align:center;">モデル</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">インスタンスタイプ</th>
    <th width="86%" colspan="10" style = "text-align:center;">ENIクォータ</th>
   </tr>
   <tr>
    <th style = "text-align:center;">CPU：1コア</th>
    <th style = "text-align:center;">CPU：2コア</th>
    <th style = "text-align:center;">CPU：4コア</th>
    <th style = "text-align:center;">CPU：6コア</th>
    <th style = "text-align:center;">CPU：8コア</th>
    <th style = "text-align:center;">CPU：10コア</th>
    <th style = "text-align:center;">CPU：12コア</th>
    <th style = "text-align:center;">CPU：14コア</th>
    <th style = "text-align:center;">CPU：16コア</th>
    <th style = "text-align:center;">CPU：&gt;16コア</th>
   </tr>
   <tr>
    <th rowspan="9" style = "text-align:center;">標準型</th>
    <th style = "text-align:center;">標準型S5</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準ストレージ拡張型S5se</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準型SA2</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準型S4</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準ネットワーク最適化型SN3ne</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準型S3</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準型SA1</th>
    <td  >2</td>
    <td  >2</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準型S2</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準型S1</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th rowspan="2" style = "text-align:center;">High IO型</th>
    <th style = "text-align:center;">High IO型IT5</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">High IO型IT3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th rowspan="5" style = "text-align:center;">メモリ型</th>
    <th  style = "text-align:center;">メモリ型M5</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">メモリ型M4</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">メモリ型M3</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">メモリ型M2</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">メモリ型M1</th>
    <td  >2</td>
    <td  >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th rowspan="4" style = "text-align:center;">計算型</th>
    <th  style = "text-align:center;">計算型C4</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">コンピューティングネットワーク拡張型CN3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">計算型C3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;" >計算型C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th  rowspan="7" style = "text-align:center;">GPUモデル</th>
    <th  style = "text-align:center;">GPU計算型GN2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr>
    <th class="xl71" x:str style = "text-align:center;">GPU計算型GN6</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">GPU計算型GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
   </tr>
   <tr>
    <th style = "text-align:center;">GPU計算型GN7</th>
    <td  >-</td>
    <td  >-</td>
   <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">GPU計算型GN8</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr>
    <th  style = "text-align:center;">GPU計算型GN10X</th>
   <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >6</td>
      <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">GPU計算型GN10Xp</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">FPGAモデル</th>
    <th style = "text-align:center;">FPGAアクセラレーション型FX4</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
   </tr>
   <tr>
    <th rowspan="3" style = "text-align:center;">ビッグデータ型</th>
    <th  style = "text-align:center;">ビッグデータ型D3</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">ビッグデータ型D2</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">ビッグデータ型D1</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >6</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr>
    <th colspan="2" style = "text-align:center;">Cloud Physical Machine2.0</th>
    <td colspan="10" style = "text-align:center;">ENIのバインドはサポートしていません</td>
   </tr>
  </table>
:::
::: CVMの単一ネットワークカードは、バインドされたプライベートネットワークIPクォータをサポートします
<table>
   <tr>
    <th width="6%"  rowspan="2" style = "text-align:center;">モデル</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">インスタンスタイプ</th>
    <th width="86%" colspan="10" style = "text-align:center;">単一ネットワークカードにプライベートネットワークIPクォータをバインドします</th>
   </tr>
   <tr>
    <th style = "text-align:center;">CPU：1コア</th>
    <th style = "text-align:center;">CPU：2コア</th>
    <th style = "text-align:center;">CPU：4コア</th>
    <th style = "text-align:center;">CPU：6コア</th>
    <th style = "text-align:center;">CPU：8コア</th>
    <th style = "text-align:center;">CPU：10コア</th>
    <th style = "text-align:center;">CPU：12コア</th>
    <th style = "text-align:center;">CPU：14コア</th>
    <th style = "text-align:center;">CPU：16コア</th>
    <th style = "text-align:center;">CPU：&gt;16コア</th>
   </tr>
   <tr>
    <th rowspan="9" style = "text-align:center;">標準型</th>
    <th style = "text-align:center;">標準型S5</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準ストレージ拡張型S5se</th>
    <td  >-</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準型SA2</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準型S4</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準ネットワーク最適化型SN3ne</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準型S3</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準型SA1</th>
    <td >メモリ=1G：2<br/>メモリ&gt;1G：6</td>
    <td  >10</td>
    <td >メモリ=8G：10<br/>メモリ=16G：20</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準型S2</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準型S1</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th rowspan="2" style = "text-align:center;">High IO型</th>
    <th style = "text-align:center;">High IO型IT5</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">High IO型IT3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th rowspan="5" style = "text-align:center;">メモリ型</th>
    <th  style = "text-align:center;">メモリ型M5</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">メモリ型M4</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">メモリ型M3</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">メモリ型M2</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">メモリ型M1</th>
    <td  >6</td>
    <td  >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th rowspan="4" style = "text-align:center;">計算型</th>
    <th  style = "text-align:center;">計算型C4</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">コンピューティングネットワーク拡張型CN3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">計算型C3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;" >計算型C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th  rowspan="7" style = "text-align:center;">GPUモデル</th>
    <th  style = "text-align:center;">GPU計算型GN2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr>
    <th class="xl71" x:str style = "text-align:center;">GPU計算型GN6</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">GPU計算型GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
   </tr>
   <tr>
    <th style = "text-align:center;">GPU計算型GN7</th>
    <td  >-</td>
    <td  >-</td>
   <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">GPU計算型GN8</th>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr>
    <th  style = "text-align:center;">GPU計算型GN10X</th>
   <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >20</td>
      <td  >-</td>
    <td  >-</td>
    <td  >-</td>
     <td  >-</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">GPU計算型GN10Xp</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th style = "text-align:center;">FPGAモデル</th>
    <th style = "text-align:center;">FPGAアクセラレーション型FX4</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
   </tr>
   <tr>
    <th rowspan="3" style = "text-align:center;">ビッグデータ型</th>
    <th  style = "text-align:center;">ビッグデータ型D3</th>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">ビッグデータ型D2</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">ビッグデータ型D1</th>
    <td  >-</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >20</td>
     <td  >-</td>
     <td  >-</td>
     <td  >-</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr>
    <th colspan="2" style = "text-align:center;">Cloud Physical Machine2.0</th>
    <td colspan="10" style = "text-align:center;">ENIのバインドはサポートしていません</td>
   </tr>
  </table>
:::
</dx-tabs>

## APIの概要
ここでENIとCVMに関するAPIインターフェースを次の表に示します。他のENIに関する操作については、[ENI API一覧](https://intl.cloud.tencent.com/document/product/215/15755)をご参照ください。

| インターフェース機能 | Action ID |  機能説明 |
|---------|---------|---------|
| ENIの作成 | [CreateNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15818) |  ENIの作成 |
| ENIがプライベートIP の申請 | [AssignPrivateIpAddresses](https://intl.cloud.tencent.com/document/api/215/15813) | ENIがプライベートIP の申請 |
| CVMにバインドされたENI | [AttachNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15819) | CVMにバインドされたENI |
