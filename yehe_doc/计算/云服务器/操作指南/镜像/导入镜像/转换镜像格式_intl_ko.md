## 작업 시나리오
현재 Tencent Cloud CVM은 RAW, VHD, QCOW2, VMDK와 같은 이미지 파일 형식 가져오기를 지원합니다. 다른 형식의 이미지 파일은 가져오기 전에 변환해야 합니다. 본 문서는 qemu-img 툴을 사용하여 다른 형식의 이미지 파일을 VHD 또는 RAW 형식으로 변환하는 방법을 설명합니다.

## 작업 단계
실제 운영 체제에 따라 해당 작업 단계를 선택할 수 있습니다.
<dx-tabs>
::: Windows 운영 체제[](id:windows)
<dx-alert infotype="explain" title="">
본문은 Windows 10 운영 체제를 예로 들어 이미지 형식을 변환합니다. 운영 체제 버전에 따라 약간의 차이가 있으므로 실제 상황에 따라 설명서를 참고하십시오.
</dx-alert>


#### qemu-img 설치
[qemu-img 다운로드 주소](https://qemu.weilnetz.de/w64/?spm=a2c4g.11186623.0.0.52164204ykdbP9)로 이동하여 다운로드하여 설치를 완료하십시오. 본문은 `C:\Program Files\qemu`에 설치를 예로 들어 설명합니다.


#### 환경 변수 설정
1. **시작**을 우클릭하고, 팝업 메뉴에서 **시스템**을 선택합니다.
2. 팝업 창에서 **고급 시스템 설정**을 선택합니다.
3. 팝업된 ‘시스템 속성’ 창에서 **고급** 탭을 선택하고 **환경 변수**를 클릭합니다.
4. ‘환경 변수’ 창의 ‘시스템 변수’에서 `Path`를 선택하고 **편집**을 클릭합니다. 아래 이미지와 같습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d23a111449b96d2f97615bcc5431b9f4.png)
5. 팝업된 ‘환경 변수 편집’ 창에서 생성을 클릭한 후, qemu-img `C:\Program Files\qemu`의 설치 경로를 입력하고 **확인**을 클릭합니다.
6. ‘환경 변수’ 창에서 **확인**을 다시 클릭합니다.

#### 환경 변수 설정 인증
1. **Win + R**을 눌러 실행 창을 엽니다.
2. ‘실행’ 창에서 **cmd**를 입력하여 명령 라인을 엽니다.
3. 다음 명령을 실행하고 반환 결과에 따라 환경 변수가 성공적으로 설정되었는지 여부를 판단합니다.
```
qemu-img --help
```

#### 이미지 형식 변환
1. 명령줄에서 다음 명령을 실행하여 이미지 파일이 있는 디렉터리로 전환합니다.
```
cd <원본 이미지 파일이 있는 디렉터리>
```
2. 다음 명령을 실행하여 이미지 형식을 변환합니다.
```
qemu-img convert -f <원본 이미지 파일 형식> -O <타깃 이미지 형식> <원본 이미지 파일 이름> <타깃 이미지 파일 이름>
```
매개변수 설명은 다음과 같습니다.
 - `-f`: 매개변수 값은 원본 이미지 파일의 형식입니다. 
 - `-O`(대문자여야 함): 매개변수 값은 타깃 이미지 형식, 원본 이미지 파일 이름 및 타깃 파일 이름입니다.
예를 들어 다음 명령을 실행하여 `test.qcow2` 이미지 파일을 `test.raw`로 변환합니다.
```
qemu-img convert -f qcow2 -O raw test.qcow2 test.raw
```
변환이 완료되면 타깃 파일이 원본 이미지 파일이 있는 디렉터리에 나타납니다.

:::
::: Linux 운영 체제[](id:linux)
<dx-alert infotype="explain" title="">
본문은 Ubuntu 20.04 및 CentOS 7.8 운영 체제를 예로 들어 이미지 형식을 변환합니다. 운영 체제 버전에 따라 약간의 차이가 있으므로 실제 상황에 따라 설명서를 참고하십시오.
</dx-alert>

#### qemu-img 설치
1. 다음 명령을 실행하여 qemu-img를 설치합니다.
 - Ubuntu：
 ```
 apt-get update #패키지 목록 업데이트
 ```
 ```
 apt-get install qemu-utils #qemu-img 툴 설치
 ```
 - CentOS：
 ```
 yum install qemu-img
 ```
2. 다음 명령을 실행하여 이미지 형식을 변환합니다.
```
qemu-img convert -f qcow2 -O raw test.qcow2 test.raw
```
매개변수 설명은 다음과 같습니다.
 - `-f`: 매개변수 값은 원본 이미지 파일 형식입니다. 
 - `-O`(대문자여야 함): 매개변수 값은 타깃 이미지 형식, 원본 이미지 파일 이름 및 타깃 파일 이름입니다.
변환이 완료되면 타깃 파일이 원본 이미지 파일이 있는 디렉터리에 나타납니다.
:::
</dx-tabs>

## 관련 문서
- [미러 이미지 가져오기 개요](https://intl.cloud.tencent.com/document/product/213/4945)
- [Windows 이미지 제작](https://intl.cloud.tencent.com/document/product/213/17815)
- [Linux 이미지 제작](https://intl.cloud.tencent.com/document/product/213/17814)



