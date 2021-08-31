## 작업 시나리오
본 문서에서는 CVM 콘솔과 클라우드 API를 통해 셧다운 상태의 인스턴스를 스타트업 하는 방법에 대해 설명합니다.




- 작업 순서
### 콘솔을 통해 인스턴스 스타트업 하기
1. [CVM 콘솔](https://console.cloud.tencent.com/cvm/)에 로그인합니다.
2. 실제 필요에 따라 부동한 작업 방식을 선택하십시오.
	- **단일 인스턴스 스타트업**: 스타트업해야 할 인스턴스를 선택하고 인스턴스 오른쪽에서 [더 보기]>[인스턴스 상태]>[스타트업]을 클릭합니다. 
![](https://main.qcloudimg.com/raw/5adf1eaf69be183707a56c60991bb73f.png)
	- **다중 인스턴스 스타트업**: 스타트업해야 하는 모든 인스턴스를 선택한 뒤, 리스트의 상단에서 [스타트업]을 클릭해 인스턴스를 일괄로 스타트업 하십시오.
![](https://main.qcloudimg.com/raw/e4514bfc1e524e353737414d018a575b.png)

### API를 통해 인스턴스 스타트업 하기
[StartInstances](https://intl.cloud.tencent.com/document/product/213/33236) 인터페이스를 참조하십시오.

## 후속 작업
다음의 작업은 인스턴스를 스타트업 했을 경우에만 실행할 수 있습니다.
- **인스턴스 로그인**: 인스턴스 운영 체제에 따라. [Linux 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5436)과 [Windows 인스턴스 로그인](https://intl.cloud.tencent.com/document/product/213/5435)을 참조하십시오.
- **[클라우드 디스크 초기화](https://intl.cloud.tencent.com/document/product/362/31596)**: 마운트된 클라우드 디스크에 포맷, 파티션, 파일 시스템 작성 등의 초기화 작업을 실행합니다.
