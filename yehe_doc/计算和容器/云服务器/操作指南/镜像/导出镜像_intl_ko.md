## 작업 시나리오
Tencent Cloud는 생성된 사용자 정의 이미지를 [Cloud Object Storage](https://intl.cloud.tencent.com/document/product/436/6222) 버킷으로 내보내기를 지원하며, 이 기능을 통해 원하는 이미지를 내보낼 수 있습니다.

## 전제 조건
- 현재 이 기능을 사용하려면 신청해야 합니다. [티켓 제출](https://console.intl.cloud.tencent.com/workorder/category)을 통해 신청하십시오.
- [COS 콘솔](https://console.cloud.tencent.com/cos)로 이동하여 COS 서비스를 활성화해야 합니다.
- 사용자 정의 이미지가 위치한 리전에 버킷이 생성되어야 합니다. 자세한 내용은 [버킷 생성](https://intl.cloud.tencent.com/document/product/436/13309)을 참고하십시오.


## 주의 사항
- Windows 사용자 정의 이미지 내보내기는 현재 지원되지 않습니다.
- 사용자 정의 이미지의 시스템 디스크 및 데이터 디스크의 단일 블록 용량은 500GB를 초과할 수 없습니다.
- 전체 이미지를 내보낼 때 데이터 디스크의 수는 5보다 클 수 없습니다.


## 작업 단계
1. CVM 콘솔에 로그인한 뒤, 왼쪽 사이드바의 **[이미지](https://console.cloud.tencent.com/cvm/image)**를 선택합니다.
2. ‘이미지’ 페이지 상단에서 내보낼 사용자 정의 이미지가 있는 리전을 선택하고 **사용자 정의 이미지** 탭을 클릭합니다.
3. 이미지가 있는 행의 오른쪽에 있는 **더 보기** > **이미지 내보내기**를 아래 이미지와 같이 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/67a493d7ae96d92b514f5c124619821c.png)
4. ‘이미지 내보내기’ 팝업 창에서 아래 이미지와 같이 설정합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/4cf1d41610772605ac5867be12353b5a.png)
 - **COS Bucket**: 이미지를 내보내기 할 버킷을 선택합니다. 버킷은 이미지와 동일한 리전에 있어야 합니다.
 - **내보내기할 파일의 접두사명**: 내보내기 파일 접두사 이름을 사용자 정의합니다.
 ‘CVM에 COS Bucket 액세스 권한을 부여하는데 동의합니다’를 선택합니다.
5. **확인**을 클릭하여 이미지 내보내기 작업을 시작합니다.
6. 팝업 창에서 **확인**을 클릭합니다.
내보내기 시간은 이미지의 크기와 작업 큐의 사용량에 따라 다르므로 잠시만 기다려 주십시오. 내보내기 작업이 완료되면 이미지 파일이 타깃 버킷에 저장됩니다. [버킷 리스트](https://console.cloud.tencent.com/cos/bucket) 페이지로 이동하여 버킷 ID를 클릭하여 세부 정보 페이지로 이동할 수 있으며, ‘사용자 정의 접두사명_xvda.raw’라는 파일이 내보낸 이미지 파일입니다.
