TencentDB for MySQL은 데이터베이스 액세스 비밀번호의 강도를 높이고 데이터베이스 보안을 보장하기 위해 비밀번호 복잡도 설정을 지원합니다.

## 전제 조건
- 데이터베이스 버전:
 - MySQL 5.6, 마이너 버전 20201231 이상.
 - MySQL 5.7, 마이너 버전 20201231 이상.
 - MySQL 8.0, 마이너 버전 20201230 이상.

- 2노드/3노드 인스턴스 아키텍처.

## 주의 사항
MySQL 콘솔을 통해 계정을 생성하고 비밀번호를 설정하거나 계정 비밀번호를 재설정할 때 비밀번호 복잡도 설정 정책은 다음과 같은 초기 계정 비밀번호 제한을 위반할 수 없습니다.
- 길이는 8 - 64자 이내여야 합니다.
- 알파벳 대소문자, 숫자, 특수 기호 중 세 가지로 구성합니다.
- 특수 기호는 `_+-&=!@#$%^*()` 입니다.

## 비밀번호 복잡도 활성화
>?비밀번호 복잡도 기능이 활성화된 후, 새로운 계정을 생성하거나 재설정할 때 새로운 비밀번호 복잡도 정책에 따라 비밀번호가 설정됩니다.

### 구매 페이지에서 인스턴스 생성 시 활성화
1. [MySQL 구매 페이지](https://buy.intl.cloud.tencent.com/cdb)에 로그인합니다.
2. 필요에 따라 다양한 매개변수를 구성하고 **비밀번호 복잡도** 매개변수 항목 다음에 **활성화**를 선택합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/d8954b4267f8b9c75b3f33834c8a8ad5.png)
3. 활성화 선택 후 다음 설정을 완료합니다.
<table>
<thead><tr><th>매개변수</th><th>설명</th></tr></thead>
<tbody><tr>
<td>소문자 및 대문자의 최소 글자 수</td>
<td>1 - 16자, 기본값: 1</td></tr>
<tr>
<td>숫자의 최소 글자 수</td>
<td>1 - 16자, 기본값: 1</td></tr>
<tr>
<td>특수 문자 최소 글자 수</td>
<td>1 - 16자, 기본값: 1</td></tr>
<tr>
<td>비밀번호 최소 글자 수</td>
<td>8 - 64자로, 기본값은 8이며, 최소값은 위의 세 매개변수의 최소 글자 수의 합보다 커야 합니다.</td></tr>
</tbody></table>

### 콘솔에서 기존 인스턴스 열기
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인 후, 인스턴스 리스트에서 인스턴스 ID 또는 **작업**열의 **관리**를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 **데이터베이스 관리** > **Manage Account** 페이지를 선택하고 **비밀번호 복잡도**(기본값: 비활성화)를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ae8c348798736f38a4ea1069e29c7b5f.png)
3. 비밀번호 복잡도 팝업 창에서 활성화를 선택하고 다음 매개변수 설정을 완료한 후 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/f4407c8d310de235c596f541f087d747.png)
<table>
<thead><tr><th>매개변수</th><th>설명</th></tr></thead>
<tbody><tr>
<td>소문자 및 대문자의 최소 글자 수</td>
<td>1 - 16자, 기본값: 1</td></tr>
<tr>
<td>숫자의 최소 글자 수</td>
<td>1 - 16자, 기본값: 1</td></tr>
<tr>
<td>특수 문자 최소 글자 수</td>
<td>1 - 16자, 기본값: 1</td></tr>
<tr>
<td>비밀번호 최소 글자 수</td>
<td>8 - 64자로, 기본값은 8이며, 최소값은 위의 세 매개변수의 최소 글자 수의 합보다 커야 합니다.</td></tr>
</tbody></table>

## 비밀번호 복잡도 비활성화
1. [TencentDB for MySQL 콘솔](https://console.cloud.tencent.com/cdb)에 로그인 후, 인스턴스 리스트에서 인스턴스 ID 또는 **작업**열의 **관리**를 클릭하여 인스턴스 관리 페이지로 이동합니다.
2. 인스턴스 관리 페이지에서 **데이터베이스 관리** > **계정 관리** 탭을 선택하고 **비밀번호 복잡도**를 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/ae613393746da572d25e4bc90e940895.png)
3. 비밀번호 복잡도 팝업 창에서 **비활성화**를 선택하고 **확인**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/06c7f71ceaacb063768ac6c83ab78b76.png)

## 관련 문서
- [계정 생성](https://intl.cloud.tencent.com/document/product/236/31900)
- [비밀번호 재설정](https://intl.cloud.tencent.com/document/product/236/31901)
