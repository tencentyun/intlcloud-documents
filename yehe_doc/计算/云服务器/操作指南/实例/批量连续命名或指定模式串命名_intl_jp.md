## ユースケース

複数のインスタンスを作成する際、インスタンスの名称に規則性を持たせたい場合、我々はインスタンスの一括作成後、サフィックス数字の自動昇順機能及び指定パターン文字列機能を提供しています。購入、またはTencentCloud APIを通じて実現できます。

- ｎ個のインスタンスを購入し、「CVM+序数」のようなインスタンス名称を生成したい際は（つまりインスタンスの名称が CVM1、CVM2、CVM3 となる）、 [サフィックス数字の自動昇順](#AutoAscending) 機能を通じて実現できます。
- ｎ個のインスタンスを作成し、なおかつインスタンスの序数がｘからカウントしたい際、[単一パターン文字列指定](#SpecifySingleString) 機能を通じて実現できます。
- ｎ個の複数のプレフィックスを有するインスタンスを作成し、なおかつ全てのインスタンスのプレフィックスに序数が指定されていることを望む際、[複数パターン文字列指定](#SpecifyMultipleStrings) 機能を通じて実現できます。


## 操作手順

<span id="AutoAscending"></span>
### サフィックス数字の自動昇順

複数購入したインスタンスを同じプレフィックスで、序数がインクリメントするのみの名称に設定できます。
>作成したインスタンスのデフォルトの序数は1からインクリメントし、最初の序数を指定することはできません。
>
以下の操作は三台のインスタンスを購入し、生成したインスタンスの名称に「CVM+序数」（すなわちインスタンスの名称は CVM1、CVM2 和 CVM3となる）を希望した際の例です。

#### 購入ページでの操作

1.  [インスタンスの作成](http://intl.cloud.tencent.com/document/product/213/4855) を参照して、3台のインスタンスを購入し、「2.ホスト設定」の中で**「プレフィックス+序数」**の命名規則でインスタンスの名称を記入し、すなわちインスタンス名称を `CVM`と記入します。下図に示す通り：
![](https://main.qcloudimg.com/raw/9815074c0fde0f3dbc7f0b9f4504d7e3.png)
2. ページの提示に基づき操作を進め、支払いを完了させる。
4.  [CVMコンソール](https://console.cloud.tencent.com/cvm/index)に戻り、 新しく作成されたインスタンスを確認します。すなわち一括購入したインスタンスのプレフィックスが同じで、序数がインクリメントされていることを確認できます。下図に示す通り：
![](https://main.qcloudimg.com/raw/34057be61529702cc287db4a971865d3.png)

#### API操作

TencentCloud API [RunInstances](https://intl.cloud.tencent.com/document/api/213/15730) で InstanceName フィールドを `CVM`と指定します。

### パターン文字列の指定

一括購入したインスタンスを複雑、かつ序数を指定したインスタンス名称に設定できます。インスタンス名称は単一、もしくは複数のパターン文字列設定をサポートし、インスタンス名称を設定するときは、実際の需要に応じて設定を行ってください。

パターン文字列指定の命名：**{R:x}**、x で生成したインスタンスのデフォルト序数を表示する。

<span id="SpecifySingleString"></span>
#### 単一パターン文字列の指定

以下の操作では3台のインスタンスを作成し、序数を3からインクリメントするように例を作ります。

##### 購入ページでの操作

1.  [インスタンスの作成](http://intl.cloud.tencent.com/document/product/213/4855) を参照してインスタンスを購入し、「2.ホスト設定」の中で**「プレフィックス+パターン文字列指定{R:x}」**という命名規則でインスタンスの名称を記入し、すなわちインスタンス名称を `CVM{R:x}`と記入します。下図に示す通り：
![](https://main.qcloudimg.com/raw/1b06d1bdf95e10afdd7dfde39e3a7e11.png)
2. ページの提示に基づき操作を進め、支払いを完了させる。
3.  [CVMコンソール](https://console.cloud.tencent.com/cvm/index)に戻り、 新しく作成されたインスタンスを確認し、すなわち一括購入したインスタンスのプレフィックスが同じで、序数が3からインクリメントされていることを確認できます。下図に示す通り：
![](https://main.qcloudimg.com/raw/69d59d2523a9fc27a5b58d61070cfe21.png)

##### API操作

TencentCloud API [RunInstances](https://intl.cloud.tencent.com/document/api/213/15730) で InstanceName フィールドを `CVM{R:3}`と指定します。

<span id="SpecifyMultipleStrings"></span>
#### 複数パターン文字列の指定

以下の操作例は、3台のインスタンスを作成し、インスタンス名称に cvm、 Big 、 test プレフィックスを含み、かつ cvm と Big プレフィックスの後に序数を付け、序数はそれぞれ13と2からインクリメントします（すなわちインスタンス名称は cvm13-Big2-test、cvm14-Big3-test、cvm15-Big4-testとなる）。

##### 購入ページでの操作

1.  [インスタンスの作成](http://intl.cloud.tencent.com/document/product/213/4855) を参照してインスタンスを３台購入し、「2.ホスト設定」の中で**「プレフィックス+パターン文字列指定{R:x}-プレフィックス+パターン文字列指定{R:x}-プレフィックス」**という命名規則でインスタンスの名称を記入し、すなわちインスタンス名称を `cvm{R:13}-Big{R:2}-test` と記入します。下図に示す通り：
![](https://main.qcloudimg.com/raw/6704d8309016c2406c51d3a3b99b6883.png)
2. ページの提示に基づき操作を進め、支払いを完了させる。
3.  [CVMコンソール](https://console.cloud.tencent.com/cvm/index)に戻り、 新しく作成されたインスタンスを確認し、すなわち一括購入したインスタンスのプレフィックスが指定された序数からインクリメントされていることを確認できます。下図に示す通り：
![](https://main.qcloudimg.com/raw/2d6980c90ab552c911bdf16197c685f9.png)

##### API操作

 TencentCloud API [RunInstances](https://intl.cloud.tencent.com/document/api/213/15730) で、 InstanceName フィールドを ` cvm{R:13}-Big{R:2}-test`と指定します。

