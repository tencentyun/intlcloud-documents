## 소개

Tencent Cloud COS(Cloud Object Storage)는 객체 잠금 기능을 제공하며, 이 기능은 설정한 기간 내에 객체를 수정하거나 삭제할 수 없으며 즉시 액세스할 수 있습니다. 본 문서는 콘솔에서 객체 잠금 기능을 활성화하는 방법에 대해 소개합니다.

## 작업 단계

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인합니다.
2. 왼쪽 사이드바에서 **버킷 리스트**를 클릭하여 버킷 리스트 페이지로 이동합니다.
3. 객체 잠금을 설정할 버킷을 클릭하여 버킷 리스트로 이동합니다.
4. **보안 관리 > 객체 잠금**을 클릭하고 **객체 잠금** 구성 항목을 찾은 다음 **편집**을 클릭하여 ‘활성화’합니다.
5. 보관 기간을 설정하고 **저장**을 클릭합니다.
![](https://main.qcloudimg.com/raw/f932220976adfe110e352bbd04079438.png)
	보관 기간: 자연수를 입력합니다. 보관 주기는 연장만 가능하고 단축할 수 없으니 합리적으로 설정하시기 바랍니다.
6. 팝업 창에서 **확인**을 클릭합니다.
설정 후 **파일 목록**을 클릭해 확인할 파일을 선택하고 파일 오른쪽의 **세부 정보**를 클릭하여 객체 잠금 규칙이 만료되는 날짜(현지 시간)를 볼 수 있습니다.
>?이제 객체 잠금은 얼로우리스트에 있는 고객만 사용할 수 있습니다. 이 기능을 활성화하려면 당사에 [문의하기](https://intl.cloud.tencent.com/contact-sales)로 문의하십시오.
