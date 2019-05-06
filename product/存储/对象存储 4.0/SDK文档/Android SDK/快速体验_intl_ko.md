## 배경
&nbsp;&nbsp;&nbsp;&nbsp;모바일 인터넷 시대에 APP은 인터넷 서비스의 기초 인프라로서 다량의 데이터를 업로드 및 다운로드해야 하며, 데이터의 안전성과 신뢰성이 매우 중요합니다. 현재 개발자는 [Tencent Cloud COS 서비스](https://cloud.tencent.com/product/cos)를 사용하면 데이터 저장에 대한 더 이상 신경쓸 일이 없이 응용프로그램의 비즈니스 로직에만 집중하면 되어 작업량을 줄이고 개발 효율을 향상시킬 수 있습니다. 본문은 COS에 기반한 응용프로그램 전송 서비스 구축 방법을 소개합니다. 이를 통해 Tencent Cloud COS에서 응용프로그램 데이터의 업로드 및 다운로드를 구현하며 사용자의 서버에서 자신의 비즈니스 배포 및 임시 키 생성 및 관리만 하면 됩니다.

## 준비

- 임시 키 서비스 구축은 [임시 키 생성 및 사용 가이드](https://cloud.tencent.com/document/product/436/14048)를 참조하십시오.
- Android 4.0(api level 15) 이상 버전의 휴대폰.

>?임시 키 서비스를 통해 권한을 부여하시길 권장합니다. 일시 구축이 불가능한 경우, 영구 키를 통해 체험판 데모를 사용할 수 있습니다.


## App 다운로드 및 설치


Android 휴대폰 QR 코드를 사용하여 체험판 데모를 바로 다운로드할 수 있습니다.

![](https://main.qcloudimg.com/raw/2687b91ad1d02d335a9f264411275318.png)

완전한 코드는 [프로젝트 GitHub 주소 >>](https://github.com/tencentyun/qcloud-sdk-android-samples/tree/master/COSTransferPractice)를 참조하십시오.
