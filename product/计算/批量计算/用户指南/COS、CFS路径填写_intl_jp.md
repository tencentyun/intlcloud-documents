## 概要情報

Batchでのログ実行（StdOut、StdErr）およびリモートストレージマッピングはすべてCOS/CFSパスを記入することに関わりますが、これはhttp方式でCOS bucketやファイルにアクセスするのとは少し違います。詳細は下記をご覧ください。

## 1. COSパスの説明

### COS XML APIアクセスドメイン名のみがサポートされます

![](https://main.qcloudimg.com/raw/0af010fcd27c428f7a3cbb3d1b69affa.png)

COSでサポートされるアクセスドメイン名には、XML APIとJSON APIに適用される2つのタイプが含まれます。上図の赤いボックスで示されているように、Batchは記入するとき、XML API形式のドメイン名のみをサポートします。

### 接頭辞はcos://で始まる必要があります

![](https://main.qcloudimg.com/raw/ef19923ec04d89da175c90ed56232d01.png)

例えば、上図のアドレスは、Batchのパスを記入する場合に、接頭辞cos://を追加する必要があります。具体的な形式は次のとおりです

``` 
cos://testbatch-1252462967.cos.ap-beijing-1.myqcloud.com/ 
```

``注意：/で終わる必要があります``

### サブディレクトリをマウントします

![](https://main.qcloudimg.com/raw/127aaa3874563e5e7cef7e1eab2448d4.png)

サブディレクトリは、通常のファイルディレクトリの方式でBucketドメイン名の後ろに直接追加すればよいです。例えば、上図のBucketのフォルダです。ディレクトリをマウントするとき、COSパスは次のように記入されます

``` 
cos://testbatch-1252462967.cos.ap-beijing-1.myqcloud.com/testdir/ 
```

### 同じ地域のBucketをサポートします

COSは地域属性があるものであり、データをストレージとCVM間で最も効率的に転送できるように、BatchジョブがCOS Bucketと同じ地域にあることを保証する必要があります。

## 2. CFSパスの説明

リモートストレージマッピングでは、自動マウントCFS/NASパスをローカルパスに構成できます。

![](https://main.qcloudimg.com/raw/cc269aa87bc6faf265acdccd50acf793.png)

### 接頭辞はcfs://またはnfs://で始まる必要があります

例えば、上図のアドレスは、Batchのパスを記入する場合に、接頭辞cfs://やnfs://を追加する必要があります。具体的な形式は次のとおりです

``` 
cfs://10.66.140.208/ 
```

``注意：/で終わり、CFS/NASとBatchのジョブが同じネットワークに構成されていることを保証する必要があります``








