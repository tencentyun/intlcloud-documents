DjangoはオープンソースコードのWebアプリケーションフレームワークであり、Pythonで書き込みます。
この課程ではデフォルトのDjangoサイトを、稼働しているPython2.7のCVMにどうやってデプロイするかを説明します。

使用するソフトウェア環境：CentOS7.2 | Python2.7 | Django1.11

### 手順1：CVMインスタンスにログイン
CVMの購入とアクセスについては[Linux CVMのカスタマイズ設定](https://intl.cloud.tencent.com/document/product/213/10517)をご参照ください。

### 手順2：Pythonのインストール
CentOSではデフォルトでPythonをインストールし、`python --version`によってPythonのバージョンを確認することができます。

### 手順3：Djangoのインストール
1. pipをインストールします。
```
yum install python-pip 
```
2. pipパッケージを更新させます。
```
pip install --upgrade pip
```
2. pipを介してDjangoをインストールします。
```
pip install Django==1.11
```
3. Djangoバージョンを確認して、Djangoのインストールが完了したかをテストします。
```
python # pythonのコマンドラインに入る
>>> import django
>>> django.VERSION
```

### 手順4：MySQLdbモジュールのインストール
MySQLのサポートモジュールをインストールします。
```
yum install python-devel
yum install mysql-devel
yum -y install mysql-devel libxml2 libxml2-dev libxslt* zlib gcc openssl
yum install gcc libffi-devel python-devel openssl-devel
pip install MySQL-python
```

### 手順5：Apacheサービスのインストール
1. CVMインスタンスで`yum`を使用してApacheをインストールします。
```
yum install httpd -y
```
2. Apacheサービスを起動します。
```
service httpd start
```
3. Apacheをテストします。
>この手順ではCVMがセキュリティグループにおいて、ソースを**all**に設定し、ポートプロトコルを**TCP:80**のインバウンドルールにします。セキュリティグループの設定方法については[セキュリティグループ操作](https://intl.cloud.tencent.com/document/product/213/12452)をご参照ください。
>
ローカルのブラウザに`http://xxx.xxx.xxx.xxx/`（このうち`xxx.xxx.xxx.xxx`はCVMの公式サイトのIPアドレス）を入力し、下の画面が現れたら、Apacheの起動に成功しています。
![](https://main.qcloudimg.com/raw/a8708d09de9280c730f47eb8289f7c47.png)

### 手順6：Apacheのmod_wsgi拡張をDjangoのアプリケーションコンテナとしてインストールします。
1. httpd-develをインストールします。
```
yum install -y httpd-devel
```
2. mod_wsgiをインストールします。
```
yum install -y mod_wsgi
```

### 手順7：プロジェクトテストDjango環境の作成
1. `/usr/local`下でプロジェクト項目を作成し、`django-admin.py startproject projectname`を稼働して1つのプロジェクトを作成し、このうちprojectnameをプロジェクト名とします。
```
cd /usr/local
django-admin.py startproject projectname
```
2. **プロジェクトルートディレクトリ**では`django.wsgi`ファイルを新規作成してApacheとしてサポートします。
```
cd /usr/local/projectname
vim django.wsgi
```
3. `django.wsgi`に以下の内容を入力します。
```
import os
import sys
from django.core.wsgi import get_wsgi_application
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(__file__)), '.'))
os.environ['DJANGO_SETTINGS_MODULE'] = 'projectname.settings'
application = get_wsgi_application()
```
4. Apacheサポートを追加し、`httpd.conf`に以下の内容を追加します。`httpd.conf`のパスは`/etc/httpd/conf/httpd.conf`です。
```
LoadModule wsgi_module modules/mod_wsgi.so
WSGIScriptAlias /python "/usr/local/projectname/django.wsgi"
<Directory "/usr/local/projectname">
    AllowOverride None
    Options None
    Require all granted
</Directory>
<Directory "/usr/local/projectname">
    AllowOverride None
    Options None
    Require all granted
</Directory>
```
5. ビューの作成には、**プロジェクトディレクトリ**`/usr/local/projectname/projectname`下で`view.py`ファイルを作成してアクセスの入り口とします。コンテンツは以下のとおりです。
```
from django.http import HttpResponse
def hello(request):
       return HttpResponse("Hello world ! ")
```
6. 設定URLについては、**プロジェクト名ディレクトリ**`/usr/local/projectname/projectname`下の`urls.py`ファイルを設定し、当初のコンテンツを削除します。追加内容は次のとおりです。
```
from django.conf.urls import *
from projectname.view import hello
urlpatterns = [
    url(r'^hello/$',hello),
]
```
7. **プロジェクトディレクトリ**`/usr/local/projectname/projectname`下の`settings.py`ファイルを修正します。
```
ALLOWED_HOSTS = ['*']
```
8. Apacheサービスを再起動します。
```
service httpd restart
```
9. ローカルブラウザに`http://xxx.xxx.xxx.xxx/python/hello`（このうち`xxx.xxx.xxx.xxx`はCVMの公式サイトIPのアドレス）を入力し、画面に「Hello world !」と表示されたらプロジェクト環境の作成に成功しています。

### 手順8：DjangoにTemcemtDB（オプション）を設定
1. プロジェクトディレクトリ下の`settings.py`ファイルを設定します。
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'mysql',
        'USER': 'root', # TencentDB アカウント名
        'PASSWORD': '123456', # TencentDB アカウントパスワード
        'HOST': '0.0.0.0', # TencentDB 内部ネットアドレス
        'PORT': '3306', # TencentDB ポート
    }
}
```
2. 設定完了後、以下のコマンドを使用してデータベースの接続をテストできます。
```
$python manage.py validate/check
```
3. テストに合格するとデータベースの操作が可能になります。より多くのデータベースの操作については[モデルとデータベース](https://docs.djangoproject.com/en/1.11/topics/db/)をご参照ください。
