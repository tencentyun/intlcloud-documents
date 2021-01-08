
4. 修改`sites`目录属主属组。
```
chown -R apache:apache /var/www/html/sites
```
5. 重启 Apache 服务。
```
service httpd restart
```
6. 在您本地的浏览器中输入`http://115.xxx.xxx.xxx/`（其中 `115.xxx.xxx.xxx`为您的云服务器公网 IP 地址），进入 Drupal 安装界面。选择安装版本，单击【Save and continue】。
![](https://main.qcloudimg.com/raw/f52af1bb9822ddefc1989df9a0a95e8c.png)
7. 选择安装语言，单击【Save and continue】。
![](https://main.qcloudimg.com/raw/11a8f788ebd0595e6afdff936656c2cc.png)
8. 设置数据库，输入您在**安装 mariadb 服务**中配置的数据库信息。

9. 输入站点信息。
 
10. 完成 Drupal 的安装。

11. 后续可以访问 `http://115.xxx.xxx.xxx/`（其中 `115.xxx.xxx.xxx`为您的云服务器公网 IP 地址）对网站进行个性化设置。
