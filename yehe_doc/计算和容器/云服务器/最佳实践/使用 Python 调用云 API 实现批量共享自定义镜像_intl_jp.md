## 操作步骤
このドキュメントでは、Python SDKを使用してAPIを呼び出し、サブユーザーを通じてCVMのカスタムイメージを一括でまとめて共有する方法について説明します。同様のニーズがある場合、またはSDKの使用方法を知りたい場合は、このドキュメントをご覧ください。


## 前提条件[](id:preconditions)
- サブユーザーを作成しました。そのサブユーザーは CVM およびクラウド APIに対するすべての権限を持ちます。 
 - サブユーザーの作成方法については、 [サブユーザーの作成](https://intl.cloud.tencent.com/document/product/598/13674)をご参照ください。
 - サブユーザーに権限を付与する方法については、[サブユーザー権限の設定](https://intl.cloud.tencent.com/document/product/598/32650)をご参照ください。このドキュメントでは、サブユーザーに `QcloudCVMFullAccess`と `QcloudAPIFullAccess` のプリセットポリシーを付与します。
 - サブユーザーの SecretId と SecretKey を作成します。操作手順については、[アクセスキー](https://intl.cloud.tencent.com/document/product/598/32675)をご参照ください。作成したSecretId と SecretKeyを適切に保存する必要があります。
- 共有するカスタムイメージがあります。カスタムイメージを作成する必要がある場合は、 [カスタムイメージの作成](https://intl.cloud.tencent.com/document/product/213/4942)をご参照ください。


## 操作手順

### Pythonのインストール
1. 次のコマンドを実行して、Python 3.6 以降が現在のCVMインスタンスにインストールされているかどうかを確認します。インストールされている場合は、このステップをスキップしてください。
```shellsession
python --version
```
2.  CVMインスタンスに Python がインストールされていない場合。
 - CentOS 上の CVM インスタンスの場合は、次のコマンドを実行して Python をインストールします。
```shellsession
yum install python3
```
 - Ubuntu または Debian上のCVM インスタンスの場合は、次のコマンドを実行して Python をインストールします。
```shellsession
sudo apt install python3
```
 - 他のOS上の CVM インスタンスの場合は、 [Python 公式ウェブサイト](https://www.python.org/doc/)にアクセスし、Python 3.6 以降をダウンロードし、インストールパッケージを Linux サーバーにアップロードし、パッケージを解凍してPython をインストールします。
3. インストールが完了したら、次のコマンドを実行して Python のバージョンを確認します。
```shellsession
python --version
```

### コード作成
1. ターゲットマシン上に `test.py` ファイルを作成し、次のコードを入力します。
```python
import json
from tencentcloud.common import credential
from tencentcloud.common.profile.client_profile import ClientProfile
from tencentcloud.common.profile.http_profile import HttpProfile
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cvm.v20170312 import cvm_client, models

# デフォルトでは、環境変数 TENCENTCLOUD_SECRET_ID および TENCENTCLOUD_SECRET_KEY を読み取り、secretId および SecretKey を取得します。
# 認証情報の管理方法の詳細については、https://github.com/TencentCloud/tencentcloud-sdk-python#%E5%87%AD%E8%AF%81%E7%AE%A1%E7%90%86をご覧ください
cred = credential.EnvironmentVariableCredential().get_credential()
httpProfile = HttpProfile()
httpProfile.endpoint = "cvm.tencentcloudapi.com"
clientProfile = ClientProfile()
clientProfile.httpProfile = httpProfile

# この例では南京が使用されています。 実際の状況に応じてリージョンを変更します。 たとえば、上海の場合、リージョンを「ap-shanghai」に変更します。
aria = 'ap-nanjing'
client = cvm_client.CvmClient(cred,aria, clientProfile)
def img_share(img_id,img_name,accountids):
    try:
        req1 = models.ModifyImageSharePermissionRequest()
        params1 = {
            "ImageId": img_id,
            "AccountIds": accountids,
            "Permission": "SHARE"
        }
        req1.from_json_string(json.dumps(params1))

        resp1 = client.ModifyImageSharePermission(req1)
        response1 = json.loads(resp1.to_json_string())
        print(img_name,'共有成功！',response1)
    except TencentCloudSDKException as err:
        print(img_name,'共有失敗!',err)
try:
    req = models.DescribeImagesRequest()
    params = {
        "Filters": [
            {
                "Name": "image-type",
                "Values": ["PRIVATE_IMAGE"]
            }
        ],
        "Limit": 100
    }
    req.from_json_string(json.dumps(params))
    resp = client.DescribeImages(req)
    response = json.loads(resp.to_json_string())
    img_num = response["TotalCount"]
    print('イメージリストを取得中....')
    share_config = input('1.すべてのイメージを共有します\n\n2.. 共有するイメージを決定します\n\n1 または 2 を入力して Enter キーを押します。 デフォルト値: 2：') or '2'
    accountids = input('イメージを共有するユーザーの UIN を入力し、複数のUINをカンマで区切ってください：').split(",")
    for i in range(img_num):
        basic = response['ImageSet'][i]
        img_id = basic['ImageId']
        img_name = basic['ImageName']
        if share_config == '1':
            img_share(img_id,img_name,accountids)
        elif share_config == '2':
            print('イメージID：',img_id,'イメージ名：',img_name)
            share_choice = input('このイメージを共有するかどうか y/n:') or 'y'
            if share_choice == 'y':
                img_share(img_id,img_name,accountids)
            elif share_choice == 'n':
                continue
            else:
                print('正しいオプションを入力してください！！')
        else:
            print('正しいオプションを入力してください！！')

except TencentCloudSDKException as err:
    print(err)
```
 - **SecretId と SecretKey**： [前提条件](#preconditions) で作成したサブユーザーのSecretIdとSecretKey に置き換えてください。
 - **aria**：共有するカスタムイメージが存在する実際のリージョンに置き換えてください。詳細については、[共通パラメータ ](https://www.tencentcloud.com/document/product/213/31574)をご覧ください。
2. ターゲットマシンで次のコマンドを実行してコードを実行します。



画面上の指示に従って1または2を入力(すべてのイメージを同時に共有するか、イメージを 1 つずつ選択して共有するかを選択)、ピアアカウントIDを入力します。ピアアカウント所有者に [アカウント情報](https://console.cloud.tencent.com/developer)ページに移動してアカウントIDを取得するように通知できます。
イメージが正常に共有されると、対応する数の RequestID が返されます。

## 関連する API ドキュメント
このドキュメントで使用されるAPIは[DescribeImages](https://intl.cloud.tencent.com/document/product/213/33272) と [ModifyImageSharePermission](https://www.tencentcloud.com/document/product/213/33268)です。