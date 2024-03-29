## 확인 사항
- 확인 요건: 원본 및 대상 데이터베이스의 다음 매개변수 값을 확인합니다. 원본 데이터베이스와 대상 데이터베이스에서 매개변수 값이 다른 경우 확인 알람이 표시되며 마이그레이션 작업을 차단하지는 않지만 비즈니스에 영향을 미칩니다. 매개변수 수정 여부를 평가 및 결정해야 합니다.
TimeZone, lc_monetary, lc_numeric, array_nulls, server_encoding, DateStyle, extra_float_digits , gin_fuzzy_search_limit, xmlbinary, constraint_exclusion。

- 비즈니스에 미치는 영향: 매개변수 값이 다를 경우 원본 데이터베이스와 대상 데이터베이스 간의 데이터 불일치가 발생할 수 있습니다. 구체적인 영향은 다음과 같습니다.
  - TimeZone: 인스턴스 시간대를 설정합니다. 이 매개변수의 값이 다른 경우 마이그레이션 후 데이터가 올바르지 않을 수 있습니다.
  - lc_monetary: 인스턴스 통화 모드를 설정합니다. 이 매개변수의 값이 다른 경우 마이그레이션 후 통화 숫자가 올바르지 않을 수 있습니다.
  - lc_numeric: 인스턴스 숫자 모드를 설정합니다. 이 매개변수의 값이 다른 경우 마이그레이션 후 데이터가 올바르지 않을 수 있습니다.
  - array_nulls: 배열이 비어 있을 수 있는지 여부를 설정합니다. 이 매개변수의 값이 다를 경우 데이터 불일치가 발생하고 특정 데이터의 마이그레이션이 실패할 수 있습니다.
  - server_encoding: 인스턴스 문자 집합을 설정합니다. 이 매개변수의 값이 다른 경우 저장된 데이터에 잘못된 문자가 나타날 수 있습니다.
  - DateStyle: 날짜 형식을 설정합니다. 이 매개변수의 값이 다른 경우 데이터 마이그레이션이 실패할 수 있습니다.
  - extra_float_digits: 부동 소수점 값 출력 정밀도를 설정합니다. 이 매개변수에 값이 있으면 데이터 정밀도가 영향을 받습니다. 고정밀 데이터베이스 사용 사례에서는 마이그레이션 후 데이터 불일치가 발생합니다.
  - gin_fuzzy_search_limit: GIN 인덱스가 반환하는 집합 크기의 상한선을 설정합니다. 이 매개변수의 값이 다르면 마이그레이션 후 데이터 표시 불일치가 발생합니다.
  - xmlbinary: xml 함수 변환 결과를 설정합니다. 이 매개변수의 값이 다른 경우 대상 데이터베이스의 함수 실행이 원본 데이터베이스의 함수 실행과 다를 수 있습니다.
  - constraint_exclusion: 제한이 적용되는지 여부를 설정합니다. 이 매개변수의 값이 다를 경우 마이그레이션 후 데이터 불일치가 발생할 수 있습니다. 


## 수정 방법
1. superuser 계정으로 원본 데이터베이스에 로그인합니다.
2. 다음 예시 명령을 실행하여 해당 매개변수를 수정합니다.
   - 원본 데이터베이스에서 매개변수를 먼저 수정하도록 선택할 수 있습니다. 이러한 매개변수를 수정할 수 없는 경우 [티켓을 제출](https://console.cloud.tencent.com/workorder/category)하여 대상 데이터베이스에서 수정해야 합니다.
   - server_encoding 매개변수는 원본 데이터베이스에서 수정할 수 없습니다. 예외적인 경우 대상 데이터베이스에 생성되었는지 확인하고 원본 데이터베이스와 다를 경우 새로운 인스턴스를 신청해야 합니다. 그렇지 않은 경우 다음과 같이 수정합니다(현재 TencentDB 인스턴스는 UTF-8 및 LATIN의 두 가지 문자 세트만 지원합니다).
```
alter system set timezone='매개변수 값';
alter system set lc_monetary='매개변수 값';
alter system set lc_numeric='매개변수 값';
```

