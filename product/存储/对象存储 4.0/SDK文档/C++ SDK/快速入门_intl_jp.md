## 開発準備
### 適用システム
現在、このSDKはLinuxプラットフォームにのみ対応します。

### SDKの取得
COSのXML C++ SDKリソースのダウンロードアドレス：[XML C++ SDKダウンロード]（https://github.com/tencentyun/cos-cpp-sdk-v5 "cos-cpp-sdk-v5ダウンロードアドレス"）。
Demoのダウンロードアドレス：[XML C++ SDK Demo](https://github.com/tencentyun/cos-cpp-sdk-v5/blob/master/demo/cos_demo.cpp "Cpp SDK参考")。

### 環境の準備
**スタティックライブラリへの依存：** jsoncpp boost_system boost_thread Poco（libフォルダーにあります）。
**ダイナミックライブラリの依存：** ssl crypto rt z（インストールが必要です）。
SDKではJsonCppのベースおよびヘッダファイルを提供しています。自己インストールする場合、以下の手順によりインストールしたベースをコンパイルしてから、SDKにおける関連ベースとヘッダファイルを置き換えると良いです。上記のベースがシステムにインストールされている場合、SDKにおける関連ベースとヘッダファイルを削除すると良いです。詳しいインストールのステップを以下に示します：

#### 1. CMakeツールをインストールします。
```
yum install -y gcc gcc-c++ make automake
//gccなどの必須プログラムパッケージをインストールします（インストール済みの場合、このステップをスキップしてください）
yum install -y wget

//cmakeのバージョンにつき、3.5以上のバージョンが必要です
wget https://cmake.org/files/v3.5/cmake-3.5.2.tar.gz
tar -zxvf cmake-3.5.2.tar.gz
cd cmake-3.5.2
./bootstrap --prefix=/usr
gmake
gmake install
```

#### 2. ブーストのベースとヘッダファイルをインストールします。
```
wget http://sourceforge.net/projects/boost/files/boost/1.54.0/boost_1_54_0.tar.gz
tar -xzvf boost_1_54_0.tar.gz
cd boost_1_54_0
./bootstrap.sh --prefix=/usr/local
./b2 install --with=all
#ブーストベースは/usr/local/libディレクトリーにインストールされます
```

#### 3. OpenSSLをインストールします。

```
yum install openssl openssl-devel
```

または

```
wget https://www.openssl.org/source/openssl-1.0.1t.tar.gz  
tar -xzvf ./openssl-1.0.1t.tar.gz
cd openssl-1.0.1t/
./config --prefix=/usr/local/ssl --openssldir=/usr/local/ssl

cd /usr/local/
ln -s ssl openssl
echo "/usr/local/openssl/lib" >> /etc/ld.so.conf
ldconfig

# ヘッダファイル/ベースファイルの検索パスを追加します（~/.bashrcに書き込むことができます）
LIBRARY_PATH=/usr/local/ssl/lib/:$LIBRARY_PATH
CPLUS_INCLUDE_PATH=/usr/local/ssl/include/:$CPLUS_INCLUDE_PATH
```

#### 4. [Pocoの公式サイト](https://pocoproject.org/download.html)からPocoのベースとヘッダファイルを取得してインストールします（completeバージョンをダウンロードしてください）。
```
./configure --omit=Data/ODBC,Data/MySQL
make
make install
```

#### 5. コンソールからAPPID、SecretId、SecretKeyを取得します。
>**注意：**
>SecretId、SecretKey、バケットなどの名称の意味と取得方式につき、[COS用語情報](/document/product/436/7751)を参照してください。
>`CMakeList.txt`ファイルの変更により、ローカルBoostヘッダファイルのパスを指定することができます。下記のテキストを変更します： 
```
SET(BOOST_HEADER_DIR "/root/boost_1_61_0")
```

### SDKの構成
[SDKの取得](#sdk-.E8.8E.B7.E5.8F.96)ステップGitHubによるソースコードをダウンロードし、ご利用の開発環境に統合してください。下記のコマンドを実行してください：
``` bash
cd ${cos-cpp-sdk} 
mkdir -p build 
cd build 
cmake .. 
make
```

cos_demo.cppには常用のAPI例があります。生成されたcos_demoをそのまま実行できます。生成された静的ベース名は：libcossdk.a。生成されたlibcossdk.aをご自分のプロジェクトのlibパスに入れ、includeディレクトリーをご自分のプロジェクトのincludeパスにコピーしてください。

## クイックスタート
### 初期化
```
"SecretId":"*********************************", //V5.4.3バージョン以下のsdk構成ファイルにつき、"AccessKey"を使用してください
"SecretKey":"********************************",
"Region":"cn-north",                
//COS地域の正確性を確保してください
"SignExpiredTime":360,              
//署名タイムアウトの時間、単位：s
"ConnectTimeoutInms":6000,          
//connectタイムアウトの時間、単位：ms
"HttpTimeoutInms":60000,            
//httpタイムアウトの時間、単位：ms
"UploadPartSize":1048576,           
//アップロードファイルのパートのサイズ、範囲：1 MB~5 Gb、デフォルトは1 MB
"UploadThreadPoolSize":5,           
//単独ファイルをマルチパートアップロードする際のスレッドプールのサイズ
"DownloadSliceSize":4194304,        
//ダウンロードする際のファイルのパートサイズ
"DownloadThreadPoolSize":5,         
//単独ファイルをダウンロードする際のスレッドプールのサイズ
"AsynThreadPoolSize":2,             
//非同期のアップロード・ダウンロード時のスレッドプールのサイズ
"LogoutType":1,                     
//ログの出力タイプ、0：出力なし、1：画面に出力、2：syslogに出力
"LogLevel":3                     
//ログのレベル、1：ERR、2：WARN、3：INFO、4：DBG
```
### Bucketの作成
```
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    //1. 構成ファイルパスを指定し、CosConfigを初期化します
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    //2. バケット作成のリクエストを構築します
    std::string bucket_name = "cpp_sdk_v5-123456789"; //バケット名
    qcloud_cos::PutBucketReq req(bucket_name);
    qcloud_cos::PutBucketResp resp;
    
    //3. バケットAPIの作成を呼び出します
    qcloud_cos::CosResult result = cos.PutBucket(req, &resp);
    
    //4. 呼び出しの結果を処理します
    if (result.IsSucc()) {
        // 作成完了
    } else {
        //バケットの作成に失敗した場合、CosResultのメンバー関数を呼び出してrequestIDなどのエラー情報を出力することができます
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### ファイルのアップロード
```
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    //1. 構成ファイルパスを指定し、CosConfigを初期化します
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    //2. ファイルのアップロードのリクエストを作成します
    std::string bucket_name = "cpp_sdk_v5-123456789"; //アップロードする目標バケット名
    std::string object_name = "object_name"; //object_nameとはオブジェクト鍵（Key）のことで、バケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名bucket1-1250000000.Cos.ap-guangzhou.myqcloud.com/doc1/pic1.Jpgにおいて、オブジェクト鍵はdoc1/pic1.jpgです。
    //requestの構造関数にローカルファイルのパスを入力する必要があります
    qcloud_cos::PutObjectByFileReq req(bucket_name, object_name, "/path/to/local/file");
    req.SetXCosStorageClass("STANDARD_IA")； //Set方法を呼び出してメタデータなどを設定します
    qcloud_cos::PutObjectByFileResp resp;
    
    //3. ファイルのアップロードAPIを呼び出します
    qcloud_cos::CosResult result = cos.PutObject(req, &resp);
    
    //4. 呼び出しの結果を処理します
    if (result.IsSucc()) {
        //ファイルのアップロード成功
    } else {
        //アップロードに失敗した場合、CosResultのrequestIDなどのメンバー関数を呼び出してエラー情報を出力することができます
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

### ファイルのダウンロード
```
#include "cos_api.h"
#include "cos_sys_config.h"
#include "cos_defines.h"

int main(int argc, char *argv[]) {
    //1. 構成ファイルパスを指定し、CosConfigを初期化します
    qcloud_cos::CosConfig config("./config.json");
    qcloud_cos::CosAPI cos(config);
    
    //2. バケット作成のリクエストを構築します
    std::string bucket_name = "cpp_sdk_v5-123456789"; //アップロードする目標バケット名
    std::string object_name = "object_name"; //object_nameとはオブジェクト鍵（Key）のことで、バケットにおけるオブジェクトの唯一の識別子です。例えば、オブジェクトのアクセスドメイン名bucket1-1250000000.Cos.ap-guangzhou.myqcloud.com/doc1/pic1.Jpgにおいて、オブジェクト鍵はdoc1/pic1.jpgです。
    std::string local_path = "/tmp/object_name";
    //requestはappid、bucketname、objectおよびローカルのパスを提供する必要があります（ファイル名を含みます）
    qcloud_cos::GetObjectByFileReq req(bucket_name, object_name, local_path);
    qcloud_cos::GetObjectByFileResp resp;
    
    //3. バケットAPIの作成を呼び出します
    qcloud_cos::CosResult result = cos.GetObject(req, &resp);
    
    //4. 呼び出しの結果を処理します
    if (result.IsSucc()) {
        //ファイルのダウンロード成功
    } else {
        //ファイルのダウンロードに失敗した場合、CosResultのrequestIDなどのメンバー関数を呼び出してエラー情報を出力することができます
        std::cout << "ErrorInfo=" << result.GetErrorInfo() << std::endl;
        std::cout << "HttpStatus=" << result.GetHttpStatus() << std::endl;
        std::cout << "ErrorCode=" << result.GetErrorCode() << std::endl;
        std::cout << "ErrorMsg=" << result.GetErrorMsg() << std::endl;
        std::cout << "ResourceAddr=" << result.GetResourceAddr() << std::endl;
        std::cout << "XCosRequestId=" << result.GetXCosRequestId() << std::endl;
        std::cout << "XCosTraceId=" << result.GetXCosTraceId() << std::endl;
    }
}
```

