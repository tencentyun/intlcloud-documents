Django is an open-source web application framework written in Python.
This tutorial describes how to deploy the default Django website to a CVM instance where Python 2.7 runs.

Software environments used here include CentOS 7.2, Python 2.7, and Django 1.11.

### Step 1. Log in to the CVM instance
For more information on how to purchase and access CVM instances, please see [Getting Started with Linux CVM](https://intl.cloud.tencent.com/document/product/213/2936).

### Step 2. Install Python
Python is installed in CentOS by default. You can view the Python version by running `python --version`.

### Step 3. Install Django
1. Install pip.
```
yum install python-pip 
```
2. Update the pip package.
```
pip install --upgrade pip
```
2. Install Django through pip.
```
pip install Django==1.11
```
3. View the Django version to see whether the installation is successful.
```
python # Enter the Python command line
>>> import django
>>> django.VERSION
```

### Step 4. Install the MySQLdb module
Install the supporting modules of MySQL.
```
yum install python-devel
yum install mysql-devel
pip install MySQL-python
```

### Step 5. Install the Apache service
1. Install Apache in the CVM instance with `yum`.
```
yum install httpd -y
```
2. Start the Apache service.
```
service httpd start
```
3. Test Apache.
>In this step, you should configure an inbound rule with the source being **all** and the port protocol being **TCP:80** in the security group of your CVM instance. For more information on how to configure the security group, please see [Security Groups](https://intl.cloud.tencent.com/document/product/213/12452).
>
Enter `http://xxx.xxx.xxx.xxx/` in your local browser (where `xxx.xxx.xxx.xxx` is the public IP of your CVM instance). If the following page appears, Apache has started successfully.
![](https://main.qcloudimg.com/raw/a8708d09de9280c730f47eb8289f7c47.png)

### Step 6. Install Apache's mod_wsgi extension as a Django application container
1. Install httpd-devel.
```
yum install -y httpd-devel
```
2. Install mod_wsgi.
```
yum install -y mod_wsgi
```

### Step 7. Create a project to test the Django environment
1. Create a test project under `/usr/local` by running `django-admin.py startproject projectname`, where projectname is the name of the project.
```
cd /usr/local
django-admin.py startproject projectname
```
2. Create a `django.wsgi` file in the **project's root directory** to support Apache.
```
cd /usr/local/projectname
vim django.wsgi
```
3. Enter the following in `django.wsgi`.
```
import os
import sys
from django.core.wsgi import get_wsgi_application
sys.path.insert(0, os.path.join(os.path.dirname(os.path.realpath(__file__)), '.'))
os.environ['DJANGO_SETTINGS_MODULE'] = 'projectname.settings'
application = get_wsgi_application()
```
4. Add Apache support by adding the following content to `httpd.conf` in `/etc/httpd/conf/httpd.conf`.
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
5. Create a view and a `view.py` file in the **project directory** `/usr/local/projectname/projectname` as the access entry with the following content:
```
from django.http import HttpResponse
def hello(request):
       return HttpResponse("Hello world ! ")
```
6. Configure the URL and the `urls.py` file in the **project directory** `/usr/local/projectname/projectname`. Delete the original content and add the following:
```
from django.conf.urls import *
from projectname.view import hello
urlpatterns = [
    url(r'^hello/$',hello),
]
```
7. Modify the `settings.py` file in the **project directory ** `/usr/local/projectname/projectname`.
```
ALLOWED_HOSTS = ['*']
```
8. Restart the Apache service.
```
service httpd restart
```
9. Enter `http://xxx.xxx.xxx.xxx/python/hello` in your local browser (where `xxx.xxx.xxx.xxx` is the public IP of your CVM instance). If "Hello world !" appears on the page, the project environment has been set up successfully.

### Step 8. Configure TencentDB in Django (optional)
1. Configure the `settings.py` file in the project directory.
```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'mysql',
        'USER': 'root', # TencentDB account name
        'PASSWORD': '123456', # TencentDB account password
        'HOST': '0.0.0.0', # TencentDB private network address
        'PORT': '3306', # TencentDB port
    }
}
```
2. Run the following command to test the database connection after configuration.
```
$python manage.py validate/check
```
3. Once the test is passed, database operations can be performed. For more information, please see [Models and Databases](https://docs.djangoproject.com/en/1.11/topics/db/).
