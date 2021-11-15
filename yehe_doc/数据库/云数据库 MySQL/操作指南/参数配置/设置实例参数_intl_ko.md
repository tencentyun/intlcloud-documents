[MySQL 콘솔](https://console.cloud.tencent.com/cdb)을 통해 일부 매개변수를 조회 및 수정할 수 있으며 콘솔에서 매개변수 수정 기록 또한 조회할 수 있습니다.

## 주의 사항
- 인스턴스 안정성 확보를 위해 콘솔은 일부 매개변수의 수정만 허용합니다. 콘솔의 매개변수 설정 페이지에 보여지는 매개변수는 사용자가 수정할 수 있는 매개변수입니다.
- 수정된 매개변수를 적용하기 위해 인스턴스를 재시작해야 한다면 시스템에서 재시작 여부에 대한 알림을 표시하므로, 응용 프로그램의 재연결 메커니즘을 확인하고 비즈니스 사용량이 가장 적은 시간대에 작업하시길 권장합니다.

## 매개변수 리스트를 통해 매개변수 수정하기

<span id = "plxgcs"></span>
### 매개변수 일괄 수정
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 인스턴스 리스트에서 인스턴스 명칭 혹은 '작업'열의 [관리]를 클릭하여 인스턴스 관리 페이지에 접속합니다.
2. [데이터베이스 관리]>[매개변수 설정]에서 [매개변수 일괄 수정]를 클릭합니다.
![](https://main.qcloudimg.com/raw/82c535bd50543645831988ca2e9b688e.png)
3. 'Current Value' 열에서 수정이 필요한 매개변수를 수정하고 착오가 없는지 확인한 뒤, [Confirm Modification]을 클릭합니다.
![](https://main.qcloudimg.com/raw/5307fbeef4b1fccef478ab7fd57b3167.png)
4. 팝업된 대화 상자에서 매개변수 작업의 '실행 방식'을 선택한 뒤, [확인]을 클릭합니다.
>?
>- [지금 실행]을 선택하면 선택된 인스턴스의 매개변수 수정 작업이 즉시 실행 및 적용됩니다.
>- [점검 시간 내]를 선택하면 인스턴스의 [점검 시간](https://intl.cloud.tencent.com/document/product/236/10929)에서 매개변수 수정 작업이 실행 및 적용됩니다.
>

<span id = "xgdgcs"></span>
### 단일 매개변수 수정
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 인스턴스 리스트에서 인스턴스 이름을 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. [데이터베이스 관리]>[매개변수 설정]에서 수정이 필요한 타깃 매개변수를 선택한 뒤, '매개변수 실행값' 열의 <img src="https://main.qcloudimg.com/raw/788902e3f8c335cf17de420f7181c2a8.png"  style="margin:0;"> 모양을 클릭하여 매개변수 값을 수정합니다.
![](https://main.qcloudimg.com/raw/4687ed705274b76ec92c43b7f9d448ab.png)
3. '매개변수 수정 가능 값' 열의 안내에 따라 타깃 매개변수 값을 입력한 뒤, <img src="https://main.qcloudimg.com/raw/1f4c7f2e0744bc601efb5d9fb04a7a04.png"  style="margin:0;"> 모양을 클릭하면 수정된 값이 저장되고, <img src="https://main.qcloudimg.com/raw/2106cb4b9337a1a2fff5908581d2a908.png"  style="margin:0;"> 모양을 클릭하면 작업이 취소됩니다.
![](https://main.qcloudimg.com/raw/41c7d73d4c5d404a112f54c3a63da726.png)
4. 팝업된 대화 상자에서 매개변수 작업의 '실행 방식'을 선택한 뒤, [확인]을 클릭합니다.
>?
>- [지금 실행]을 선택하면 선택된 인스턴스의 매개변수 수정 작업이 즉시 실행 및 적용됩니다.
>- [점검 시간 내]를 선택하면 인스턴스의 [점검 시간](https://intl.cloud.tencent.com/document/product/236/10929)에서 매개변수 수정 작업이 실행 및 적용됩니다.
>


## 매개변수 템플릿 가져오기로 매개변수 수정하기
### 방법 1: [매개변수 설정] 페이지를 통해 가져오기
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 인스턴스 리스트에서 인스턴스 이름을 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. [데이터베이스 관리]>[매개 변수 설정]에서 [템플릿에서 가져오기]를 클릭합니다.
![](https://main.qcloudimg.com/raw/bd7a2fd3dc89895f1a3bd779d0fe8bbc.png)
3. 팝업된 대화 상자에서 매개변수 템플릿을 선택한 후, [가져오기 및 기존의 매개변수 덮어쓰기]를 클릭합니다.
![](https://main.qcloudimg.com/raw/2f649840f16befabea6259f9b4c7f47c.png)
4. 매개변수를 확인한 후에 [수정 확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/1673166256bc4d122f5a72c3c703ffab.png)
5. 팝업된 대화 상자에서 매개변수 작업의 '실행 방식'를 선택한 뒤, [확인]을 클릭합니다.
>?
>- [지금 실행]을 선택하면 선택된 인스턴스의 매개변수 수정 작업이 즉시 실행 및 적용됩니다.
>- [점검 시간 내]를 선택하면 인스턴스의 [점검 시간](https://intl.cloud.tencent.com/document/product/236/10929)에서 매개변수 수정 작업이 실행 및 적용됩니다.
>


### 방법 2: [매개변수 템플릿] 페이지를 통해 가져오기
[매개변수 템플릿을 인스턴스에 적용하기](https://intl.cloud.tencent.com/document/product/236/31906#.E5.BA.94.E7.94.A8.E5.8F.82.E6.95.B0.E6.A8.A1.E6.9D.BF.E4.BA.8E.E5.AE.9E.E4.BE.8B)를 참조하십시오.

## 매개변수 설정 파일 가져오기로 매개변수 수정하기
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 인스턴스 리스트에서 인스턴스 이름을 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. [데이터베이스 관리]>[매개 변수 설정]에서 [매개변수 가져오기]를 클릭합니다.
![](https://main.qcloudimg.com/raw/52d6f069bbce29c933254593d59c0236.png)
3. 팝업된 대화 상자에서 업로드할 매개변수 파일을 선택한 후, [가져오기 및 기존의 매개변수 덮어쓰기]를 클릭합니다.
![](https://main.qcloudimg.com/raw/42fb6ef8936131a3bc776e492478e745.png)
4. 매개변수를 확인한 후에 [수정 확인]을 클릭합니다.
![](https://main.qcloudimg.com/raw/1673166256bc4d122f5a72c3c703ffab.png)
5. 팝업된 대화 상자에서 매개변수 작업의 '실행 방식'를 선택한 뒤, [확인]을 클릭합니다.
>?
>- [지금 실행]을 선택하면 선택된 인스턴스의 매개변수 수정 작업이 즉시 실행 및 적용됩니다.
>- [점검 시간 내]를 선택하면 인스턴스의 [점검 시간](https://intl.cloud.tencent.com/document/product/236/10929)에서 매개변수 수정 작업이 실행 및 적용됩니다.
>


## 매개변수 설정 파일 내보내기
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 인스턴스 리스트에서 인스턴스 이름을 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. [데이터베이스 관리]>[매개 변수 설정]에서 [매개변수 내보내기]를 클릭해서 매개변수 구성 파일을 내보냅니다.
![](https://main.qcloudimg.com/raw/6885ffbc45f3154ed203551a309e1848.png)

## 매개변수 설정을 매개변수 템플릿으로 내보내기
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 인스턴스 리스트에서 인스턴스 이름을 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. [데이터베이스 관리]>[매개변수 설정]에서 [템플릿으로 저장]을 클릭하면 매개변수 설정을 매개변수 템플릿으로 저장할 수 있습니다.
![](https://main.qcloudimg.com/raw/fca4ec16b316948af812db9988d0c92c.png)

## 사용자 정의 시간에 매개변수 수정
매개변수 수정 작업 마지막 단계를 수행할 때 팝업된 대화 상자에서 매개변수의 수정 시간을 설정할 수 있습니다.
>? [점검 시간 내]를 선택하면 인스턴스의 [점검 시간](https://intl.cloud.tencent.com/document/product/236/10929)에서 매개변수 수정 작업이 실행 및 적용됩니다.
>
![](https://main.qcloudimg.com/raw/00d4892fb614dd285cdec91a4a74cf2d.png)


## 매개변수 수정 작업 취소
[점검 시간 내]의 매개변수 수정 작업을 제출한 후 매개변수의 수정을 취소하고 싶다면, 작업이 실행되기 전에('Waiting for execution' 상태) 왼쪽 사이드바의 [[작업 리스트](https://console.cloud.tencent.com/mysql/task)] 탭에서 '작업'열의 [취소]를 클릭하여 매개변수 수정 작업을 취소할 수 있습니다.
![](https://main.qcloudimg.com/raw/566fd9374d0d59b38ceb99d310b782a9.png)


## 매개변수 수정 기록 조회
1. [MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인한 뒤, 인스턴스 리스트에서 인스턴스 이름을 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. [데이터베이스 관리]>[매개 변수 설정]에서 오른쪽의 [마지막 수정 기록]을 클릭합니다.
![](https://main.qcloudimg.com/raw/93494ebb3b80a6547f1c6fe7bcbf9c8a.png)
3. 아래의 이미지와 같이 최근 매개변수 수정 기록을 조회할 수 있습니다.


## 후속 작업
- 데이터베이스 매개변수 템플릿을 사용하여 데이터베이스의 매개변수 설정을 일괄적으로 관리할 수 있으며, 자세한 내용은 [매개변수 템플릿 사용](https://intl.cloud.tencent.com/document/product/236/31906)을 참조 바랍니다.
- 중요 매개변수 설정에 대한 내용은 [매개변수 설정 제안](https://intl.cloud.tencent.com/document/product/236/38056)을 참조 바랍니다.
