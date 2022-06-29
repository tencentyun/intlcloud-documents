## CVMインスタンス購入アカウントの制限

- ユーザーはTencent Cloudアカウントの登録を行う必要があります。登録ガイドについては、[Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)をご参照ください。
- ユーザーは実名認証が必要です。資格認証ガイドについては、[実名認証ガイド](https://intl.cloud.tencent.com/document/product/378/3629)をご参照ください。
- 従量課金のCVMが作成されると、1時間のホスティング料金が凍結されます。請求書の支払いを行える十分な残高がアカウントにあることを確認してください。

## CVMインスタンスの使用制限

- 仮想化ソフトウェアのインストールと再仮想化は、現時点ではサポートされていません（VMwareやHyper-Vのインストールなど）。
- サウンドカードを使用したり、外部ハードウェアデバイス（USBフラッシュドライブ、外付けディスク、Uキーなど）をマウントしたりすることはできません。
- パブリックネットワークゲートウェイは現在、Linuxシステムのみサポートしています。

## CVMインスタンスの購入制限

- 各ユーザーが各アベイラビリティーゾーンで購入可能な従量課金制のCVMインスタンスの**総数**は、30台または60台とし、CVM購入ページの実際の状況に応じて変化します。
- 詳細については、[CVMインスタンスの購入制限](https://intl.cloud.tencent.com/document/product/213/2664)をご参照ください。


## イメージに関する制限

- パブリックイメージについては、現在は使用上の制限がありません。
- カスタムイメージ：リージョンごとに最大10のカスタムイメージがサポートされます。
- 共有イメージ：カスタムイメージごとに最大50のTencent Cloudユーザーと共有することができます。また、アカウントが同じリージョンにある相手との共有のみをサポートしています。
- 詳細については、[イメージタイプの制限](https://intl.cloud.tencent.com/document/product/213/4941)をご参照ください。


## ネットワークカードに関する制限

CPUとメモリの設定に応じて、CVMにバインドできるENIの数は、単一ネットワークカードにバインドされるプライベートネットワークIPの数とは大きく異なります。ネットワークカードと単一ネットワークカードのIPクォータの数は、次のとおりです。
>! 単一ネットワークカードにバインドされるIPの数は、ネットワークカードにバインドできるIPの数の上限を表すのみで、上限に応じてEIPクォータを提供することを約束するものではありません。アカウントのEIPクォータは、[EIP使用制限](https://intl.cloud.tencent.com/document/product/213/5733)に従って提供されます。

<dx-tabs>
::: CVMはバインドされたENIクォータをサポートします
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
    <td colspan="10" style = "text-align:center;">ENIのバインドはサポートしていません</td>
   </tr>
  </table>
:::
::: CVMの単一ネットワークカードは、バインドされたプライベートIPの数
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
    <td colspan="10" style = "text-align:center;">ENIのバインドはサポートしていません</td>
   </tr>
  </table>
:::
</dx-tabs>


## 帯域幅に関する制限

- アウトバウンド帯域幅上限（ダウンストリーム帯域幅）
 - 2020年2月24日00:00以降に作成されたマシンには以下のルールが適用されます。
<table>
<tr><th rowspan="2">ネットワーク課金モード</th><th colspan="2">インスタンス</th><th rowspan="2">設定可能な帯域幅の上限範囲（Mbps）</th></tr>
<tr><th style="width: 18.5607%;">インスタンス課金モデル</th><th style="width: 24.5814%;">インスタンスの設定</th></tr>
<tr><td>トラフィック課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>帯域幅課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>共有帯域幅</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</table>

 - 2020年2月24日00:00以前に作成されたマシンには以下のルールが適用されます。 
<table>
<tr><th rowspan="2">ネットワーク課金モード</th><th colspan="2">インスタンス</th><th rowspan="2">設定可能な帯域幅の上限範囲（Mbps）</th></tr>
<tr><th>インスタンス課金モデル</th><th>インスタンスの設定</th></tr>
<tr><td>トラフィック課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>帯域幅課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>共有帯域幅</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</table>


- インバウンド帯域幅上限（アップストリーム帯域幅）：
	- ユーザーが購入した固定帯域幅が10Mbpsを超える場合、Tencent Cloudは購入した帯域幅と同じ外部ネットワーク着信帯域幅をアサインします。
	- ユーザーが購入した固定帯域幅が10 Mbps未満の場合、Tencent Cloudは10Mbpsの外部ネットワークのインバウンド方向帯域幅をアサインします。

## ディスクに関する制限

<table>
	<tr><th>制限タイプ</th><th>制限の説明</th></tr>
	<tr><td>エラスティッククラウドディスク機能</td><td>2018年5月以降は、CVMと一緒に購入したデータディスクはすべてエラスティックCBSとなり、CVMからのアンインストールと再マウントに対応します。この機能は、すべての <a href="https://intl.cloud.tencent.com/document/product/213/35071">アベイラビリティーゾーン</a>でサポートされています。</td></tr>
	<tr><td>CBSのパフォーマンス制限</td><td>I/O性能は同時に有効になります。</br>例えば、1TBのSSD CBSの場合、ランダムIOPSの最大値は26,000に達する可能性があります。これは、読み取りIOPSと書き込みIOPSの両方がこの値に達する可能性があることを意味します。同時に、複数のパフォーマンス制限により、この例では使用するblock sizeが4KB/8KBの場合、I/Oは最大IOPS値に達することができますが、使用するblock sizeが16KBの場合、I/Oは最大IOPS値に達することができません（スループットは260MB/秒の制限に達しています）。</td></tr>
	<tr><td>1台のCVMインスタンスにマウントできるエラスティックCBS数</td><td>最大20個。</td></tr>
	<tr><td>1つのリージョンにおけるスナップショットのクォータ</td><td>64 + リージョン内のCBSの数 * 64（個）。</td></tr>
	<tr><td>CBSにマウントできるCVMの制限</td><td>CVMとCBSは同一のアベイラビリティーゾーンになければなりません。</td></tr>
	<tr><td>スナップショットロールバックの制限</td><td>スナップショットデータはスナップショットを作成したCBSにしかロールバックできません。</td></tr>
	<tr><td>スナップショットで作成されるCBSのタイプ制限</td><td>データディスクスナップショットを使用することでのみ、新しいエラスティックCBSを作成することができます。</td></tr>
	<tr><td>スナップショットで作成されるCBSのサイズ制限</td><td>スナップショットで作成される新しいCBSの容量は、スナップショットCBSの容量以上でなければなりません。</td></tr>
</tr>
</table>



## セキュリティグループに関する制限

- セキュリティグループはリージョンを区別します。1つのCVMは同一リージョン内のセキュリティグループにしかバインドできません。
- セキュリティグループは[ネットワーク環境](https://intl.cloud.tencent.com/document/product/213/5227)に存在するあらゆるCVMインスタンスに適用できます。
- 各ユーザーは各リージョンの各プロジェクト下に最大で50個のセキュリティグループを設定することができます。
- 1つのセキュリティグループのインバウンド方向またはアウトバウンド方向のアクセスポリシーは、最大100か条まで設定することができます。
- 1つのCVMは複数のセキュリティグループに加えることができ、セキュリティグループは同時に複数のCVMにバインドすることができます。
- **基本ネットワーク**内CVMにバインドされたセキュリティグループ**は、**Tencent Cloudのリレーショナルデータベース（MySQL、MariaDB、SQL Server、PostgreSQL）、NoSQLデータベース（Redis、Memcached）から（またはこれら宛て）のデータパケットをフィルタリングできません。このようなインスタンスのトラフィックをフィルタリングする必要がある場合は、iptablesを使用するか、クラウドファイアウォール製品を購入すると行うことができます。
- 関連するクォータ制限を下表に示します。
<table>
<tr><th>機能説明</th><th>制限</th></tr>
<tr><td>セキュリティグループ数</td><td>50個/リージョン</td></tr>
<tr><td>セキュリティグループルール数</td><td>100件/インバウンド方向、100件/アウトバウンド方向</td></tr>
<tr><td>各セキュリティグループにバインドできるCVMインスタンス数</td><td>2000個</td></tr>
<tr><td>各CVMインスタンスにバインドすることができるセキュリティグループ数</td><td>5个</td></tr>
<tr><td>各セキュリティグループが参照できるセキュリティグループID数</td><td>10个</td></tr>
</table>

## VPCに関する制限

| リソース| 制限（個） | 
|---------|---------|
| 各アカウントの各リージョン内のVPC数 | 20 | 
| 各VPC内のサブネット数 | 100 |
| 各VPCがサポートする関連付けられている基幹ネットワークホスト数 | 100 |
| 各VPC内のルーティングテーブル数 | 10 |
| 各サブネットに関連付けられているルーティングテーブル数 | 1 |
| 各ルーティングテーブルのルーティングポリシー数| 50 |
| 各VPCのHAVIPデフォルトクォータ数 | 10 |

