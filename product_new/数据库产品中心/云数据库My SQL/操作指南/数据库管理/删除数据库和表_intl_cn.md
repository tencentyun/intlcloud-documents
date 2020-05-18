## 通过 phpMyAdmin 控制台的图形界面
### 删除数据库
1. [登录 phpMyAdmin 控制台](https://intl.cloud.tencent.com/document/product/236/32341)，单击需要管理的数据库名称，进入数据库管理界面，单击【操作】。
![](https://main.qcloudimg.com/raw/dc2a0cec1568a8b98afa5ee745b130d0.png)
2. 在此页面可以对数据库进行【新建数据表】、【删除数据库】等一系列操作。单击【删除数据库（DROP）】即可完成数据库的删除操作。


### 删除数据表
选择需要删除表的数据库，在此页面可以对数据表进行【浏览】、【结构】、【搜索】、【删除】等一系列操作。单击【删除】。
![](https://main.qcloudimg.com/raw/d782e2f163851208d175b58e4d1383b6.png)

## 通过 phpMyAdmin 控制台的 SQL 命令
### 删除数据库
1. 登录 phpMyAdmin 控制台，通过 SQL 命令删除数据库，单击【SQL】。
![](https://main.qcloudimg.com/raw/d6ddac058780924dc717d54c61e92083.png)
2. 执行如下命令删除数据库。
```
drop database <database name>;
```

### 删除数据表
1. 通过 SQL 命令删除数据表，单击【SQL】。
![](https://main.qcloudimg.com/raw/b487a3625a974f45f9b5ebc6c58372f0.png)
2. 执行如下命令删除数据表。
```
drop table <table name>;
```
