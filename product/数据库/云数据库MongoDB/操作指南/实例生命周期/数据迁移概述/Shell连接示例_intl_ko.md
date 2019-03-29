
CVM에서 MongoDB가 제공하는 Shell 클라이언트([설치 문서 보기](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-linux/))를 이용하여 TencentDB for MongoDB를 연결한 후, 데이터를 관리합니다. 최신 버전의 MongoDB 클라이언트 슈트를 사용해야 합니다.

### 빠른 시작
전형적인 연결 명령은 다음과 같습니다.
```
mongo 10.66.187.127:27017/admin -u mongouser -p thepasswordA1
```
다음 그림과 같습니다.
![전형적인 연결 명령 스크린샷 예제](https://mc.qcloudimg.com/static/img/ce6b26f8cd6b1cc2981bc0cd44f9d09d/shell_default.png)

### 여러 인증 방식의 연결 설명
[연결 예제](https://cloud.tencent.com/doc/product/240/3563) 문서에 설명되어 있습니다. TecentDB for MongoDB는 기본적으로 "rwuser"와 "mongouser" 두 개 사용자 이름을 제공하며 각각 "MONGODB-CR"과 "SCRAM-SHA-1" 인증 방식을 지원합니다.
두 가지 인증 방식의 경우 Shell 명령 매개변수가 다릅니다. 자세한 내용은 다음을 참조하십시오.

### SCRAM-SHA-1 인증(Mongouser)
**기본 사용자 "Mongouser" 및 콘솔에서 생성한 모든 새 사용자는 SCRAM-SHA-1 인증 방식을 사용합니다. ** 해당 Shell의 연결 매개변수는 [빠른 시작](#.E5.BF.AB.E9.80.9F.E5.BC.80.E5.A7.8B) 부분과 똑같고 별도의 매개변수를 추가할 필요가 없습니다. 예제는 다음과 같습니다.
```
mongo 10.66.187.127:27017/admin -u mongouser -p thepasswordA1
```
특별한 상황에서 MongoDB를 연결한 후 직접적으로 "Singer"와 같은 어느 데이터베이스에 들어가고 싶은 경우, 예제에 따라 작업하십시오.
```
mongo 10.66.187.127:27017/singer -u mongouser -p thepasswordA1 --authenticationDatabase admin
```
다음 그림과 같습니다.
![DB로의 연결 명령 스크린샷 예제](https://mc.qcloudimg.com/static/img/c30cc3e6e2db6c8bd3cce2e327ce63db/sha1_sonedb.png)

### MONGODB-CR 인증(rwuser)
**주의: 기본 사용자 "rwuser"만 MONGODB-CR 방식으로 인증합니다. ** 해당 Shell의 연결 매개변수는 MONGODB-CR 인증 방식을 명확히 지정해야 합니다. 다음 예제를 참조하십시오.
```
mongo 10.66.187.127:27017/admin -u rwuser -p thepasswordA1 --authenticationMechanism=MONGODB-CR
```
다음 그림과 같습니다.
![MONGODB-CR 인증 스크린샷 예제](https://mc.qcloudimg.com/static/img/ff200b49c3fa5c70812027dd89e3ebc3/cr_default.png)
특별한 상황에서 MongoDB를 연결한 후 직접적으로 "singer"와 같은 어느 데이터베이스에 들어가고 싶은 경우, 예제에 따라 작업하십시오.
```
mongo 10.66.187.127:27017/singer -u rwuser -p thepasswordA1 --authenticationMechanism=MONGODB-CR --authenticationDatabase admin
```
다음 그림과 같습니다.
![DB로의 연결 명령 스크린샷 예제](https://mc.qcloudimg.com/static/img/d31bfa612a295fd070ea5dd09c7ce6a3/cr_somedb.png)

### Shell로 데이터 가져오기/내보내기
상기 두 가지 인증 방식은 모두 Shell에서 데이터를 가져오기와 내보내기 작업을 진행할 수 있습니다. [여기를 참고하십시오.](https://cloud.tencent.com/doc/product/240/5321)
