## 집계 함수

COS Select는 다음 집계 함수를 지원합니다.

| 함수 이름          | 매개변수 유형                    | 반환 유형                                                     |
| :-------------- | :-------------------------- | :----------------------------------------------------------- |
| AVG(expression) | INT,FLOAT,DECIMAL         | 입력 매개변수가 정수 형식일 경우 DECIMAL을 반환하며 부동 소수점 형식일 경우 FLOAT를 반환합니다. 그 외의 상황에서는 반환 값과 입력 매개변수가 일치합니다. |
| COUNT           | -                           | INT                                                          |
| MAX(expression) | INT,DECIMAL                | 반환 값은 입력 매개변수와 일치합니다.                                             |
| MIN(expression) | INT, DECIMAL                | 반환 값은 입력 매개변수와 일치합니다.                                             |
| SUM(expression) | INT, FLOAT, DOUBLE, DECIMAL | 입력 매개변수가 정수 형식일 경우 INT를 반환하며 부동 소수점 형식일 경우 FLOAT를 반환합니다. 그 외의 상황에서는 반환 값과 입력 매개변수가 일치합니다. |

## 조건부 함수

COS Select는 다음 조건부 함수를 지원합니다.

### COALESCE

COALESCE 함수는 순서대로 입력 매개변수를 결정하며 null이 아닌 최초의 매개변수 값을 반환합니다. 입력한 매개변수에 null이 아닌 매개변수가 포함되지 않는 경우 함수는 null 값을 반환합니다.

#### 구문

```sql
COALESCE ( expression, expression, ... )
```

> ?expression 매개변수는 INT、String、Float 유형의 값, 배열, 중첩 배열 입력을 지원합니다.

#### 예시

```shell
COALESCE(1)                -- 1
COALESCE(1, null)          -- 1
COALESCE(null, null, 1)    -- 1
COALESCE(missing, 1)       -- 1
COALESCE(null, 'string')   -- 'string'
COALESCE(null)             -- null
COALESCE(null, null)       -- null
COALESCE(missing)          -- null
COALESCE(missing, missing) -- null
```

### NULLIF

NULLIF 함수는 두 개의 입력 매개변수 간의 차이를 판단하는데 두 개의 입력 매개변수 값이 같으면 NULL을 반환하고 그렇지 않으면 첫번째 입력 매개변수 값을 반환합니다.

#### 구문

```sql
NULLIF ( expression1, expression2 )
```

> ? expression 매개변수는 INT、String、Float 유형의 값, 배열, 중첩 배열 입력을 지원합니다.

#### 예시

```shell
NULLIF(1, 2)             -- 1
NULLIF(1, '1')           -- 1
NULLIF(1, NULL)          -- 1
NULLIF(1, 1)             -- null
NULLIF(1.0, 1)           -- null
NULLIF(missing, null)    -- null
NULLIF(missing, missing) -- null
NULLIF([1], [1])         -- null
NULLIF(NULL, 1)          -- null
NULLIF(null, null)       -- null
```

## 변환 함수

COS Select는 다음 변환 함수를 지원합니다.

### CAST

CAST 함수로 하나의 인스턴스를 다른 인스턴스로 변환할 수 있습니다. 인스턴스는 값일 수도 있고 어떤 확정 값을 계산할 수 있는 함수일 수도 있습니다.

#### 구문

```shell
CAST ( expression AS data_type )
```

> ?
>
> - expression 매개변수는 값, 배열, 오퍼레이터 혹은 어떤 확정 값을 계산할 수 있는 SQL 함수일 수 있습니다.
> - data type 매개변수는 변환 후의 데이터 유형이며 INT 유형을 예시로 들 수 있습니다. 현재 COS Select에서 지원하는 데이터 유형은 [데이터 유형](https://intl.cloud.tencent.com/document/product/436/32476)을 참고하십시오.

#### 예시

```shell
CAST('2007-04-05T14:30Z' AS TIMESTAMP)
CAST(0.456 AS FLOAT)
```

## 날짜 함수

COS Select는 다음 날짜 함수를 지원합니다.

### DATE_ADD

DATE_ADD 함수는 지정 타임스탬프(년, 월, 일, 시, 분, 초)에서 지정 시간만큼 더할 수 있으며 새로운 타임스탬프를 반환합니다.

#### 구문

```shell
DATE_ADD( date_part, quantity, timestamp )
```

> ?
> - date_part 매개변수는 지정 타임스탬프에서 수정할 부분입니다. 년, 월, 일, 시, 분, 초가 될 수 있습니다.
> - quantity 매개변수는 추가할 값을 나타내며 반드시 자연수여야 합니다.
> - timestamp 매개변수는 수정할 타임스탬프입니다.

#### 예시

```shell
DATE_ADD(year, 5, `2010-01-01T`)                -- 2015-01-01
DATE_ADD(month, 1, `2010T`)                     -- 2010-02T 
DATE_ADD(month, 13, `2010T`)                    -- 2011-02T
DATE_ADD(hour, 1, `2017T`)                      -- 2017-01-01T01:00-00:00
DATE_ADD(hour, 1, `2017-01-02T03:04Z`)          -- 2017-01-02T04:04Z
DATE_ADD(minute, 1, `2017-01-02T03:04:05.006Z`) -- 2017-01-02T03:05:05.006Z
DATE_ADD(second, 1, `2017-01-02T03:04:05.006Z`) -- 2017-01-02T03:04:06.006Z
```

### DATE_DIFF

DATE_DIFF 함수는 두 타임스탬프를 비교하고 두 타임스탬프의 차이 값을 반환합니다. 차이 값은 지정한 시간 단위를 보여줍니다. timestamp1의 date_part 값이 timestamp2보다 큰 경우 반환 값은 정수입니다. 그 반대의 경우는 음수를 반환합니다.

#### 구문

```shell
DATE_DIFF( date_part, timestamp1, timestamp2 )
```

> ?
> - date_part 매개변수는 두 타임스탬프를 비교한 시간 단위를 지정합니다. 년, 월, 일, 시, 분, 초일 수 있습니다.
> - timestamp1 매개변수는 입력한 첫번째 타임스탬프입니다.
> - timestamp2 매개변수는 입력한 두번째 타임스탬프입니다.

#### 예시

```shell
DATE_DIFF(year, `2010-01-01T`, `2011-01-01T`)            -- 1
DATE_DIFF(year, `2010T`, `2010-05T`)                     -- 4 
DATE_DIFF(month, `2010T`, `2011T`)                       -- 12
DATE_DIFF(month, `2011T`, `2010T`)                       -- -12
DATE_DIFF(day, `2010-01-01T23:00T`, `2010-01-02T01:00T`) -- 0 
```

### EXTRACT

 EXTRACT 함수는 지정된 타임스탬프에서 추출한 지정 시간 단위 값입니다.

#### 구문

```shell
EXTRACT( date_part FROM timestamp )
```

> ?
> - date_part 매개변수는 추출할 시간 단위를 지정합니다. 년, 월, 일 시, 분, 초일 수 있습니다.
> - timestamp 매개변수는 입력한 타임스탬프입니다.

#### 예시

```shell
EXTRACT(YEAR FROM `2010-01-01T`)                           -- 2010
EXTRACT(MONTH FROM `2010T`)                                -- 1 
EXTRACT(MONTH FROM `2010-10T`)                             -- 10
EXTRACT(HOUR FROM `2017-01-02T03:04:05+07:08`)             -- 3
EXTRACT(MINUTE FROM `2017-01-02T03:04:05+07:08`)           -- 4
EXTRACT(TIMEZONE_HOUR FROM `2017-01-02T03:04:05+07:08`)    -- 7
EXTRACT(TIMEZONE_MINUTE FROM `2017-01-02T03:04:05+07:08`)  -- 8
```

### TO_STRING

TO_STRING 함수로 타임스탬프를 지정 포맷 시간 문자열로 변환할 수 있습니다.

#### 구문

```shell
TO_STRING ( timestamp time_format_pattern )
```

> ?
> - timestamp 매개변수는 변환할 타임스탬프를 지정합니다.
> - time_format_pattern 매개변수는 변환 시간 포맷을 지정합니다.

| 포맷             | 설명                                                         | 예시                              |
| ---------------- | ------------------------------------------------------------ | --------------------------------- |
| yy             | 연도 단위 2자리 수                                                    | 98                              |
| y             | 연도 단위 4자리 수                                                    | 1998                              |
| yyyy           | 연도 단위 고정 4자리 수, 부족한 부분은 0으로 보충                                 | 0199                            |
| M              | 월 단위                                                         | 1                              |
| MM             | 월 단위 고정 2자리 수, 부족한 부분은 0으로 보충                                 | 01                              |
| MMM            | 월 단위 영어 약어                                               | Jan                             |
| MMMM           | 월 단위 영어 전체 표기                                               | January                         |
| MMMMM          | 월 단위의 첫 글자 약어                                             | J(to_timestamp 함수에는 적합하지 않음) |
| d             | 한 달 중에 하루(1~31)                                       | 1                              |
| dd             | 일 수 중 고정 2자리 수(1~31)                                      | 01                              |
| a             | 오전 혹은 오후 표기(AM/PM)                                  | AM                              |
| h              | 시간, 12시간제                                               | 1                             |
| hh             | 시각 고정 2자리 수이며 12시간제                                    | 01                              |
| H              | 시간, 24시간제                                               | 1                             |
| HH             | 시각 고정 2자리 수이며 24시간제                                    | 01                              |
| m              | 분(00-59)                                               | 1                               |
| mm            | 시간 고정 2자리 수이며 24시간제                                    | 01                              |
| s              | 분(00-59)                                                  | 1                               |
| ss            | 시각 고정 2자리 수이며 24시간제                                    | 01                              |
| S              | 초의 소수 부분(정확도 0.1, 범위 0.0 - 0.9)                         | 0                              |
| SS              | 초의 소수 부분(정확도 0.01, 범위 0.00 - 0.99)                         | 6                              |
| SSS            | 초의 소수 부분(정확도 0.001, 범위 0.000 - 0.999)                   | 60                              |
| ...              | ...                                                          | ...                               |
| SSSSSSSSS     | 초의 소수 부분(정확도 0.000000001, 범위 ０.000000000 - 0.999999999) | 60000000                        |
| n             | 나노 초                                                         | 60000000                        |
| X              | 시간 단위 오프셋, 오프셋이 0이면 "Z"로 표시                             | +01 혹은 Z                      |
| XX 혹은 XXXX              | 시간 혹은 분 단위 오프셋, 오프셋이 0이면 "Z"로 표시                             | +0100 혹은 Z                      |
| xxx 혹은 xxxxx              | 시간 혹은 분 단위 오프셋, 오프셋이 0이면 "Z"로 표시                             | +01:00 혹은 Z                      |
| x              | 시간 단위 오프셋                                                 | 1                               |
| xx 혹은 xxxx   | 시간 혹은 분 단위 오프셋                                         | 0100                            |
| xxx 혹은 xxxxx   | 시간 혹은 분 단위 오프셋                                         | 01:00                            |

#### 예시

```shell
TO_STRING(`1998-07-20T20:18Z`,  'MMMM d, y')                    -- "July 20, 1998"
TO_STRING(`1998-07-20T20:18Z`, 'MMM d, yyyy')                   -- "Jul 20, 1998"
TO_STRING(`1998-07-20T20:18Z`, 'M-d-yy')                        -- "7-20-69"
TO_STRING(`1998-07-20T20:18Z`, 'MM-d-y')                        -- "07-20-1998"
TO_STRING(`1998-07-20T20:18Z`, 'MMMM d, y h:m a')               -- "July 20, 1998 8:18 PM"
TO_STRING(`1998-07-20T20:18Z`, 'y-MM-dd''T''H:m:ssX')           -- "1998-07-20T20:18:00Z"
TO_STRING(`1998-07-20T20:18+08:00Z`, 'y-MM-dd''T''H:m:ssX')     -- "1998-07-20T20:18:00Z"
TO_STRING(`1998-07-20T20:18+08:00`, 'y-MM-dd''T''H:m:ssXXXX')   -- "1998-07-20T20:18:00+0800"
TO_STRING(`1998-07-20T20:18+08:00`, 'y-MM-dd''T''H:m:ssXXXXX')  -- "1998-07-20T20:18:00+08:00"
```

### TO_TIMESTAMP

 TO_TIMESTAMP 함수로 시간 문자열을 타임스탬프로 변환할 수 있습니다.

#### 구문

```shell
TO_TIMESTAMP ( string )
```

> ?  string 매개변수는 입력한 시간 문자열입니다.

#### 예시

```shell
TO_TIMESTAMP('2007T')                         -- `2007T`
TO_TIMESTAMP('2007-02-23T12:14:33.079-08:00') -- `2007-02-23T12:14:33.079-08:00`
```

### UTCNOW

 UTCNOW로 UTC 타임스탬프를 반환할 수 있습니다.

#### 구문

```
UTCNOW()
```

#### 예시

```shell
UTCNOW() -- 2019-01-01T14:23:12.123Z
```

## 문자열 함수

COS Select는 다음 문자열 함수를 지원합니다.

### CHAR_LENGTH, CHARACTER_LENGTH

CHAR_LENGTH과 CHARACTER_LENGTH는 문자열의 문자 수를 계산해줍니다. 두 함수의 semantics는 같습니다.

#### 구문

```shell
CHAR_LENGTH ( string )
```

> ?  string 매개변수는 계산할 문자의 문자열을 지정합니다.

#### 예시

```shell
CHAR_LENGTH('null')      -- 4
CHAR_LENGTH('tencent')   -- 7
```

### LOWER

 LOWER 함수는 문자열의 모든 대문자를 소문자로 변환할 수 있으며 대문자가 아닌 문자열은 수정할 수 없습니다.

#### 구문

```shell
LOWER ( string )
```

> ?  string 매개변수는 대문자를 소문자로 변환해야 하는 문자열을 지정합니다.

#### 예시

```shell
LOWER('TENcent') -- 'tencent'
```

### SUBSTRING

 SUBSTRING 함수는 문자열의 부속 문자열을 반환합니다. 하나의 인덱스를 지정하고 SUBSTRING 함수를 사용해 인덱스부터 부속 문자열 길이에 따라 기존 문자열의 나머지를 추출하여 결과를 반환합니다.

>? 입력 문자열이 1개의 문자로 이루어졌고 인덱스 설정이 1보다 크면 SUBSTRING 함수가 그 문자열을 자동으로 1로 치환합니다.
>

#### 구문

```shell
SUBSTRING( string FROM start [ FOR length ] )
```

> ?
> - string 매개변수는 추출할 문자의 문자열을 지정합니다.
> - start 매개변수는 문자열의 어떤 인덱스값이며 추출 위치를 지정합니다.
> - length 매개변수는 문자 길이를 지정하며 문자 길이를 따로 지정하지 않은 경우 문자열의 나머지 부분이 추출됩니다.

#### 예시

```shell
SUBSTRING("123456789", 0)      -- "123456789"
SUBSTRING("123456789", 1)      -- "123456789"
SUBSTRING("123456789", 2)      -- "23456789"
SUBSTRING("123456789", -4)     -- "123456789"
SUBSTRING("123456789", 0, 999) -- "123456789" 
SUBSTRING("123456789", 1, 5)   -- "12345"
```

### TRIM

 TRIM 함수는 지정 문자열의 첫 글자 앞 혹은 끝 글자 뒤의 모든 문자 부호를 삭제할 수 있습니다. 기본적으로 삭제하는 문자 부호는 " "입니다.

#### 구문

```shell
TRIM ( [[LEADING | TRAILING | BOTH remove_chars] FROM] string )
```

> ?
> -  string 매개변수는 작업에 필요한 문자열을 지정합니다.
> - `LEADING | TRAILING | BOTH` 매개변수는 삭제할 문자열 앞(LEADING) 혹은 문자열 뒤(TRAILING) 혹은 두 곳 모두 삭제(BOTH)할 부분의 나머지 문자를 지정합니다.
> -  remove_chars 매개변수는 삭제할 나머지 문자열을 지정합니다. remove_chars 매개변수는 1개의 문자보다 길 수 있으며 TRIM 함수는 string 매개변수 앞뒤에서 나머지 문자열을 식별하여 삭제 처리합니다.

#### 예시

```shell
TRIM('       foobar         ')               -- 'foobar'
TRIM('      ＼tfoobar＼t         ')            -- '＼tfoobar＼t'
TRIM(LEADING FROM '       foobar         ')  -- 'foobar'
TRIM(TRAILING FROM '       foobar         ') -- 'foobar'
TRIM(BOTH FROM '       foobar         ')     -- 'foobar'
TRIM(BOTH '12' FROM '1112211foobar22211122') -- 'foobar'
```

### UPPER

 UPPER 함수는 문자열의 모든 소문자를 대문자로 변환할 수 있으며 소문자가 아닌 문자열은 수정할 수 없습니다.

#### 구문

```shell
UPPER ( string )
```

> ? string 매개변수는 변환할 대문자 문자열을 지정합니다.

#### 예시

```shell
UPPER('tenCENT') -- 'TENCENT'
```

