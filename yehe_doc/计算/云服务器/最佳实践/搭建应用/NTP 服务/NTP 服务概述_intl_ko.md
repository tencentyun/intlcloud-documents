네트워크 타임 프로토콜(Network Time Protocol, NTP)은 네트워크에서 각 컴퓨터의 시간을 동기화하는 데 사용되는 프로토콜입니다. 그 용도는 컴퓨터의 시계를 협정 세계시 UTC로 동기화하는 것입니다.

Tencent Cloud는 Tencent Cloud 내부 네트워크 디바이스용으로 내부 네트워크 NTP 서버를 제공하며 비 Tencent Cloud 디바이스일 경우, Tencent Cloud가 제공하는 공용 네트워크 NTP 서버를 사용할 수 있습니다.

### 내부 네트워크 NTP 서버

```ruby
time1.tencentyun.com
time2.tencentyun.com
time3.tencentyun.com
time4.tencentyun.com
time5.tencentyun.com
```

### 외부 네트워크 NTP 서버
```ruby
ntp.tencent.com
ntp1.tencent.com
ntp2.tencent.com
ntp3.tencent.com
ntp4.tencent.com
ntp5.tencent.com
```
다음은 이전 외부 네트워크 NTP 서버 주소이며 이전 주소를 계속 사용할 수 있지만 새 외부 네트워크 NTP 서버 주소를 설정하여 사용하는 것이 좋습니다.
```ruby
time.cloud.tencent.com
time1.cloud.tencent.com 
time2.cloud.tencent.com 
time3.cloud.tencent.com
time4.cloud.tencent.com
time5.cloud.tencent.com
```

Linux 시스템의 NTP 타임 원본 서버 설정 관련 자세한 내용은 [<Linux 인스턴스에서 NTP 서비스 설정>](https://intl.cloud.tencent.com/document/product/213/32381)을 참고하십시오.
Windows 시스템의 NTP 타임 원본 서버 설정 관련 자세한 내용은 [<Windows 인스턴스에서 NTP 서비스 설정>](https://intl.cloud.tencent.com/document/product/213/32380)을 참고하십시오.



