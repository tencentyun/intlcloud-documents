
## MySQL/TDSQL-C 확인 사항
- 확인 요건: 뷰 구조를 내보낼 때 DTS는 원본 데이터베이스의 ‘DEFINER’([DEFINER = user1])에 해당하는 user1이 마이그레이션 대상 user2와의 동일 여부를 확인합니다.
   - 동일한 경우 마이그레이션 후 설정을 수정하지 마십시오.
   - 서로 다른 경우 ‘DEFINER’에서 ‘INVOKER’로 마이그레이션([INVOKER = user1])한 후 대상 데이터베이스에서 user1의 ‘SQL SECURITY’ 속성을 변경하고, 대상 데이터베이스에서 ‘DEFINER’를 마이그레이션 대상의 user2([DEFINER = 마이그레이션 대상 user2])로 설정합니다.

- 확인 설명: ‘SQL SECURITY’ 매개변수는 사용자가 지정 뷰에 액세스할 때 시스템이 누구의 권한에 따라 수행할지를 나타냅니다. 
  - ‘DEFINER’: 정의자만 명령을 실행할 수 있습니다.
  - ‘INVOKER’: 호출 권한이 있는 호출자만 명령을 실행할 수 있습니다.
기본적으로 ‘DEFINER’는 시스템에 의해 지정됩니다.

## TDSQL for MySQL 확인 사항
마이그레이션 대상의 user@host와 동일한 definer만 허용됩니다. 즉, 뷰 구조를 내보낼 때 DTS는 원본 데이터베이스의 definer에 해당하는 user1([DEFINER = user1])이 마이그레이션 대상의 user@host에 있는 user2(user@host)와 동일한지 확인하고, 동일한 경우 뷰를 마이그레이션할 수 있습니다. 그렇지 않으면 할 수 없습니다.

마이그레이션 대상의 user@host와 다른 definer의 경우 마이그레이션을 하려면 원본 데이터베이스 뷰에서 definer를 마이그레이션 대상의 사용자로 수정하거나 마이그레이션/동기화 작업 시 선택하지 않고 작업이 완료된 후 뷰를 수동으로 동기화합니다.

