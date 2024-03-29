## 작업 시나리오
비디오 심사 페이지에는 미디어 자산에서 시작하고 태스크 플로우에서 설정한 심사 작업의 결과를 포함한 비디오 심사 결과가 표시됩니다.

## 작업 단계

1. [VOD 콘솔](https://console.cloud.tencent.com/vod/overview)에 로그인한 후, 왼쪽 사이드바에서 [비디오 심사]를 클릭하여 비디오 심사 페이지로 들어갑니다.
![](https://main.qcloudimg.com/raw/f3d1b953ef6f8fc4f2a16910f18a079d.png)
	- 기간별 조회: 오늘, 어제, 최근 7일 동안의 비디오 심사 결과 및 최근 7일 이내의 모든 기간에 대한 비디오 심사 결과를 비디오 심사 목록에서 조회할 수 있습니다.
	- 접두사 검색: FileId 또는 비디오 이름 접두사로 심사 결과를 검색할 수 있습니다.
	- 필터: 비디오 파일을 시간에 따라 오름차순 또는 내림차순으로 정렬하고 심사 상태, 기계 심사 결과 또는 수동 확인 결과를 필터링할 수 있습니다.
	- 삭제: 대상 비디오 파일을 선택하고 목록 위의 [삭제]를 클릭하여 일괄 삭제합니다. 또는 단일 파일의 행에서 [삭제]를 클릭하여 개별 삭제합니다.
	
>?비디오 심사 결과를 얻으려면 미디어 자산에서 [비디오 심사](https://intl.cloud.tencent.com/document/product/266/33892)를 시작해야 합니다.

2. 대상 비디오 파일이 있는 행의 [결과 조회]를 클릭하여 ‘심사 결과’ 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/8f92f1853c4fc5151fda3ba689708064.png)
	- 내용 표시: 이 페이지는 작업 ID, 비디오 파일 이름, 원본 비디오 파일 URL, 기계 심사 결과, 수동 확인 결과 및 기계 심사 결과의 세부 정보를 표시합니다.
	- 비디오 정보 복사: 작업 ID, 비디오 파일 이름, 원본 비디오 파일 URL을 복사할 수 있습니다.
	- 심사 결과 확인:
		- [통과 확인]을 클릭하면 비디오에 규정 위반 사항이 없고 수동 심사 결과가 ‘통과’임을 확인합니다.
		- [위반 확인]을 클릭하면 비디오에 규정 위반 사항이 있고 수동 확인 결과가 ‘위반’임을 확인합니다.
		- [재심사]를 클릭하여 다른 심사 템플릿을 선택하고 심사 작업을 다시 시작하거나 또는 ‘비디오 심사’ 페이지의 대상 비디오 파일 행에서 [재심사]를 클릭합니다.
	- 심사 내용: VOD 비디오 심사 결과는 **MP4 형식의 비디오 미리보기**만 지원합니다. 심사 결과 내역은 태그 형태로 표시되며, 특정 심사 템플릿을 기반으로 심사 결과 및 세그먼트 신뢰도를 표시하여 [신뢰도 임계값 조정](https://intl.cloud.tencent.com/document/product/266/14059#yz)을 용이하게 합니다.
		




