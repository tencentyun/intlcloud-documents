## CVM インスタンスの購入に関するアカウント制限

- ユーザーはTencent Cloudアカウントの登録を行う必要があります。登録ガイドについては、[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)をご参照ください。
- 従量課金のCVMが作成されると、システムは1時間分のCVM使用料をデポジットとしてアカウント残高に凍結され、 請求書の支払いを行うための十分な資金がアカウントにあることを確認する必要があります。

## CVMインスタンスの使用制限

- 仮想化ソフトウェアのインストールと再仮想化は、現時点ではサポートされていません（VMwareやHyper-Vのインストールなど）。
- サウンドカードを使用したり、外部ハードウェアデバイス（USBフラッシュドライブ、外付けディスク、 USBトークンなど）をマウントしたりすることはできません。
- パブリックゲートウェイは現在、Linuxシステムのみをサポートしています。

## CVMインスタンスの購入制限

- 各ユーザーが各アベイラビリティーゾーンで購入可能な従量課金制のCVMインスタンスの**総数**は30台～ 60台です。購入可能数は、CVM購入ページにアクセスして確認してください。
- 詳細については、[CVMインスタンスの購入制限](https://intl.cloud.tencent.com/document/product/213/2664)をご参照ください。


## イメージの使用に関する制限

- パブリックイメージ：使用制限なし。
- カスタムイメージ：リージョンごとに最大10のカスタムイメージがサポートされます。
- 共有イメージ：各カスタムイメージは、最大50人のTencent Cloudユーザーと共有することができます。カスタムイメージは、ソースアカウントと同じリージョンのアカウントとのみ共有できます。
- 詳細については、[イメージの種類](https://intl.cloud.tencent.com/document/product/213/4941)をご参照ください。

## ENI 制限

CPUとメモリの構成に基づいて、CVMインスタンスにアタッチできるENIの最大数は、ENIにアタッチできるプライベートIPの最大数とは異なります。ENIと単一のENI IPのクォータ数は以下のとおりです：
>! 1つのENI にアタッチする IP の数は、ENIにアタッチできるIPの数の上限を表すのみで、上限に応じてEIPクォータを提供することをお約束するものではありません。アカウントのEIPクォータは、[EIP使用制限](https://intl.cloud.tencent.com/document/product/213/5733)に従って提供されます。

<dx-tabs>
::: CVMインスタンスにアタッチできるENIの数
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">モデル</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">インスタンスタイプ</th>
    <th width="86%" colspan="10" style = "text-align:center;">ENIクォータ</th>
   </tr>
   <tr >
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
   <tr >
    <th rowspan="9" style = "text-align:center;">標準型</th>
    <th style = "text-align:center;">標準型S5</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">標準ストレージ拡張型S5se</th>
    <td >-</td>
    <td >-</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">標準型SA2</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">標準型S4</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準ネットワーク最適化型SN3ne</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >8</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">標準型S3</th>
    <td >2</td>
    <td >4</td>
    <td >4</td>
    <td >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">標準型SA1</th>
    <td >2</td>
    <td >2</td>
    <td >4</td>
    <td >-</td>
    <td >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">標準型S2</th>
    <td >2</td>
    <td >4</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
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
   <tr >
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
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr >
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
   <tr >
    <th style = "text-align:center;">メモリ型M4</th>
    <td >2</td>
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
   <tr >
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
   <tr >
    <th style = "text-align:center;">コンピューティングネットワーク拡張型CN3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >8</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">コンピューティング型C3</th>
    <td  >-</td>
    <td >-</td>
    <td >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;" >コンピューティング型C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >8</td>
    <td  >8</td>
   </tr>
   <tr >
    <th  rowspan="6" style = "text-align:center;">GPUモデル</th>
     <th class="xl71" x:str style = "text-align:center;">GPUコンピューティング型GN6</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >8</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPUコンピューティング型GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >4</td>
    <td  >-</td>
    <td  >6</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPUコンピューティング型GN7</th>
    <td >-</td>
    <td >-</td>
   <td  >4</td>
    <td >-</td>
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
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >8</td>
    <td  >-</td>
    <td  >8</td>
   </tr>
   <tr >
    <th  style = "text-align:center;">GPUコンピューティング型GN10X</th>
   <td >-</td>
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
   <tr >
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
    <td >8</td>
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
   <tr >
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
   <tr >
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
   <tr >
    <th style = "text-align:center;">ビッグデータ型D1</th>
    <td >-</td>
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
   <tr >
    <th colspan="2" style = "text-align:center;">ベアメタル型CVM</th>
    <td colspan="10" style = "text-align:center;">ENIをアタッチすることはできません</td>
   </tr>
  </table>
:::
::: CVMインスタンスの単一のENIにアタッチできるプライベートIPの数
<table >
   <tr >
    <th width="6%"  rowspan="2" style = "text-align:center;">モデル</th>
    <th  width="8%"  rowspan="2" style = "text-align:center;">インスタンスタイプ</th>
    <th width="86%" colspan="10" style = "text-align:center;">単一ネットワークカードにプライベートネットワークIPクォータをバインドします</th>
   </tr>
   <tr >
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
   <tr >
    <th rowspan="9" style = "text-align:center;">標準型</th>
    <th style = "text-align:center;">標準型S5</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">標準ストレージ拡張型S5se</th>
    <td >-</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">標準型SA2</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">標準型S4</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr>
    <th style = "text-align:center;">標準ネットワーク最適化型SN3ne</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >30</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">標準型S3</th>
    <td >6</td>
    <td >10</td>
    <td >10</td>
    <td >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">標準型SA1</th>
    <td >メモリ=1G：2<br/>メモリ&gt;1G：6</td>
    <td >10</td>
    <td >メモリ=8G：10<br/>メモリ=16G：20</td>
    <td >-</td>
    <td >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">標準型S2</th>
    <td >6</td>
    <td >10</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
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
   <tr >
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
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr >
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
   <tr >
    <th style = "text-align:center;">メモリ型M4</th>
    <td >6</td>
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
   <tr >
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
   <tr >
    <th style = "text-align:center;">コンピューティングネットワーク拡張型CN3</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >30</td>
   </tr>
   <tr  >
    <th  style = "text-align:center;">コンピューティング型C3</th>
    <td  >-</td>
    <td >-</td>
    <td >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;" >コンピューティング型C2</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td  >-</td>
    <td  >-</td>
    <td  >-</td>
    <td >30</td>
    <td  >30</td>
   </tr>
   <tr >
    <th  rowspan="7" style = "text-align:center;">GPUモデル</th>
    <th  style = "text-align:center;">GPUコンピューティング型GN2</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
   </tr>
   <tr >
    <th class="xl71" x:str style = "text-align:center;">GPUコンピューティング型GN6</th>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >30</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPUコンピューティング型GN6S</th>
    <td  >-</td>
    <td  >-</td>
    <td  >10</td>
    <td  >-</td>
    <td  >20</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
    <td >-</td>
   </tr>
   <tr >
    <th style = "text-align:center;">GPUコンピューティング型GN7</th>
    <td >-</td>
    <td >-</td>
   <td  >10</td>
    <td >-</td>
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
    <td >-</td>
    <td  >-</td>
    <td  >-</td>
    <td  >30</td>
    <td  >-</td>
    <td  >30</td>
   </tr>
   <tr >
    <th  style = "text-align:center;">GPUコンピューティング型GN10X</th>
   <td >-</td>
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
   <tr >
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
    <td >30</td>
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
   <tr >
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
   <tr >
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
   <tr >
    <th style = "text-align:center;">ビッグデータ型D1</th>
    <td >-</td>
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
   <tr >
    <th colspan="2" style = "text-align:center;">ベアメタル型CVM</th>
    <td colspan="10" style = "text-align:center;">ENIをアタッチすることはできません</td>
   </tr>
  </table>
:::
</dx-tabs>


## 帯域幅制限

- アウトバウンド帯域幅の上限 (ダウンストリーム帯域幅)：
 - 次のルールは、2020年2月24日00:00以降に作成されたインスタンスに適用されます。
<table>
<tr><th rowspan="2">ネットワーク課金モデル</th><th colspan="2">インスタンス</th><th rowspan="2">帯域幅設定範囲（Mbps）</th></tr>
<tr><th style="width: 18.5607%;">インスタンス課金モデル</th><th style="width: 24.5814%;">インスタンスの設定</th></tr>
<tr><td>トラフィック課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>帯域幅課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>共有帯域幅</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</table>

 - 次のルールは、2020年2月24日00:00より前に作成されたインスタンスに適用されます。 
<table>
<tr><th rowspan="2">ネットワーク課金モデル</th><th colspan="2">インスタンス</th><th rowspan="2">帯域幅設定範囲（Mbps）</th></tr>
<tr><th>インスタンス課金モデル</th><th>インスタンスの設定</th></tr>
<tr><td>トラフィック課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>帯域幅課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>共有帯域幅</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</table>


- インバウンド帯域幅の上限（アップストリーム帯域幅）：
	- ユーザーが購入した固定帯域幅が10Mbpsを超える場合、Tencent Cloudは購入した帯域幅に等しいパブリックネットワークインバウンド帯域幅を割り当てます。
	- ユーザーが購入した固定帯域幅が10Mbps未満の場合、Tencent Cloudは10Mbpsのパブリックネットワークインバウンド帯域幅を割り当てます。

## ディスクに関する制限

<table>
	<tr><th>制限タイプ</th><th>制限の説明</th></tr>
	<tr><td>エラスティッククラウドディスク機能</td><td>2018年5月以降、CVMインスタンスと一緒に購入したデータディスクはすべてエラスティッククラウドディスクとなり、CVMからのアンインストールと再マウントに対応します。この機能は、すべての<a href="https://intl.cloud.tencent.com/document/product/213/35071">アベイラビリティーゾーン</a>でサポートされています。</td></tr>
	<tr><td>クラウドディスクのパフォーマンス制限</td><td>I/O 仕様は、入力と出力の両方のパフォーマンスに同時に適用されます。</br>例えば、1TB SSDの最大ランダムIOPSが26,000の場合、読み取りと書き込みの両方のパフォーマンスがこの値に達する可能性があることを意味します。同時に、複数のパフォーマンス制限により、この例では使用するブロックサイズが4KBまたは8KBの場合、IOPSは最大26,000 IOPSに達する可能性があります。ブロックサイズが16KBの場合、I/Oは最大IOPS値に達することはできません (スループットは既に260MB/秒の制限に達しています)。</td></tr>
	<tr><td>単一CVMインスタンスにアタッチできるエラスティッククラウドディスクの数</td><td>最大20個。</td></tr>
	<tr><td>1つのリージョンにおけるスナップショットのクォータ</td><td>64 + リージョン内のクラウドディスクの数 * 64（個）。</td></tr>
	<tr><td>クラウドディスクをCVMインスタンスにアタッチするための前提条件</td><td>CVM インスタンスとクラウドディスクは、同じアベイラビリティゾーンにある必要があります。</td></tr>
	<tr><td>スナップショットロールバックの制限</td><td>スナップショットデータは、スナップショットが作成されたクラウドディスクにのみロールバックできます。</td></tr>
	<tr><td>スナップショットを使用したクラウドディスクの作成 - タイプ制限</td><td>データディスクのスナップショットのみが新しいエラスティッククラウドディスクの作成に使用できます。</td></tr>
	<tr><td>スナップショットを使用したクラウドディスクの作成 - サイズ制限</td><td>スナップショットを使用して新しいクラウドディスクを作成する場合は、新しいクラウドディスクの容量は、スナップショットのソースディスクより大きくする必要があります。</td></tr>
</tr>
</table>



## セキュリティグループに関する制限

- CVMインスタンスは、同じリージョン内のセキュリティグループにのみ関連付けることができます。
- セキュリティグループは、あらゆる [ネットワーク環境](https://intl.cloud.tencent.com/document/product/213/5227) におけるCVMインスタンスに適用できます。
- 各ユーザーは各リージョンの各プロジェクト下に最大で50個のセキュリティグループを設定することができます。
- セキュリティグループには、最大100 個のインバウンドまたはアウトバウンドルールを構成することができます。
- 1つのCVMインスタンスを複数のセキュリティグループに関連付けることができ、1つのセキュリティグループを複数のCVMインスタンスに関連付けることができます。
- クラシックネットワーク上のCVMインスタンスに関連付けられたセキュリティグループは、Tencent Cloudのリレーショナルデータベース（MySQL、MariaDB、SQL Server、PostgreSQL）、NoSQLデータベース（Redis、Memcached）から（またはこれら宛て）のデータパケットをフィルタリングできません。このようなインスタンスのトラフィックをフィルタリングする必要がある場合は、iptablesを使用するか、クラウドファイアウォール製品を購入すると行うことができます。
- 関連するクォータ制限を下表に示します。
<table>
<tr><th>機能説明</th><th>制限</th></tr>
<tr><td>セキュリティグループ数</td><td>50個/リージョン</td></tr>
<tr><td>セキュリティグループごとのルール数</td><td>100件/インバウンド方向、100件/アウトバウンド方向</td></tr>
<tr><td>各セキュリティグループに関連付けることができるCVMインスタンスの数</td><td>2000個</td></tr>
<tr><td>各CVMインスタンスに関連付けることができるセキュリティグループの数</td><td>5个</td></tr>
<tr><td>各セキュリティグループが参照できるセキュリティグループID数</td><td>10个</td></tr>
</table>

## VPCに関する制限

| リソース| 制限（個） | 
|---------|---------|
| 各アカウントの各リージョン内のVPC数 | 20 | 
| 各VPC内のサブネット数 | 100 |
| 各VPCに関連付けることができるクラシックネットワークタイプのCVMインスタンスの数 | 100 |
| 各VPC内のルーティングテーブル数 | 10 |
| 各サブネットに関連付けることができるルーティングテーブル数 | 1 |
| 各ルーティングテーブルのルーティングポリシー数| 50 |
| 各VPCのHAVIPデフォルトクォータ数 | 10 |

