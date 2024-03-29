## 概要

COSコンソールから、バケットにアップロードされた単一または複数のオブジェクトをコピーすることができ、ソースパスからターゲットパスへのオブジェクトのコピーが可能になります。

>?
> - CASタイプのオブジェクトに対するコピー＆ペーストはサポートされていません。
> - 標準ストレージ（マルチAZ）は、現時点では標準ストレージ（マルチAZ）タイプとしてコピーすることのみをサポートしており、標準ストレージ、低頻度およびアーカイブストレージタイプとしてコピーすることをサポートしていません。
> - 低頻度ストレージ（マルチAZ）タイプは、現時点では低頻度ストレージ（マルチAZ）タイプとしてコピーすることのみをサポートしており、標準ストレージ、低頻度およびアーカイブストレージタイプとしてコピーすることをサポートしていません。
> - サブアカウントでオブジェクトをコピーするには、PutObject、GetObject、GetObjectACLという3つの権限が必要です。
> 

## 操作手順

1. [COSコンソール](https://console.cloud.tencent.com/cos5)にログインします。
2. 左側ナビゲーションバーで**バケットリスト**をクリックし、バケットリストページに進みます。
3. 対応するバケットを見つけ、そのバケット名をクリックし、バケットのファイルリストページに進みます。
4. コピーしたいオブジェクトやフォルダを選択し（複数選択も可能です）、上方の**その他の操作 > コピー**をクリックします。
5. コピーに成功したと表示されたら、ターゲットパスを選択し、上方の**その他の操作 > 貼り付け**をクリックすれば貼り付けることができます。
例えば、バケットexamplebucket1-1250000000の下にあるtargetフォルダに貼り付けます。
![](https://main.qcloudimg.com/raw/c5ced94c2d09085efb55bf39a87a258b.png)
>! ターゲットパスをソースパスと同じにすることはできません。同じにした場合、貼り付けが失敗します。
>

