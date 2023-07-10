## 키 문제

### APPID, SecretId, SecretKey 등 키 정보는 어떻게 확인합니까?

버킷 이름의 뒷부분이 APPID 정보로, [COS 콘솔](https://console.cloud.tencent.com/cos5/bucket)에 로그인하여 확인할 수 있습니다. SecretId, SecretKey 등의 정보는 CAM 콘솔에 로그인하여 [API 키 관리](https://console.cloud.tencent.com/cam/capi)에서 확인할 수 있습니다.

### 임시 키의 유효시간은 얼마나 됩니까?

임시 키는 현재 루트 계정의 경우 최장 2시간(즉, 7200초)이고 서브 계정의 경우 최장 36시간(즉, 129600초)이며, 기본값은 30분(즉, 1800초)로 설정되어 있습니다. 임시 키 만료 후, 만료된 임시 키를 가진 요청은 거절됩니다. 임시 키 관련 자세한 소개는 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048)를 참조하십시오.

### APPID, SecretId 등과 같은 키 관련 정보가 노출되었습니다. 어떻게 해야 합니까?

노출된 키를 삭제하고 새로운 키를 생성할 수 있습니다. 자세한 내용은 [액세스 키](https://intl.cloud.tencent.com/document/product/598/34227)를 참조하십시오.

### 개인 읽기/쓰기 파일에 유효기간이 있는 액세스 링크는 어떻게 생성합니까?

자세한 방법은 [임시 키 생성 및 사용 가이드](https://intl.cloud.tencent.com/document/product/436/14048) 문서를 참조하여 키 유효기간을 설정하십시오.

## ACL+ Policy 등의 권한 문제

### 업로드 및 다운로드 시 “403 Forbidden” 및 권한 거절 등 오류가 발생합니다. 어떻게 처리해야 합니까?

다음 순서에 따라 문제를 진단하십시오.

1. 다음 정보가 정확하게 설정되어 있는지 확인합니다.
   BucketName, APPID, Region, SecretId, SecretKey 등
2. 상기 정보가 정확하게 설정되어 있다는 전제 하에 서브 계정을 사용하여 작업했는지 확인하고, 서브 계정을 사용한 경우 루트 계정에서 서브 계정에 권한을 부여했는지 확인합니다. 권한을 부여하지 않은 경우 먼저 루트 계정으로 로그인하여 서브 계정에 권한을 부여합니다.
   권한 부여 방법은 [액세스 권한 관리 설정 관련 사례](https://intl.cloud.tencent.com/document/product/436/12514)를 참조하십시오.
3. 임시 키를 사용한 경우 현재 작업이 임시 키를 획득할 때 설정한 Policy에 부합하는지 확인하고, 부합하지 않는다면 관련 Policy 설정을 수정합니다.
4. 상기 순서에 따라 진행해도 문제를 해결할 수 없는 경우 [티켓 제출](https://console.cloud.tencent.com/workorder/category?level1_id=83&level2_id=84&source=0&data_title=%E5%AF%B9%E8%B1%A1%E5%AD%98%E5%82%A8%20COS&step=1)을 통해 문의하십시오.

### 기본 도메인 액세스 공개 읽기 버킷 사용 시 파일 리스트가 리턴됩니다. 파일 리스트를 숨기려면 어떻게 해야 합니까?

상응하는 버킷에 deny anyone의 Get Bucket 권한을 설정하면 되며, 작업 방법은 다음과 같습니다.

[COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하여 버킷 리스트를 선택해 상응하는 버킷의 **권한 관리** 페이지로 이동합니다.

#### 방법 1:

1. **정책 권한 설정 페이지**를 찾아 [그래픽 설정]에서 [정책 추가]를 클릭합니다.
2. 다음 이미지와 같이 상응하는 권한 설정을 추가하고 [확인]을 클릭해 저장합니다.
   ![정책 그래픽 설정](https://main.qcloudimg.com/raw/6c9262116cb78654ea5c25d9ba483595.png)

#### 방법 2:

**정책 권한 설정 페이지**를 찾아 [정책 구문]>[편집]을 클릭하여 다음 표현식을 입력합니다.
```
{
  "Statement": [
    {
      "Action": [
        "name/cos:GetBucket",
        "name/cos:GetBucketObjectVersions"
      ],
      "Effect": "Deny",
      "Principal": {
        "qcs": [
          "qcs::cam::anyone:anyone"
        ]
      },
      "Resource": [
        "qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"
      ]
    }
  ],
  "version": "2.0"
}
```

>“qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*”의 관련 정보를 다음과 같이 변경합니다.
> - “ap-beijing”을 사용자의 버킷 리전으로 변경합니다.
> - “1250000000”을 사용자의 APPID 정보로 변경합니다.
> - “examplebucket-1250000000”을 사용자의 버킷 이름으로 변경합니다.
>
> 이 중, 버킷 이름의 뒷부분이 APPID이며, [COS 콘솔](https://console.cloud.tencent.com/cos5/bucket)에서 버킷 이름을 확인할 수 있습니다.

### COS의 ACL 제한 타깃은 버킷입니까, 계정입니까? 파일 업로드 시 권한을 지정할 수 있습니까?

ACL 제한 타깃은 계정입니다. ACL 규칙 수가 1000개를 초과할 경우 오류가 발생하여 파일 업로드 시 권한 지정을 권장하지 않습니다.

### 협업 파트너에게 지정된 버킷의 액세스 권한을 어떻게 부여합니까?

협업 파트너 계정은 일종의 특수 서브 계정으로, 자세한 내용은 [액세스 정책 언어 개요](https://intl.cloud.tencent.com/document/product/436/18023)를 참조하십시오.

### 여러 비즈니스에서 버킷 작업이 필요한 경우, 버킷 또는 다른 차원으로 권한을 격리할 수 있습니까?

[CAM 콘솔](https://console.cloud.tencent.com/cam/overview)에 로그인하여 사용자 관리 페이지로 이동해 비즈니스별로 서브 계정을 활성화하고 각각의 권한을 부여할 수 있습니다.


### 자회사 또는 직원에게 서브 계정을 생성하여 특정 버킷의 액세스 권한을 어떻게 부여합니까?

자세한 내용은 [서브 계정에 COS 액세스 권한 부여](https://intl.cloud.tencent.com/document/product/436/11714)를 참조하여 서브 계정을 생성하고 권한을 부여하십시오.

### 특정 서브 계정에 특정 버킷에 대해서만 작업 권한을 부여하고 싶은 경우 어떻게 해야 합니까?

서브 계정에 특정 버킷에 대해서만 작업 권한을 부여하고 싶은 경우 서브 계정에 경로 추가를 이용할 수 있습니다. 자세한 내용은 [서브 계정의 액세스 버킷 리스트](https://intl.cloud.tencent.com/document/product/436/17061)를 참조하십시오.

### A 계정을 사용하여 B 계정에 A 계정의 버킷에 대한 쓰기 권한을 어떻게 부여합니까?

자세한 내용은 [ACL 액세스 제어 사례](https://intl.cloud.tencent.com/document/product/436/12470) 및 [CAM 액세스 관리 사례](https://intl.cloud.tencent.com/document/product/436/12469)를 참조하여 권한을 부여하십시오.

## 링크 도용 방지 문제

### CDN 가속을 활성화하고 CDN 도메인으로 리소스를 액세스하는 경우, 링크 도용 방지 설정은 어떻게 적용합니까?

CDN 가속 도메인으로 리소스에 액세스하는 경우 CDN 캐시 등의 요소로 인해 COS 링크 도용 방지의 안정성에 영향을 줄 수 있습니다. [CDN 콘솔](https://console.cloud.tencent.com/cdn)을 통한 링크 도용 방지 설정을 권장하며, 자세한 내용은 [CDN 링크 도용 방지 설정](https://intl.cloud.tencent.com/document/product/228/6292)을 참조하십시오.

### 화이트리스트를 설정하여 액세스를 허용해 브라우저에서 단독으로 링크를 열어 액세스하는 것을 허용할 수 있습니까?

링크 도용 방지 설정 시 공백 referer 허용을 선택하면 화이트리스트를 설정하여 브라우저에서 단독으로 링크를 열어 액세스할 수 있습니다.

### 버킷 test의 링크 도용 방지 화이트리스트를 설정하고 `a.com`의 액세스를 허용하였으나 `a.com` 웹페이지 재생기에서 버킷 test의 비디오 파일이 재생되지 않습니다.

웹 페이지에서 Windows Media Player, Flash Player 등의 재생기를 사용하여 비디오 링크 재생 시 요청의 referer가 공백인 경우 화이트리스트 히트 미스가 발생하므로 화이트리스트 설정 시 공백 referer 허용을 권장합니다.

## 암호화 및 백업 등 기타 문제

### COS에서 파일 암호화를 지원합니까?

서버에서의 파일 암호화를 지원하며, 자세한 내용은 [서버에서의 암호화](https://intl.cloud.tencent.com/document/product/436/18145)를 참조하십시오.

### COS의 표준 스토리지, 표준IA 스토리지, CAS 데이터에 백업이 존재합니까?

COS의 데이터는 멀티 사본 또는 이레이저 코딩 방식으로 하위 레이어에 저장되며, 분산형 엔진이 한 리전의 여러 가용존에 분포하고 있어 99.999999999%의 신뢰성을 자랑합니다. 멀티 사본과 이레이저 코딩 저장은 하위 레이어 로직으로, 사용자는 확인할 수 없습니다.

### 동일한 계정의 버킷 요청량이 너무 큰 경우 다른 버킷 액세스에 영향을 줍니까?

요청량이 커도 영향을 주지 않습니다. 그러나 빈도가 너무 빠르면 영향을 주며, 자세한 내용은 [요청 속도 및 성능 최적화](https://intl.cloud.tencent.com/document/product/436/13653)를 참조하십시오.
