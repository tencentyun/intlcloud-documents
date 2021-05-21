These examples provide code snippets based on Python 3.6 for your reference.

You can click [scf-python-code-snippet](https://github.com/awesome-scf/scf-python-code-snippet) to obtain the relevant code snippets and directly use them for deployment.

## Obtaining Environment Variables

This example shows you how to obtain all or a single environment variable.

```
# -*- coding: utf8 -*-
import os
		
def main_handler(event, context):
      print(os.environ)
      print(os.environ.get("SCF_RUNTIME"))
      return("Hello World")
```

## Formatting Local Time

This example shows you how to output date and time in the specified format.

The SCF environment uses the UTC format by default. To output in Beijing time, you can add the `TZ=Asia/Shanghai` environment variable to the function.

```
# -*- coding: utf8 -*-
import time
		
def main_handler(event, context):
      print(time.strftime('%Y-%m-%d %H:%M:%S',time.localtime(time.time())))   
      return("Hello World")
```

## Accessing TencentDB for MySQL Instance

This example shows you how to use the PyMySQL library for the database connection. You need to run the `pip3 install PyMySQL -t .` command under the project directory to install this dependent library.

Please note the following:

* Configure the function in the same VPC where the TencentDB for MySQL instance is located to ensure the network accessibility.
* Replace the database’s IP, username, password, name and other information shown in the codes with your actual values.


```
# -*- coding: utf8 -*-
import pymysql

def main_handler(event, context):
        
       # Start connecting to the database
       db = pymysql.connect(host="host ip",port=3306,user="user",password="password",database="db name")
    
       # Use the cursor() method to create a cursor object
       cursor = db.cursor()
    
       # Use the execute() method to execute the SQL query statement 
       cursor.execute("SELECT VERSION()")
    
       # Use the fetchone() method to obtain a single data entry.
       data = cursor.fetchone()
    
       print ("Database version : %s " % data)
    
       # Stop connecting to database
       db.close()
    
```

## Initiating Network Connections in a Function

This example shows you how to use the requests library to initiate network connections in a function and obtain page information. You can run the `pip3 install requests -t .` command under the project directory to install this dependent library.

```
# -*- coding: utf8 -*-
import requests
	

def main_handler(event, context):
      addr = "https://cloud.tencent.com"    
      resp = requests.get(addr)
      print(resp)
      print(resp.text)
      return resp.status_code

```


## Obtaining Webpages Using SCF and API Gateway

This example shows you how to access the URL through API Gateway while obtaining the HTML page by configuring API Gateway trigger and enabling integration response.

```
# -*- coding: utf8 -*-
import time

def main_handler(event, context):
      resp = {
          "isBase64Encoded": False,
          "statusCode": 200,
          "headers": {"Content-Type":"text/html"},
          "body": "<html><body><h1>Hello</h1><p>Hello World.</p></body></html>"
      }  
      return resp
```

## Obtaining Images Using SCF and API Gateway

This example shows you how to access the URL through API Gateway while obtaining the binary image file by configuring API Gateway trigger and enabling integration response.


```
# -*- coding: utf8 -*-
import base64

def main_handler(event, context):
       with open("tencent_cloud_logo.png","rb") as f:
           data = f.read()
       base64_data = base64.b64encode(data)    
       base64_str = base64_data.decode('utf-8')
       resp = {
           "isBase64Encoded": True,
           "statusCode": 200,
           "headers": {"Content-Type":"image/png"},
           "body": base64_str
       }
       return resp
```

