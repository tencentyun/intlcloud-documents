네트워크 타임 프로토콜(Network Time Protocol, NTP)은 네트워크에서 각 컴퓨터의 시간을 동기화하는 데 사용되는 프로토콜입니다. 그 용도는 컴퓨터의 시계를 협정 세계시 UTC로 동기화하는 것입니다.

Tencent Cloud는 Tencent Cloud 내부 네트워크 디바이스용으로 내부 네트워크 NTP 서버를 제공하며 비 Tencent Cloud 디바이스일 경우, Tencent Cloud가 제공하는 공용 네트워크 NTP 서버를 사용할 수 있습니다.

### 내부 네트워크 NTP 서버

```
ntpupdate.tencentyun.com
```

### 외부 네트워크 NTP 서버

```
time1.cloud.tencent.com 
time2.cloud.tencent.com 
time3.cloud.tencent.com
time4.cloud.tencent.com
time5.cloud.tencent.com
```

Linux 시스템의 NTP 시계 원본 서버 설정의 자세한 내용은 [<Linux 인스턴스 NTP 서비스 설정>](https://cloud.tencent.com/document/product/213/30393)을 참조하십시오.
Windows 시스템의 NTP 시계 원본 서버 설정의 자세한 내용은 [<Windows 인스턴스 NTP 서비스 설정>](https://cloud.tencent.com/document/product/213/30394)을 참조하십시오.

