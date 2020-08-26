[MySQL 콘솔](https://console.cloud.tencent.com/cdb) 또는 [API](https://intl.cloud.tencent.com/document/product/236/15860)를 통해 일부 매개변수를 조회 및 수정할 수 있으며 콘솔에서 매개변수 수정 기록 또한 조회할 수 있습니다.

## 매개변수 값 수정
>!
>- 수정된 매개변수를 적용하기 위해 인스턴스를 재시작해야 한다면 시스템에서 재시작 여부에 대한 알림을 표시하므로, 응용 프로그램의 재연결 메커니즘을 확인하고 비즈니스 사용량이 가장 적은 시간대에 작업하시길 권장합니다.
>- 매개변수 수정을 제출하기 전, 매개변수 옆의 <img src="https://main.qcloudimg.com/raw/81fc2494e8b61ff36a63d23cccb61cd1.png"  style="margin:0;"> 혹은 수정 페이지의 [취소]를 클릭하여 수정을 취소할 수 있습니다.

### 매개변수 일괄 수정
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, Instance List에서 인스턴스 이름 혹은 작업 열의 [관리]를 클릭하여 인스턴스 관리 페이지에 접속합니다.
2. [데이터베이스 관리]>[매개 변수 설정]에서 [매개변수 일괄 수정]을 클릭합니다.
![](https://main.qcloudimg.com/raw/3ec389dafa09276ae66b00a71445d9d3.png)
3. '매개변수 실행값' 열에서 수정이 필요한 매개변수를 수정하고 착오가 없는지 확인한 뒤, [수정 확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/5307fbeef4b1fccef478ab7fd57b3167.png)
4. 팝업된 대화 상자에서 동의를 선택한 뒤, [확인]을 클릭합니다.

### 단일 매개변수 수정
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, Instance List에서 인스턴스 이름 혹은 작업 열의 [관리]를 클릭하여 인스턴스 관리 페이지에 접속합니다.
2. [데이터베이스 관리]>[매개 변수 설정]에서 수정이 필요한 타깃 매개변수를 선택한 뒤, '매개변수 실행값' 열의 <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> 모양을 클릭하여 매개변수 값을 수정합니다.
![](https://main.qcloudimg.com/raw/4687ed705274b76ec92c43b7f9d448ab.png)
3. '매개변수 수정 가능 값' 열의 안내에 따라 타깃 매개변수 값을 입력한 뒤, <img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;"> 모양을 클릭하면 수정된 값이 저장되고, <img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;"> 모양을 클릭하면 작업이 취소됩니다.
![](https://main.qcloudimg.com/raw/41c7d73d4c5d404a112f54c3a63da726.png)
4. 팝업된 대화 상자에서 [확인]을 클릭합니다.

### 사용자 정의 시간에 매개변수 수정
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, Instance List에서 인스턴스 이름 혹은 작업 열의 [관리]를 클릭하여 인스턴스 관리 페이지에 접속합니다.
2. [데이터베이스 관리]>[매개 변수 설정]에서 [매개변수 일괄 수정]을 클릭하거나 '매개변수 실행값' 열에서 <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> 모양을 클릭하여 단일 매개변수 값을 수정합니다.  
3. 수정한 매개변수 값에 착오가 없는지 확인한 뒤, [수정 확인]을 클릭하거나 <img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;"> 모양을 클릭하여 저장합니다.
4. 팝업된 대화 상자에서 매개변수의 '실행 모드'를 선택한 뒤, [확인]을 클릭합니다.
>?[유지보수 시간 내]를 선택하면 인스턴스의 [유지보수 시간](https://intl.cloud.tencent.com/document/product/236/10929) 내에서 매개변수 수정 작업이 실행 및 적용됩니다.
>


### 매개변수 수정 작업 취소
매개변수 일괄 수정 혹은 단일 매개변수 수정 작업을 제출한 후, 매개변수의 수정을 취소하고 싶다면 작업이 실행되기 전('실행 대기' 상태)에 왼쪽 사이드바의 [Task List](https://console.cloud.tencent.com/mysql/task) 탭에서 '작업' 열의 [취소]를 클릭하여 매개변수 수정 작업을 취소할 수 있습니다.

### 매개변수 템플릿에서 가져오기
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, Instance List에서 인스턴스 이름 혹은 작업 열의 [관리]를 클릭하여 인스턴스 관리 페이지에 접속합니다.
2. [데이터베이스 관리]>[매개 변수 설정]에서 [템플릿에서 가져오기]를 클릭합니다.
![](https://main.qcloudimg.com/raw/bd7a2fd3dc89895f1a3bd779d0fe8bbc.png)
3. 팝업된 대화 상자에서 매개변수 템플릿을 선택한 후, [가져오고 기존의 매겨변수를 덮어쓰기]를 클릭합니다.
![](https://main.qcloudimg.com/raw/2f649840f16befabea6259f9b4c7f47c.png)

### 매개변수 가져오기
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, Instance List에서 인스턴스 이름 혹은 작업 열의 [관리]를 클릭하여 인스턴스 관리 페이지에 접속합니다.
2. [데이터베이스 관리]>[매개 변수 설정]에서 [매개변수 가져오기]를 클릭합니다.
![](https://main.qcloudimg.com/raw/52d6f069bbce29c933254593d59c0236.png)
3. 팝업된 대화 상자에서 업로드할 파일을 선택한 후, [가져오고 기존의 매겨변수를 덮어쓰기]를 클릭합니다.
![](https://main.qcloudimg.com/raw/42fb6ef8936131a3bc776e492478e745.png)
	
## 매개변수 수정 기록 조회
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, Instance List에서 인스턴스 이름 혹은 작업 열의 [관리]를 클릭하여 인스턴스 관리 페이지에 접속합니다.
2. [데이터베이스 관리]>[매개 변수 설정]에서 오른쪽의 [마지막 수정 기록]을 클릭합니다.
![](https://main.qcloudimg.com/raw/6d6318fce61fc78c6ff3611479ae5714.png)
3. 아래의 이미지와 같이 최근 매개변수 수정 기록을 조회할 수 있습니다.
![](https://main.qcloudimg.com/raw/4c616b40d058f114e8f75c4021c02648.png)

## 후속 작업
- 중요 매개변수 설정에 대한 내용은 [매개변수 설정 제안](https://intl.cloud.tencent.com/document/product/238/38051)을 참조 바랍니다.
