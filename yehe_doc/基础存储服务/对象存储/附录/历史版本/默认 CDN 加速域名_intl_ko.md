>!2022년 5월 9일 부터 Cloud Object Storage(COS)는 사용 이력이 없는 버킷에 대한 기본 CDN 가속 도메인 지원을 중단합니다. 이 변경 사항은 기본 CDN 가속 도메인을 사용 중이거나 사용 이력이 있는 버킷에는 영향을 미치지 않으나, 사용자 정의 CDN 가속 도메인으로 전환하는 것이 좋습니다. 사용자 정의 CDN 가속 도메인 작업 가이드는 [사용자 정의 CDN 가속 도메인 이름 활성화하기](https://intl.cloud.tencent.com/document/product/436/31506) 문서를 참고하십시오.

### 설정 설명

기본 CDN 가속 도메인은 COS가 메모리 버킷에 자동으로 할당하는 CDN 가속 도메인입니다.` BucketName-APPID.file.myqcloud.com`과 같은 형식으로, 기본 CDN 가속이 활성화되면 이 도메인을 통해 액세스 가속 경험을 얻을 수 있습니다.

#### 작업 순서

#### 1. 버킷 선택
[COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인한 뒤 왼쪽 사이드바에서 **버킷 리스트**를 클릭하고, 다시 가속할 버킷을 클릭하여 버킷 관리 페이지로 이동합니다.

#### 2. 설정 페이지로 이동
>!Tencent Cloud CDN 서비스를 이용하지 않는 사용자는 **도메인 관리** 페이지에 들어갈 수 없습니다. 먼저 [CDN 콘솔](https://console.cloud.tencent.com/cdn)로 이동한 뒤 CDN 서비스를 활성화하십시오.

왼쪽의 **도메인 및 전송 관리 > 기본 CDN 가속 도메인**을 클릭한 뒤 **기본 CDN 가속 도메인** 설정 항목을 찾습니다. 기본 CDN 가속 도메인의 기본값은 **비활성화**로 설정되어 있습니다. **편집**을 클릭하여 현재 상태를 **활성화**로 변경하고, 다음 아래의 설정 항목 지침에 따라 구성합니다.

 - **가속 도메인 이름**: 기본 CDN 가속 도메인 이름은 'BucketName-APPID.file.myqcloud.com' 형식으로 COS에서 버킷에 자동으로 할당한 CDN 가속 도메인 이름입니다. 이 도메인 이름을 사용하여 액세스 가속화 경험을 얻을 수 있습니다.
 - **가속 리전**: 중국 내외 및 글로벌 가속을 지원하며, 글로벌 가속의 경우 모든 리전 간 버킷의 가속을 지원합니다.
 - **원본 서버 유형**: 기본값은 **기본 원본 서버**입니다. 원본 서버인 버킷으로 정적 웹 사이트를 활성화한 뒤 가속하려면 원본 서버 유형을 **정적 웹 사이트 원본 서버**로 설정하십시오. 자세한 내용은 [CDN 가속 개요](https://intl.cloud.tencent.com/document/product/436/18669)를 참고하십시오.
 - **원본 서버 도메인**: COS 원본 서버 도메인입니다. 버킷 생성 시 버킷 이름 및 리전에 따라 시스템에서 자동으로 생성됩니다. 기본 CDN 가속 도메인과 구분됩니다.

#### 3. Origin-pull 인증 활성화(옵션)

>!개인 읽기 버킷의 경우, Origin-pull 인증과 CDN 서비스 라이선스를 활성화하면 서명 없이도 CDN 엣지 노드에서 원본 서버로 액세스할 수 있습니다. CDN 캐시 리소스가 공용 네트워크로 전송되어 데이터 보안이 취약할 수 있으니 CDN 인증을 활성화하시길 권장합니다.

Origin-pull 인증은 불법 액세스를 차단하기 위해 CDN 엣지 노드의 서비스 자격을 인증하는 용도입니다. 자세한 내용은 다음과 같습니다.
- 공개 읽기 버킷: 라이선스가 없어도 CDN 엣지 노드에서 버킷에 바로 액세스할 수 있으므로 Origin-pull 인증을 실행하지 않아도 됩니다.
- 개인 읽기 버킷: CDN 엣지 노드는 Origin-pull 인증을 통해 서비스 자격을 인증해야 하며, 인증을 통과해야 버킷에 저장된 객체에 액세스할 수 있습니다.


(1) CDN 서비스 인증 완료

>?Origin-pull 인증을 활성화하기 전에 CDN 서비스 라이선스를 추가해야 합니다.

작업 순서는 다음과 같습니다.
CDN 서비스 라이선스를 추가하면 CDN 엣지 노드에서 버킷에 작업할 수 있는 자격이 부여됩니다. 자세한 내용은 다음과 같습니다.
- 공개 읽기 버킷: 라이선스가 없어도 CDN 엣지 노드에서 버킷에 바로 액세스할 수 있으므로 CDN 서비스 라이선스를 추가하지 않아도 됩니다.
- 개인 읽기 버킷: 특정한 서비스 자격이 있어야 CDN 엣지 노드에서 버킷에 액세스할 수 있습니다. **CDN 서비스 라이선스 추가**를 클릭하여 CDN 엣지 노드 서비스 자격을 부여받은 뒤 **위의 권한 부여에 동의합니다**를 선택하고 **확인**을 클릭합니다.

CDN 서비스 인증을 완료한 후 CDN 엣지 노드는 버킷에서 Get Object, Head Object 및 Options Object의 세 가지 작업을 수행할 수 있습니다. 시스템이 버킷 액세스 정책을 자동으로 작성하며 다음과 같은 정책 예시가 제공됩니다. 그 후 CDN 노드는 Origin-pull 시 다른 작업을 수행할 필요가 없습니다.

```xml
  {
    "Statement":[
      {
        "Action":[
          "name/cos:GetObject",
          "name/cos:HeadObject",
          "name/cos:OptionsObject"
        ],
        "Effect": "allow",
        "Principal":{
          "qcs":[
            "qcs::cam::uin/100000000001:service/cdn"
          ]
        },
        "Resource":[
          "qcs::cos:ap-chengdu:uid/1250000000:examplebucket-1250000000/*"
        ]
      }
    ],
    "version": "2.0"
  }
```

(2) 인증이 완료된 것으로 점검되면 클릭하여 **Origin-pull 인증**을 활성화할 수 있습니다.




#### 4. CDN 가속 활성화
**저장**을 클릭하면 기본 CDN 가속 도메인의 배포를 시작합니다(약 5분 소요).

#### 5. CDN 인증 설정

>!기본 CDN 가속이 활성화된 후, 누구나 해당 도메인으로 원본 서버에 바로 액세스할 수 있습니다. 보안이 필요한 데이터의 경우, **인증 설정 활성화**를 통해 원본 서버의 데이터를 보호하십시오.

 - 기본 CDN 가속 도메인과 Origin-pull 인증을 활성화하면 기본 CDN 가속 도메인 관리 인터페이스에 CDN 인증 상태 알림바가 나타납니다. 알림바의 **인증 설정** 메뉴를 통해 설정할 도메인의 **액세스 제어** 페이지로 이동할 수 있습니다.

 - 또는 [CDN 콘솔](https://console.cloud.tencent.com/cdn)로 이동하여 **도메인 관리**를 클릭한 다음 기본 CDN 가속 도메인을 선택하고 마지막으로 **액세스 제어**>**인증 설정**을 클릭합니다. 자세한 설정 단계는 [인증 설정](https://intl.cloud.tencent.com/document/product/228/35237)을 참고하십시오.

#### 6. 기능 비활성화

위의 단계를 완료하면 기본 CDN 가속이 활성화됩니다. 기본 CDN 가속을 비활성화하려면 다음과 같은 방법으로 비활성화할 수 있습니다.

- 기본 CDN 가속 도메인 관리 인터페이스에서 **편집**을 클릭하여 상태를 **활성화**에서 **비활성화**로 변경한 뒤 **저장**을 클릭합니다. 배포 완료까지 5분 정도 소요됩니다. 배포를 마치면 CDN 콘솔의 해당 도메인 상태가 **활성화됨**에서 **비활성화됨**으로 변경됩니다.
- [CDN 콘솔](https://console.cloud.tencent.com/cdn)에서 도메인의 비활성화/삭제 작업을 실행할 수 있으며, 자세한 내용은 [도메인 작업](https://intl.cloud.tencent.com/document/product/228/5736)을 참고하십시오.



>!CDN 콘솔에서 삭제되는 것은 기본 CDN 가속 도메인의 CDN 가속 모드에서의 기록일 뿐이며 실제로 기본 CDN 가속 도메인을 지우지는 않습니다. CDN 가속을 다시 활성화해야 하는 경우 COS 콘솔에서 기본 CDN 가속 도메인을 다시 활성화하십시오.
>


