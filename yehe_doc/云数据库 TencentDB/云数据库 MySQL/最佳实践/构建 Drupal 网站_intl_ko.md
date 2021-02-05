
4. `sites` 디렉터리의 소속 마스터 그룹을 수정합니다.
```
chown -R apache:apache /var/www/html/sites
```
5. Apache 서비스를 재시작합니다.
```
service httpd restart
```
6. 사용자의 로컬 브라우저에 `http://115.xxx.xxx.xxx/`를 입력합니다(`115.xxx.xxx.xxx`는 사용자의 CVM 공인 IP 주소입니다). Drupal 설치 인터페이스에서 설치 버전을 선택하고, [Save and continue]를 클릭합니다.
![](https://main.qcloudimg.com/raw/f52af1bb9822ddefc1989df9a0a95e8c.png)
7. 설치 언어를 선택하고, [Save and continue]를 클릭합니다.
![](https://main.qcloudimg.com/raw/11a8f788ebd0595e6afdff936656c2cc.png)
8. 데이터베이스를 설정하고, **설치 mariadb 서비스**에 설정된 데이터베이스 정보를 입력합니다.

9. 사이트 정보를 입력합니다.
 
10. Drupal 설치를 완료합니다.

11. 추후 웹사이트 `http://115.xxx.xxx.xxx/`(`115.xxx.xxx.xxx`는 사용자의 CVM 공인 IP 주소입니다)에 액세스해 개성화할 수 있습니다.
