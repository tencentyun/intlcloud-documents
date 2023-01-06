## 작업 시나리오
본문에서는 DTS의 데이터 마이그레이션 기능을 사용하여 다른 루트 계정에서 원본 및 대상 TencentDB 인스턴스 간에 데이터 마이그레이션을 수행하는 방법을 설명합니다.

## 지원 범위
원본 데이터베이스가 TencentDB for MySQL/MongoDB/PostgreSQL인 데이터 마이그레이션 시나리오.

## 전제 조건
대상 데이터베이스 인스턴스를 생성 완료해야 합니다.

## 주의 사항
이 작업에는 여러 계정 정보 구성 항목이 포함됩니다. 다음은 더 쉬운 이해와 구성을 위한 주요 구성 로직을 나열합니다.

- 데이터 마이그레이션 방향 : 원본 데이터베이스(다른 계정의 데이터베이스 인스턴스) > 대상 데이터베이스(현재 계정의 데이터베이스 인스턴스).
- 마이그레이션 작업을 수행하는 계정은 대상 데이터베이스의 루트 계정 또는 서브 계정일 수 있습니다.
  - 루트 계정을 사용하여 마이그레이션 작업을 실행해야 합니다. 작업을 실행하기 전에 원본 데이터베이스의 루트 계정에 대상 데이터베이스의 루트 계정에 원본 데이터베이스에 대한 액세스 권한을 부여하도록 요청합니다.
  - 서브 계정을 사용하여 마이그레이션 작업을 실행하는 경우 작업을 실행하기 전에 원본 데이터베이스의 루트 계정에 대상 데이터베이스의 루트 계정에 역할이 있는 원본 데이터베이스에 대한 액세스 권한을 부여하도록 요청한 다음 대상 데이터베이스의 루트 계정에 원본 데이터베이스에 대한 서브 계정 액세스 권한을 부여하도록 요청합니다.

## [계정 권한 부여](id:sqzh)
**루트 계정 또는 서브 계정으로 마이그레이션 작업을 실행하려면 각각 1 - 6단계 또는 1 - 11단계를 따르십시오.**

1. 원본 데이터베이스의 Tencent Cloud 루트 계정으로 [CAM 콘솔](https://console.cloud.tencent.com/cam/role)에 로그인합니다(서브 계정에 CAM 및 역할 권한이 있는 경우 서브 계정으로 로그인할 수도 있습니다).
2. 왼쪽 사이드바의 **역할**을 클릭하여 역할 관리 페이지로 이동합니다. 그 다음 **역할 생성**을 클릭합니다.
3. 역할 엔터티 선택 페이지에서 **Tencent Cloud 계정**을 선택합니다.<br>
   <img src="https://qcloudimg.tencent-cloud.cn/raw/0a085bbeedc2404ec651c380d1c51513.png" style="zoom:40%;" />
4. **역할 엔터티 정보 입력** 페이지에서 정보를 구성하고 **다음**을 클릭합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/af0d0335bc18ba1dffe9a52c72505c3e.png)
   - Tencent Cloud 계정: **기타 루트 계정**을 선택합니다.
   - 계정 ID: **[계정 정보](https://console.cloud.tencent.com/developer)**에서 볼 수 있는 대상 데이터베이스의 Tencent Cloud 루트 계정 ID를 입력합니다. 대상 데이터베이스가 서브 계정에 의해 소유된 경우에도 여기에 루트 계정 ID를 입력해야 합니다.
   - 외부 ID : 필요에 따라 활성화할 수 있습니다.  
>?외부 ID를 사용하는 경우 DTS에서 조회할 수 없으므로 ID를 직접 기록하여 보관하십시오.
5. **역할 정책 구성** 페이지에서 DTS 정책과 원본 데이터베이스 서비스에 해당하는 정책을 선택하고 **다음**을 클릭합니다.
 - DTS 정책은 QcloudDTSReadOnlyAccess(Data Transfer Service(DTS) 읽기 전용 액세스)를 선택합니다.
 - 원본 데이터베이스의 해당 정책은 해당 원본 데이터베이스가 속한 Tencent Cloud 서비스의 정책을 선택합니다. 예를 들어 원본 데이터베이스가 TencentDB for MySQL 또는 PostgreSQL인 경우 각각 QcloudAccessForMySQLRole 또는 QcloudPostgreSQLReadOnlyAccess를 선택합니다. 실제 조건에 따라 정책을 선택하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/26ccc7c5c91ab4f513ba134767b81d35.png)
6. 역할 태그를 구성합니다. 그런 다음 **검토** 페이지에서 역할 이름을 설정하고 **완료**를 클릭합니다.
>?구성된 역할 이름을 기록해 두십시오. 추후 마이그레이션 작업을 생성할 때 입력해야 합니다.
>
![](https://qcloudimg.tencent-cloud.cn/raw/7f21bb7c56d5ad2712d6571fc4cff532.png)
>?루트 계정으로 마이그레이션 작업을 실행하려면 위 단계를 따르십시오. 서브 계정으로 동기화 작업을 실행하려면 루트 계정에 다음과 같이 서브 계정 권한 부여를 요청해야 합니다.
7. (옵션)대상 데이터베이스의 Tencent Cloud 루트 계정으로 [CAM 콘솔](https://console.cloud.tencent.com/cam/role)에 로그인한 후 **정책**을 클릭합니다. 그런 다음 오른쪽의 **사용자 정의 정책 생성**을 클릭하고 **정책 구문으로 생성**을 선택합니다.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/203282357c80ce91222ffaf430a5a558.png" style="zoom:40%;" />      
8. (옵션) **빈 템플릿**을 선택하고 **다음**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/476f823438c7bc16120b44078c6926cb.png)  
9. (옵션) 정책을 생성하고 필요에 따라 정책 이름 및 설명을 입력합니다. 정책 내용에 샘플 코드를 복사한 후, 빨간 박스 안의 내용을 실제 정보로 교체하십시오.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/7956d47a1b0588a0cda26a9463a6b02b.png" style="zoom:50%;" />
<br>샘플 정책 구문:  
```
{
    "version": "2.0",
    "statement": [
    {
        "effect": "allow",
        "action": ["name/sts:AssumeRole"],
  "resource": ["qcs::cam::uin/10*******8:roleName/DTS-role"]
    }
 ]
}
```
10. (옵션) **완료**를 클릭하고 정책 목록 페이지로 돌아간 다음 **사용자/그룹 연결**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/0a36bf46c25027a727f61829f4a8eacd.png) 
11. (옵션) 대상 데이터베이스 인스턴스의 서브 계정(즉, 마이그레이션 작업을 실행하는 서브 계정)을 선택하고 아래와 같이 **확인**을 클릭합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/2b1498e12917e9bc0ba5c82b8a248d1b.png" style="zoom:80%;" />

## 마이그레이션 작업 생성
1. 대상 데이터베이스 인스턴스의 Tencent Cloud 계정으로 [DTS 콘솔](https://console.cloud.tencent.com/dts/overview)에 로그인합니다.
2. **데이터 마이그레이션** > **마이그레이션 작업 생성**을 선택하여 마이그레이션 작업을 구매합니다.
3. 구매 후 데이터 마이그레이션 목록으로 돌아가 **작업** 열에서 **구성**을 클릭하여 마이그레이션 작업 구성 페이지로 이동합니다.
4. 원본 및 대상 데이터베이스 설정 페이지에서 원본 및 대상 데이터베이스 정보를 구성합니다. 다음은 두 TencentDB for MySQL 인스턴스 간의 데이터 마이그레이션을 예로 들어 설명합니다.
   ![](https://qcloudimg.tencent-cloud.cn/raw/3ad50fd1ffaf4794a1bb6a9b9058ba06.png)
   교차 계정 데이터 동기화를 위한 주요 매개변수를 다음과 같이 구성합니다.
   - 액세스 유형: **데이터베이스**를 선택하여 원본 데이터베이스가 TencentDB 인스턴스임을 나타냅니다.
   - 교차/내부 계정: **교차 계정**을 선택합니다.
   - 피어 계정 ID: 원본 데이터베이스의 루트 계정 ID를 입력합니다.
   - 피어 계정 역할 이름: [계정 권한 부여](#sqzh)의 6단계에서 생성한 **역할 이름**. 역할에 대한 자세한 내용은 [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) 및 [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148)을 참고하십시오.
   - 외부 역할 ID: 이 매개변수는 선택 사항이며 해당 값은 이전 섹션에서 가져올 수 있습니다. 역할에 대한 자세한 내용은 [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) 및 [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148)을 참고하십시오.
>?상기 구성을 완료한 후 **리전**을 선택하여 원본 데이터베이스 계정의 인스턴스 목록을 가져옵니다. 인스턴스를 가져오는 동안 오류가 발생하면 구성이 올바르지 않거나 권한 부여가 수행되지 않았을 수 있습니다. 자세한 내용은 [FAQ](#cjwt)를 참고하십시오.
5. 마이그레이션 옵션 설정 및 마이그레이션 객체 선택 페이지에서 데이터 마이그레이션 옵션을 설정하고 마이그레이션 객체를 선택한 후 **저장 후 다음으로 이동**을 클릭합니다.
6. 확인 작업 페이지에서 확인을 완료하고 모든 점검 항목이 통과되면 **작업 실행**을 클릭합니다.
   확인이 실패한 경우 [검증 불통과 처리 방법](https://intl.cloud.tencent.com/document/product/571/42551)의 설명 대로 문제를 수정하고 확인 작업을 다시 시작합니다.
7. 데이터 마이그레이션 작업 리스트로 돌아가면 작업이 **실행 중** 상태로 들어간 것을 확인할 수 있습니다.

## [FAQ](id:cjwt)
#### 1. 여러 계정에서 인스턴스 목록을 가져올 때 role not exist[InternalError.GetRoleError] 오류가 보고되면 어떻게 해야 합니까?
**피어 계정 ID**(원본 데이터베이스의 루트 계정 ID)와 **피어 계정 역할 이름**([계정 권한 부여](#sqzh)의 6단계에서 생성된 **역할 이름**)이 올바르게 구성되었습니다.

#### 2. 인스턴스 목록에 대한 CDB 가져오기 실패: InternalError:InternalInnerCommonError


권한 부여 원본 데이터베이스가 해당 역할에 속한 Tencent Cloud 서비스 정책이 없습니다. 권한 부여는 [계정 권한 부여](#sqzh)의 5단계를 참고하십시오.


#### 3. 여러 계정에서 인스턴스 목록을 가져올 때 you are not authorized to perform operation (sts:AssumeRole) ，resource (qcs::cam::uin/1xx5:roleName/xxxx) has no permission 오류가 보고되면 어떻게 해야 합니까?


**오류 원인**: 마이그레이션 작업을 생성하는 데 사용하는 계정은 sts:AssumeRole 권한이 없는 서브 계정입니다.
**솔루션**:

- 루트 계정을 사용하여 마이그레이션 작업을 생성합니다.
- 대상 데이터베이스의 루트 계정에 [계정 권한 부여](#sqzh) 지침에 따라 서브 계정에 권한을 부여하도록 요청하고 정책 구문의 resource를 오류 메시지의 파란색 필드로 설정합니다.
  
