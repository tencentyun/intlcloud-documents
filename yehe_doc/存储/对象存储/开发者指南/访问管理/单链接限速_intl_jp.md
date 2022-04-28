## 単一リンクの速度制限

COSではファイルのアップロード、ダウンロードの際のトラフィックを管理し、他のアプリケーションのためのネットワーク帯域幅を確保することができます。[PutObject](https://intl.cloud.tencent.com/document/product/436/7749)、[PostObject](https://intl.cloud.tencent.com/document/product/436/14690)、[GetObject](https://intl.cloud.tencent.com/document/product/436/7753)、[UploadPart](https://intl.cloud.tencent.com/document/product/436/7750)リクエストの際にパラメータx-cos-traffic-limitを付加し、速度制限値を設定すると、COSは設定された速度制限値に基づいて、そのリクエストのネットワーク帯域幅を制御します。

## 利用説明

- ユーザーはPUT Object、POST Object、GET Object、Upload Partリクエストの際にx-cos-traffic-limit リクエストヘッダー（POST Objectリクエストについてはリクエストのフォームフィールド）を付加して、そのリクエストの速度制限値を指定します。このパラメータはheader、リクエストパラメータ内、またはフォームアップロードインターフェースを使用する場合はフォームドメイン内に設定することができます。
- x-cos-traffic-limitパラメータ値は数字でなければならず、単位はデフォルトではbit/sです。
- 速度制限値の範囲は819200～838860800、すなわち100KB/s～100MB/sです。この範囲を超過するとエラーコード400が返されます。
>?単位換算公式：1MByte=1024KByte=1048576Byte=8388608bitです。

## APIの使用例

シンプルアップロードのAPIの例を次に示します。速度制限値は1048576 bit/s、すなわち128KB/sです。

```sh
PUT /exampleobject HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Content-Length: 13
Authorization: q-sign-algorithm=sha1&q-ak=AKID8A0fBVtYFrNm02oY1g1JQQF0c3JO****&q-sign-time=1561109068;1561116268&q-key-time=1561109068;1561116268&q-header-list=content-length;content-md5;content-type;date;host&q-url-param-list=&q-signature=998bfc8836fc205d09e455c14e3d7e623bd2****
x-cos-traffic-limit: 1048576
```

