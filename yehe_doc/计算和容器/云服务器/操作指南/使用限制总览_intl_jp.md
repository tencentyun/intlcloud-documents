## CVM インスタンスの購入に関するアカウント制限

- ユーザーがTencent Cloudアカウントを登録する必要があり、登録ガイドは [Tencent Cloudアカウントの登録](https://intl.cloud.tencent.com/document/product/378/17985)をご参照ください。
- ユーザーが実名認証を行う必要があり、資格認証のガイドは [実名認証の手順](https://intl.cloud.tencent.com/document/product/378/3629)を参照してください。
- 従量課金のCVMを作成する時に、システムは1時間分のホスト費用をフリーズします。費用を支払うため、アカウントに十分な残額があることを確認してください。

## CVM インスタンスの使用制限

- 仮想化ソフトウェアのインストールと再仮想化は、現時点ではサポートされていません（VMwareまたはHyper-Vを使用したインストールなど）。
- 現時点ではサウンドカードアプリケーション、外部ハードウェアデバイス（USBメモリ、外部ハードディスク、銀行のUSBセキュリティーキーなどの直接ロードはサポートしておりません）。
- パブリックネットワークゲートウェイは現在、Linuxシステムのみサポートしています。

## CVMインスタンスの購入制限

- 各ユーザーが各アベイラビリティーゾーンで購入可能な従量課金制のCVMインスタンスの**総数**は、30台または60台とし、CVM購入ページの実際の状況に応じて変化します。
- 詳細については、[CVMインスタンスの購入制限](https://intl.cloud.tencent.com/document/product/213/2664)をご参照ください。


## イメージに関する制限

- 共通イメージの使用に関する制限はありません。
- カスタマイズイメージ：各リージョンに最大10個のカスタマイズイメージまでサポートします。
- 共有イメージ：各カスタマイズイメージに最大50名のTencent Cloudユーザーまで共有でき、同じリージョンのアカウントだけの共有をサポートします。
- 詳細については、 [イメージ種類の制限](https://intl.cloud.tencent.com/document/product/213/4941)をご参照ください。

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
    <th  style = "text-align:center;">計算型C3</th>
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
    <th style = "text-align:center;" >計算型C2</th>
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
     <th class="xl71" x:str style = "text-align:center;">GPU計算型GN6</th>
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
    <th style = "text-align:center;">GPU計算型GN6S</th>
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
    <th style = "text-align:center;">GPU計算型GN7</th>
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
    <th style = "text-align:center;">GPU計算型GN8</th>
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
    <th  style = "text-align:center;">GPU計算型GN10X</th>
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
    <th colspan="2" style = "text-align:center;">Cloud Physical Machine2.0</th>
    <td colspan="10" style = "text-align:center;">ENIのバインドはサポートしていません</td>
   </tr>
  </table>
:::
::: CVMの単一ネットワークカードは、バインドされたプライベートネットワークIPクォータをサポートします
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
    <th  style = "text-align:center;">計算型C3</th>
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
    <th style = "text-align:center;" >計算型C2</th>
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
    <th  style = "text-align:center;">GPU計算型GN2</th>
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
    <th class="xl71" x:str style = "text-align:center;">GPU計算型GN6</th>
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
    <th style = "text-align:center;">GPU計算型GN6S</th>
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
    <th style = "text-align:center;">GPU計算型GN7</th>
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
    <th style = "text-align:center;">GPU計算型GN8</th>
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
    <th  style = "text-align:center;">GPU計算型GN10X</th>
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
    <th colspan="2" style = "text-align:center;">Cloud Physical Machine2.0</th>
    <td colspan="10" style = "text-align:center;">ENIのバインドはサポートしていません</td>
   </tr>
  </table>
:::
</dx-tabs>


## 帯域幅に関する制限

- アウトバウンド帯域幅上限（下り帯域幅）
 - 2020年2月24日00:00以降に作成されたマシンには以下のルールが適用されます。
<table>
<tr><th rowspan="2">ネットワーク課金モード</th><th colspan="2">インスタンス</th><th rowspan="2">設定可能な帯域幅の上限範囲（Mbps）</th></tr>
<tr><th style="width: 18.5607%;">インスタンス課金モード</th><th style="width: 24.5814%;">インスタンス設定</th></tr>
<tr><td>トラフィック課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>帯域幅課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>共有帯域幅</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</table>

 - 2020年2月24日00:00より前に作成されたインスタンスには以下のルールが適用されます。 
<table>
<tr><th rowspan="2">ネットワーク課金モード</th><th colspan="2">インスタンス</th><th rowspan="2">設定可能な帯域幅の上限範囲（Mbps）</th></tr>
<tr><th>インスタンス課金モード</th><th>インスタンス設定</th></tr>
<tr><td>トラフィック課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>帯域幅課金</td><td>従量課金インスタンス</td><td>ALL</td><td>0 - 100</td></tr>
<tr><td>共有帯域幅</td><td colspan="2">ALL</td><td>0 - 2000</td></tr>
</table>


- インバウンド帯域幅の上限（上り帯域幅）：
	- ユーザーが購入した固定の帯域幅は10Mbpsを超える場合、Tencent Cloudは購入した帯域幅と等しい外部ネットワークのインバウンド方向帯域幅をアサインします。
	- ユーザーが購入した固定の帯域幅は10Mbpsより低い場合は、Tencent Cloudは10Mbpsの外部ネットワークのインバウンド方向帯域幅をアサインします。

## ディスクに関する制限

<table>
	<tr><th>制限タイプ</th><th>制限の説明</th></tr>
	<tr><td>エラスティッククラウドディスク機能</td><td>2018年5月以降は、CVMと一緒に購入したデータディスクはすべてエラスティックCBSとなり、CVMからのアンインストールと再マウントに対応します。この機能は、すべての<a href="https://intl.cloud.tencent.com/zh/document/product/213/35071">アベイラビリティーゾーン</a>でサポートされています。</td></tr>
	<tr><td>CBSのパフォーマンス制限</td><td>I/O性能は同時に有効になります。</br>例えば、1TBのSSD CBSの場合、ランダムIOPSの最大値は26,000に達する可能性があります。これは、読み取りIOPSと書き込みIOPSの両方がこの値に達する可能性があることを意味します。同時に、複数のパフォーマンス制限により、この例では使用するblock sizeが4KB/8KBの場合、I/Oは最大IOPS値に達することができますが、使用するblock sizeが16KBの場合、I/Oは最大IOPS値に達することができません（スループットは260MB/秒の制限に達しています）。</td></tr>
	<tr><td>1台のCVMにマウントできるElastic CBSの数は</td><td>最大20個です。</td></tr>
	<tr><td>1つのリージョンでのスナップショットのクォータ</td><td> 64 +リージョンのCBS数* 64（個）。</td></tr>
	<tr><td>CBSがマウントできるCVMの制限事項</td><td>CVMとCBSは同じアベイラビリティーゾーンにある必要があります。</td></tr>
	<tr><td>スナップショットのロールバック制限</td><td> スナップショットデータは、スナップショットが作成されたソースCBSにのみロールバックできます。</td></tr>
	<tr><td>スナップショットでCBSを作成する場合のタイプ制限</td><td>データディスクのスナップショットのみが新しいElastic CBSの作成に使用できます。</td></tr>
	<tr><td>スナップショットで作成されるCBSのサイズ制限</td><td>スナップショットで作成される新しいCBSの容量は、スナップショットCBSの容量以上でなければなりません。</td></tr>
	<tr><td>CBS延滞金の回収</td><td>年額・月額サブスクリプションのエラスティックCBSが、有効期限が切れてから7日以内に更新されない場合、ごみ箱に回収されます。ごみ箱に回収された後、このCBSとCVMは自発的にマウントされません。回収メカニズムの詳細については、<a href="https://intl.cloud.tencent.com/document/product/362/31625">延滞金の説明</a>をご参照ください。 </td></tr>
</table>



## セキュリティグループに関する制限

- セキュリティグループはリージョンに分かれています、1台のCVMは同一地域にあるセキュリティグループのみバインディングすることができます。
- セキュリティグループは[ネットワーク環境](https://intl.cloud.tencent.com/document/product/213/5227)のすべてのCVMインスタンスに適用されます。
- 1つのユーザーは、1つのリージョンでの1プロジェクトに最大50個のセキュリティグループを設定することができます。
- 1つのセキュリティグループはインバウンド方向またはアウトバウンド方向のアクセスポリシーは、最大100件を設定することができます。
- 1つのCVMは複数のセキュリティグループに加えることができ、セキュリティグループは同時に複数のCVMに関連付けることができます。
- **基本ネットワーク**内CVMにバインドされたセキュリティグループ**は、**Tencent Cloudのリレーショナルデータベース（MySQL、MariaDB、SQL Server、PostgreSQL）、NoSQLデータベース（Redis、Memcached）から（またはこれら宛て）のデータパケットをフィルタリングできません。このようなインスタンスのトラフィックをフィルタリングする必要がある場合は、iptablesを使用するか、クラウドファイアウォール製品を購入すると行うことができます。
- 関連するクォータ制限を下表に示します。
</table>
<tr><th>機能の説明</th><th>制限</th></tr>
<tr><td>セキュリティグループ数</td><td>50の/リージョン</td></tr>
<tr><td>セキュリティグループのルール数</td><td>100本の/インバウンド方向、100本の/アウトバウンド方向</td></tr>
<tr><td>1つのセキュリティグループに関連付けられているCVMインスタンス数</td><td>100個</td></tr>
<tr><td>各CVMインスタンスに関連付けることができるセキュリティグループ数</td><td>5个</td></tr>
<tr><td>各セキュリティグループが参照できるセキュリティグループID数</td><td>10个</td></tr>
</table>

## VPCに関する制限

| リソース| 制限（個） |
|---------|---------|
| 各アカウントの各リージョン内のVPC数 | 20 |
| 各VPC内のサブネット数 | 100 |
| 各VPCがサポートする関連付けられている基本ネットワークホスト数 | 100 |
| 1つのVPCにあるルートテーブルの数 | 10 |
| 各サブネットに関連付けられているルーティングテーブル数 | 1 |
| 各ルーティングテーブルのルーティングポリシー数| 50 |
| 各VPCのHAVIPデフォルトクォータ数 | 10 |

