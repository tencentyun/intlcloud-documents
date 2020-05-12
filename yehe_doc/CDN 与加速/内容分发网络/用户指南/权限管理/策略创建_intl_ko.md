더 세분화된 도메인 조회, 권한 관리를 위해 CDN 권한 정책을 전면적으로 업그레이드하였기에, 사용자 정의 정책 명령을 통해 도메인별로 권한을 할당할 수 있습니다.

[액세스 관리 콘솔](https://console.cloud.tencent.com/cam/overview)에 로그인하고 [Policies]을 클릭하여 정책 관리 페이지에 접속한 후 [Create Custom Policy]을 클릭합니다.
![](https://main.qcloudimg.com/raw/6570c1642d59bf00b5dee346f48ddf0e.png)
2. [Create by policy generator]을 클릭합니다.
![](https://main.qcloudimg.com/raw/12a78b0a490d6cd95a4427b92710400f.png)
3. 제품 선택 창에서 [CDN]을 선택하고 권한을 설정할 기능 그룹을 선택합니다. 모든 읽기 쓰기 권한을 부여할 경우 [All]을 체크하여 모든 서비스를 선택할 수 있습니다. 기능과 콘솔의 매핑 관계는 [Action 매핑표](https://cloud.tencent.com/document/product/228/41867)를 참조 바랍니다.
![](https://main.qcloudimg.com/raw/16c968c01bb9811df5a6356f4a364928.png)
4. 리소스 부분에 권한을 부여할 도메인을 추가하고, `*`는 모든 도메인을 의미합니다. 설정 완료 후에 [Add Statement] 및 [Next]를 클릭하면 생성한 정책이 기존 사용자 / 사용자 그룹에 연결되어 권한을 부여할 수 있습니다.
![](https://main.qcloudimg.com/raw/0497f341d3ad51b56e07682aadc23ba8.png)

