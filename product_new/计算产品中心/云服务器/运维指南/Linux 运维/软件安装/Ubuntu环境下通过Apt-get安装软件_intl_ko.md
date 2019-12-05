클라우드 서버 사용자의 소프트웨어 설치 효율성을 향상하고 소프트웨어 다운로드 및 설치 비용을 줄이기 위해 Tencent Cloud는 Apt-get 다운로드 소스를 제공합니다. 운영 체제는 Ubuntu 12.04 클라우드 서버이므로 사용자는 Apt-get을 통해 소프트웨어를 빠르게 설치할 수 있습니다.

apt-get 다운로드 소스의 경우 소프트웨어 소스를 추가할 필요가 없으며 패키지를 직접 설치할 수 있습니다. 소프트웨어 설치 속도를 높이기 위해 시스템은 인트라넷에서 Ubuntu의 mirror를 사전 구성하였으며, 이 mirror는 공식 x86_64의 전체 미러 이미지이며, 공식 웹 사이트 소스와 일치합니다. 

## 1. 설치 순서
1) Ubuntu 12.04 운영 체제의 클라우드 서버에 로그인합니다.

2) 다음 커맨드를 통하여 소프트웨어를 설치하십시오.

```
sudo apt-get install
```
다음 예시 참조

```
sudo apt-get install nginx php5-cli php5-cgi php5-fpm php5-mcrypt php5-mysql mysql-client-core-5.5 mysql-server-core-5.5
```

결과:

![](http://mccdn.qcloud.com/img56af4dfeb631a.png)

3) "Y" 입력 확인 후 소프트웨어 설치를 시작하고 설치가 완료될 때까지 기다리십시오.

## 2. 설치된 소프트웨어 정보 조회
소프트웨어 설치가 완료되면 다음 커맨드를 통하여 패키지가 있는 디렉터리와 패키지의 모든 파일을 조회할 수 있습니다.

```
sudo dpkg -L 
```

다음 커맨드를 통하여 패키지의 버전 정보를 조회할 수 있습니다.

```
sudo dpkg -l 
```

다음 예시 참조

```
sudo dpkg -L nginx 
sudo dpkg -l nginx
```

결과는 다음과 같습니다(실제 버전과 본 버전은 일치하지 않을 수 있으므로 실제로 쿼리한 버전을 기준으로 하십시오).
![](http://mccdn.qcloud.com/img56af4f1d9e433.png)
![](http://mccdn.qcloud.com/img56af4f7f57949.png)
