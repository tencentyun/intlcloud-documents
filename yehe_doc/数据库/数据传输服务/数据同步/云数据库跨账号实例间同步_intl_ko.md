## 작업 시나리오
본문에서는 DTS의 데이터 동기화 기능을 사용하여 다른 루트 계정에서 원본 및 타깃 TencentDB 인스턴스 간에 데이터 동기화를 수행하는 방법을 설명합니다.

## 지원 범위
계정 간 데이터 동기화는 TencentDB for MySQL, TDSQL for MySQL, TDSQL-C 및 TencentDB for MariaDB 인스턴스 간에 지원되지만 MySQL과 CDWPG 인스턴스 간에는 지원되지 않습니다. 자세한 내용은 [데이터 동기화가 지원하는 데이터베이스](https://intl.cloud.tencent.com/document/product/571/42579)의 **계정 간 동기화**를 참고하십시오.

## 전제 조건
타깃 데이터베이스 인스턴스를 생성했습니다.

## 주의 사항
이 작업에는 여러 계정 정보 구성 항목이 포함됩니다. 다음은 더 쉬운 이해와 구성을 위한 주요 구성 로직을 나열합니다.
- 데이터 동기화 방향 : 원본 데이터베이스(다른 계정의 데이터베이스 인스턴스) > 타깃 데이터베이스(현재 계정의 데이터베이스 인스턴스).
- 동기화 작업을 수행하는 계정은 타깃 데이터베이스의 루트 계정 또는 서브 계정일 수 있습니다.
   - 루트 계정을 사용하여 동기화 작업을 실행해야 합니다. 작업을 실행하기 전에 원본 데이터베이스의 루트 계정에 타깃 데이터베이스의 루트 계정에 원본 데이터베이스에 대한 액세스 권한을 부여하도록 요청합니다.
   - 서브 계정을 사용하여 동기화 작업을 실행해야 합니다. 작업을 실행하기 전에 원본 데이터베이스의 루트 계정에 타깃 데이터베이스의 루트 계정에 원본 데이터베이스에 대한 액세스 권한을 부여한 다음 타깃 데이터베이스의 루트 계정에 요청하여 서브 계정에 원본 데이터베이스에 대한 액세스 권한을 부여합니다.

## [계정 권한 부여](id:sqzh)
**루트 계정 또는 서브 계정으로 동기화 작업을 실행하려면 각각 1 - 6단계 또는 1 - 11단계를 따르십시오.**

1. 원본 데이터베이스의 Tencent Cloud 루트 계정으로 [CAM 콘솔](https://console.cloud.tencent.com/cam/role)에 로그인합니다(서브 계정에 CAM 및 역할 권한이 있는 경우 서브 계정으로 로그인할 수도 있습니다).
2. 왼쪽 사이드바의 **역할**을 클릭하여 역할 관리 페이지로 이동합니다. 그 다음 **역할 생성**을 클릭합니다.
3. 역할 엔터티 선택 페이지에서 **Tencent Cloud 계정**을 선택합니다.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/383f4bd0086637b5346b03797d022a2e.png" style="zoom:90%;" />
4. **역할 엔터티 정보 입력** 페이지에서 정보를 구성하고 **다음**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/77f8a29b40f48f4e6cc77ed7f191af13.png)
   - Tencent Cloud 계정: **기타 루트 계정**을 선택합니다.
   - 계정 ID: **[계정 정보](https://console.cloud.tencent.com/developer)**에서 볼 수 있는 타깃 데이터베이스의 Tencent Cloud 루트 계정 ID를 입력합니다. 타깃 데이터베이스가 서브 계정에 의해 소유된 경우에도 여기에 루트 계정 ID를 입력해야 합니다.
   - 외부 ID : 필요에 따라 활성화할 수 있습니다.  
>?외부 ID를 사용하는 경우 DTS에서 조회할 수 없으므로 ID를 직접 기록하여 보관하십시오.
5. **역할 정책 구성** 페이지에서 DTS 정책과 원본 데이터베이스 서비스에 해당하는 정책을 선택하고 **다음**을 클릭합니다.
 - DTS 정책은 QcloudDTSReadOnlyAccess(Data Transfer Service(DTS) 읽기 전용 액세스)를 선택합니다.
 - 원본 데이터베이스 서비스에 해당하는 정책, 즉 원본 데이터베이스가 속한 Tencent Cloud 서비스 정책입니다. 예를 들어, 원본 데이터베이스가 TencentDB for MySQL인 경우 QcloudAccessForMySQLRole(TencentDB for MySQL 작업 권한)을 추가합니다. 다음은 TencentDB for MySQL을 예시로 사용합니다. 다른 시나리오의 경우 실제 상황에 따라 구성을 선택하십시오.
![](https://qcloudimg.tencent-cloud.cn/raw/5d039c19c35e1d8a107a023ed5321010.png)
6. **검토** 페이지에서 역할 이름을 설정하고 **완료**를 클릭합니다.
>?나중에 동기화 작업을 생성할 때 입력해야 하는 구성된 이름을 기록합니다.
>
![](https://qcloudimg.tencent-cloud.cn/raw/acb68a6dfa00e5ccd41fdd511a0fcfd6.png)
>?루트 계정으로 동기화 작업을 실행하려면 위 단계를 따르십시오. 서브 계정으로 동기화 작업을 실행하려면 루트 계정에 다음과 같이 서브 계정 권한 부여를 요청해야 합니다.
7. (옵션) 타깃 데이터베이스의 Tencent Cloud 서브 계정으로 [CAM 콘솔](https://console.cloud.tencent.com/cam/role)에 로그인한 후 **정책**을 클릭합니다. 그런 다음 오른쪽의 **사용자 정의 정책 생성**을 클릭하고 **정책 구문으로 생성**을 선택합니다.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/050a9318db3118de54ffefb57c144c12.png" style="zoom:90%;" />      
8. (옵션) **빈 템플릿**을 선택하고 **다음**을 클릭합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/3e779e1daa8394da22d8ee3200c10370.png)  
9. (옵션) 정책을 생성하고 필요에 따라 정책 이름 및 설명을 입력합니다. 정책 내용에 샘플 코드를 복사한 후, 빨간 박스 안의 내용을 실제 정보로 교체하십시오.<br>
<img src="https://qcloudimg.tencent-cloud.cn/raw/9f877d283df7104ab5be9506d338b4a3.png" style="zoom:50%;" />
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
![](https://qcloudimg.tencent-cloud.cn/raw/ad8eb259b437793ac5a8dfe20c97b627.png) 
11. (옵션) 타깃 데이터베이스 인스턴스의 서브 계정(즉, 동기화 작업을 실행하는 서브 계정)을 선택하고 아래와 같이 **확인**을 클릭합니다.
<img src="https://qcloudimg.tencent-cloud.cn/raw/b28690185058f58e03eb44e6dd84161c.png" style="zoom:80%;" />

## 동기화 작업 생성
1. 타깃 데이터베이스 인스턴스의 Tencent Cloud 계정으로 [DTS 콘솔](https://console.cloud.tencent.com/dts/overview)에 로그인합니다.
2. **데이터 동기화** > **동기화 작업 생성**을 선택하고 동기화 작업을 구매합니다.
3. 구매 후 데이터 동기화 목록으로 돌아가 **작업** 열에서 **구성**을 클릭하여 동기화 작업 구성 페이지로 이동합니다.
4. 원본 및 타깃 데이터베이스 설정 페이지에서 원본 및 타깃 데이터베이스 정보를 구성합니다. 다음은 두 TencentDB for MySQL 인스턴스 간의 데이터 동기화를 예로 들어 설명합니다.
![](https://qcloudimg.tencent-cloud.cn/raw/28ba920ca242e72be84f81fc4bee665e.png)
교차 계정 데이터 동기화를 위한 주요 매개변수를 다음과 같이 구성합니다.
   - 액세스 유형: **데이터베이스**를 선택하여 원본 데이터베이스가 TencentDB 인스턴스임을 나타냅니다.
   - 교차/내부 계정: **교차 계정**을 선택합니다.
   - 피어 계정 ID: 원본 데이터베이스의 루트 계정 ID를 입력합니다.
   - 피어 계정 역할 이름: [계정 권한 부여](#sqzh)의 6단계에서 생성한 **역할 이름**. 역할에 대한 자세한 내용은 [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) 및 [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148)을 참고하십시오.
   - 외부 역할 ID: 이 매개변수는 선택 사항이며 해당 값은 이전 섹션에서 가져올 수 있습니다. 역할에 대한 자세한 내용은 [Role Overview](https://intl.cloud.tencent.com/document/product/598/19420) 및 [Cross-account Access Role](https://intl.cloud.tencent.com/document/product/1150/47148)을 참고하십시오.
>?상기 구성을 완료한 후 **리전**을 선택하여 원본 데이터베이스 계정의 인스턴스 목록을 가져옵니다. 인스턴스를 가져오는 동안 오류가 발생하면 구성이 올바르지 않거나 권한 부여가 수행되지 않았을 수 있습니다. 자세한 내용은 [FAQ](#cjwt)를 참고하십시오.
5. 동기화 옵션 및 객체 설정 페이지에서 데이터 초기화 옵션, 데이터 동기화 옵션 및 객체 동기화 옵션을 설정하고 **저장 후 다음으로 이동**을 클릭합니다.
6. 확인 작업 페이지에서 확인을 완료하고 모든 점검 항목이 통과되면 **작업 실행**을 클릭합니다.
확인이 실패한 경우 [검증 불통과 처리 방법](https://intl.cloud.tencent.com/document/product/571/42551)의 설명 대로 문제를 수정하고 확인 작업을 다시 시작합니다.
7. 데이터 동기화 작업 리스트로 돌아가면 작업이 **실행 중** 상태가 됩니다.
>?**작업** 열에서 **더 보기** > **중지**를 클릭하여 동기화 작업을 중지할 수 있습니다. 작업을 중지하기 전에 데이터 동기화가 완료되었는지 확인해야 합니다.

## [FAQ](id:cjwt)

#### 1. 여러 계정에서 인스턴스 목록을 가져올 때 role not exist[InternalError.GetRoleError] 오류가 보고되면 어떻게 해야 합니까?
**피어 계정 ID**(원본 데이터베이스의 루트 계정 ID)와 **피어 계정 역할 이름**([계정 권한 부여](#sqzh)의 6단계에서 생성된 **역할 이름**)이 올바른지 확인하십시오. 만약 아직 풀링이 안된다면 원본 데이터베이스에 권한을 부여할 수 있는 서비스 권한이 없을 수 있습니다([계정 권한 부여](#sqzh)의 5단계 참고).

#### 2. 인스턴스 목록에 대한 CDB 가져오기 실패: InternalError:InternalInnerCommonError

#### 권한 부여 원본 데이터베이스가 해당 역할에 속한 Tencent Cloud 서비스 정책이 없습니다. 권한 부여는 [계정 권한 부여](#sqzh)의 5단계를 참고하십시오.

#### 3. 여러 계정에서 인스턴스 목록을 가져올 때 you are not authorized to perform operation (sts:AssumeRole) ，resource (qcs::cam::uin/1xx5:roleName/xxxx) has no permission 오류가 보고되면 어떻게 해야 합니까?

 **오류 원인**: 동기화 작업을 생성하는 데 사용하는 계정은 sts:AssumeRole 권한이 없는 서브 계정입니다.

**솔루션**:

- 루트 계정을 사용하여 동기화 작업을 만듭니다.
- 타깃 데이터베이스의 루트 계정에 [계정 권한 부여](#sqzh) 지침에 따라 서브 계정에 권한을 부여하도록 요청하고 정책 구문의 resource를 오류 메시지의 파란색 필드로 설정합니다.



