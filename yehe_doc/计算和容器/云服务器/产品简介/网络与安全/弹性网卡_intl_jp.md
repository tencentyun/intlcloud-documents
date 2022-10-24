[Elastic Network Interface](https://intl.cloud.tencent.com/products/eni)(ENI)は、VPC上のCVMインスタンスにアタッチできる仮想ネットワークインタフェースであり、インスタンス間で自由に移行できます。ENI は、ネットワークの設定と管理、および信頼性の高いネットワークソリューションの構築の際に非常に役立ちます。

ENI には、VPC、アベイラビリティーゾーン、およびサブネットの属性があり、同じアベイラビリティーゾーン内のCVMインスタンスにのみアタッチすることができます。CVMインスタンスに複数のENIをアタッチでき、アタッチできるENIの最大数はCVMの仕様によって異なります。

## 関連概念

 - **プライマリENIとセカンダリENI：**PCでCVM を作成するときにデフォルトで作成されるネットワークカードはプライマリ ENI であり、ユーザーによって作成されるネットワークカードはセカンダリENIです。プライマリENIはアタッチ／デタッチをサポートしませんが、セカンダリENIはアタッチ／デタッチをサポートします。
 - **プライマリプライベートIP ：**ENIのプライマリプライベートIP は、ENIの作成時にシステムによってランダムに割り当てられるか、ユーザーによってカスタマイズされます。プライマリENIのプライマリプライベートIPを変更できますが、セカンダリENIのプライマリプライベートIP を変更できません。
 - **セカンダリプライベートIP ：**ENI の作成または変更時にユーザーによって構成されます。ユーザーは、セカンダリプライベートIPをアタッチ／デタッチすることができます。
 - **EIP：**EIPとENIのプライベートIPの間に1対1の関連付けを作成します。。
 - **セキュリティグループ：**ENIでは1つ以上のセキュリティグループを関連付けます。
 - **MAC アドレス：**ENI はグローバルに一意のMAC アドレスがあります。

## ユースケース
- **プライベートネットワーク、パブリックネットワーク、管理ネットワーク間の分離**：
重要なビジネスのネットワーク展開は、安全なデータ転送を実現するために、プライベートネットワーク、パブリックネットワーク、および管理ネットワーク間の分離が必要です。さまざまなルーティングポリシーとセキュリティポリシーにより、データセキュリティとネットワーク分離を保証できます。物理サーバーのように、CVMインスタンスに異なるサブネット上の3つのENIをアタッチすることにより、3つのネットワーク間の分離を実現できます。
- **信頼性の高いアプリケーションの展開：**
システムアーキテクチャにおける主要コンポーネントの高可用性は、マルチサーバーホットバックアップによって保証されます。Tencent Cloudは柔軟にアタッチ・デタッチできるENIとプライベートIPを提供します。Keepalived ディザスターリカバリーを設定することにより主要コンポーネントの高可用性展開を実現できます。

## 使用制限

CPUとメモリの構成に基づいて、CVMインスタンスにアタッチできるENIの最大数は、ENI にアタッチできるプライベート IPの最大数とは異なります。ENIと単一のENI IPのクォータ数は以下のとおりです：


<dx-alert infotype="notice" title="">
1つのENI にアタッチする IP の数は、ENI にアタッチできるIPの数の上限を表すのみで、上限に応じてEIPクォータを提供することをお約束するものではありません。アカウントのEIPクォータは、EIP使用制限に従って提供されます。
</dx-alert>


<dx-tabs>
::: CVMインスタンスにアタッチできるENIの数
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
    <th rowspan="4" style = "text-align:center;">コンピューティング型</th>
    <th  style = "text-align:center;">コンピューティング型C4</th>
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
    <th  style = "text-align:center;">コンピューティング型C3</th>
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
    <th style = "text-align:center;" >コンピューティング型C2</th>
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
    <th  style = "text-align:center;">GPUコンピューティング型GN2</th>
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
    <th class="xl71" x:str style = "text-align:center;">GPUコンピューティング型GN6</th>
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
    <th style = "text-align:center;">GPUコンピューティング型GN6S</th>
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
    <th style = "text-align:center;">GPUコンピューティング型GN7</th>
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
    <th style = "text-align:center;">GPUコンピューティング型GN8</th>
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
    <th  style = "text-align:center;">GPUコンピューティング型GN10X</th>
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
    <th style = "text-align:center;">GPUコンピューティング型GN10Xp</th>
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
    <td colspan="10" style = "text-align:center;">ENIのアタッチをサポートしません</td>
   </tr>
  </table>
:::
::: CVMインスタンスの単一のENIにアタッチできるプライベートIPの数
<table>
   <tr>
    <th width="6%"  rowspan="2" style = "text-align:center;">モデル</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">インスタンスタイプ</th>
    <th width="86%" colspan="10" style = "text-align:center;">単一のENIにアタッチできるプライベートIPの数</th>
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
    <th rowspan="4" style = "text-align:center;">コンピューティング型</th>
    <th  style = "text-align:center;">コンピューティング型C4</th>
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
    <th  style = "text-align:center;">コンピューティング型C3</th>
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
    <th style = "text-align:center;" >コンピューティング型C2</th>
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
    <th  style = "text-align:center;">GPUコンピューティング型GN2</th>
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
    <th class="xl71" x:str style = "text-align:center;">GPUコンピューティング型GN6</th>
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
    <th style = "text-align:center;">GPUコンピューティング型GN6S</th>
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
    <th style = "text-align:center;">GPUコンピューティング型GN7</th>
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
    <th style = "text-align:center;">GPUコンピューティング型GN8</th>
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
    <th  style = "text-align:center;">GPUコンピューティング型GN10X</th>
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
    <th style = "text-align:center;">GPUコンピューティング型GN10Xp</th>
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
    <td colspan="10" style = "text-align:center;">ENIのアタッチをサポートしません</td>
   </tr>
  </table>
:::
</dx-tabs>

## APIの概要
ここでENIとCVMに関するAPIインターフェースを次の表に示します。他のENIに関する操作については、[ENI API一覧](https://intl.cloud.tencent.com/document/product/215/15755)をご参照ください。

| インターフェース機能 | Action ID |  機能説明 |
|---------|---------|---------|
| ENIの作成 | [CreateNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15818) |  ENIの作成 |
| プライベートIPアドレスをENIに割り当てる | [AssignPrivateIpAddresses](https://intl.cloud.tencent.com/document/api/215/15813) | プライベートIPアドレスをENIに割り当てる |
| CVMインスタンスへのENIのアタッチ | [AttachNetworkInterface](https://intl.cloud.tencent.com/document/api/215/15819) | CVMインスタンスへのENIのアタッチ|
