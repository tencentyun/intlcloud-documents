## 소개

COS 콘솔을 통해 버킷에 업로드한 단일 혹은 여러 객체를 복사할 수 있으며 객체를 소스 경로에서 타깃 경로로 붙여넣기 할 수 있습니다.

>- CAS 유형 객체의 복사 붙여넣기를 지원하지 않습니다.
>- 서브 계정이 객체를 복사하려면 PutObject, GetObject, GetObjectACL 3개 권한이 필요합니다.

## 작업 순서

1. [COS 콘솔](https://console.cloud.tencent.com/cos5)에 로그인하고 왼쪽 메뉴에서 [버킷 리스트]를 클릭하여 버킷 리스트 페이지로 이동합니다.
2. 해당 버킷에서 버킷 이름을 클릭하여 버킷의 파일 리스트 페이지로 이동합니다.
3. 복사할 객체 혹은 폴더를 선택합니다. 다중 선택도 가능합니다. [더 많은 조작]에서 [복사]를 클릭하십시오.
![](https://main.qcloudimg.com/raw/dffbfdbb92b1ca08f0bbc3685d1788c9.png)
4. 복사 완료 팝업 문구가 나타나면 타깃 경로를 선택해 붙여넣습니다. 예를 들어, 버킷 examplebucket1-1250000000에 있는 target 폴더에 붙여넣습니다.
![](https://main.qcloudimg.com/raw/c5ced94c2d09085efb55bf39a87a258b.png)
>타깃 경로는 소스 경로와 같을 수 없습니다. 동일한 경우 붙여넣기에 실패합니다.
5. 붙여넣기를 완료하면 객체와 폴더가 모두 target 폴더에 복사된 것을 볼 수 있습니다.
![](https://main.qcloudimg.com/raw/fc32963a0ad9e2db5ad5a9ef7488b79a.png)
