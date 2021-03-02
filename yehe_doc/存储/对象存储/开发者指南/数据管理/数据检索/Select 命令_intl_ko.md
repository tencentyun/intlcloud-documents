## 개요

COS Select 기능은 필요한 일부 데이터를 쉽게 인덱스할 수 있도록 SELECT SQL쿼리 명령을 지원하여 비용을 감소시키고 요청 딜레이를 줄일 수 있습니다. 다음은 SELECT 조회에서 지원하는 표준 절입니다.

- SELECT 명령
- WHERE 절
- LIMIT 절

> !현재 COS Select는 절 쿼리 혹은 joins를 지원하지 않습니다.

## SELECT 명령

SELECT 명령으로 COS 객체에서 보고 싶은 데이터를 인덱스할 수 있습니다. 이름, 함수, 표현식 등으로 데이터 조회가 가능하며 리스트의 형식으로 조회 결과를 반환합니다. SELECT 명령 포맷은 다음과 같습니다.

```shell
SELECT *
SELECT projection [ AS column_alias | column_alias ] [, ...]
```

첫번째 절의 SELECT 명령은 `*`(별표)가 표시되며 COS 객체에서 모든 열을 반환합니다. 두번째 절의 SELECT 명령은 사용자 지정을 사용하여 스칼라 표현식을 출력하고 **projection**은 모든 열에 사용자 지정 이름의 출력 리스트를 생성합니다.


## WHERE 절

WHERE 절은 다음 구문을 사용합니다.

```shell
WHERE condition
```

WHERE 절은 **condition**을 통해 필터링을 진행합니다. **condition**은 Boolean 결과를 반환할 수 있는 표현식입니다. 반환 값이 TRUE인 행이어야 결과를 출력할 수 있습니다.

## LIMIT 절

LIMIT 절은 다음 구문을 사용합니다.

```shell
LIMIT number
```

LIMIT 절은 조회 당 반환 되는 기록 수를 제한합니다. **number** 매개변수를 이용해 이 제한을 지정할 수 있습니다.

## 액세스 속성

SELECT와 WHERE 절은 파일 포맷이 CSV인지 JSON인지에 따라 다음 방식으로 조회할 필드를 선택할 수 있습니다.

#### CSV

- **열 번호**: 제 N열의 조회할 데이터는 `_N`을 통해 지정할 수 있습니다. 어느 CSV 파일이든 열 번호는 1부터 증가합니다. 첫 열의 일련 번호가 `_1`인 경우 두번째 열의 일련 번호는 `_2`입니다. SELECT와 WHERE 절에서 `_N`이나 `alias._N`을 통해 조회할 열을 지정하는 것은 유효합니다.
- **열 헤더**: 조회할 CSV 파일에 헤더가 있다면 SELECT나 WHERE 절에서 이 헤더를 통해 조회가 필요한 열을 지정할 수 있습니다. SQL 명령에서는 SELECT나 WHERE 절의`alias.column_name` 혹은 `column_name`으로 지정합니다.

#### JSON 

- **문서(Document)**: `alias.name`방식을 사용하여 JSON 문서에 액세스할 수 있습니다. 중첩된 배열은 `alias.name1.name2.name3`과 같은 방식으로 액세스할 수 있습니다.
- **리스트(List)**: 0부터 일련번호가 매겨지고 `[]` 오퍼레이터를 사용하는 인덱스 기능으로 리스트 요소에 액세스할 수 있습니다. 예시로 `alias[1]`를 통해 JSON 리스트의 2번째 요소에 액세스할 수 있습니다. 중첩 배열에 액세스 해야 하는 경우 `alias.name1.name2[1].name3`과 같은 방식으로 액세스할 수 있습니다.

**예시** 
다음은 예시 데이터 샘플입니다.

```shell
{
	"name": "Leon",
	"org": "Tencent",
	"projects":
		[
		 {"project_name":"project1", "completed":true},
		 {"project_name":"project2", "completed":false}
		]
}
```

- 예시1: 다음은 데이터 예시 중 이름을 조회하는 SQL 명령 및 조회 결과입니다.
  ```shell
  Select s.name from COSObject s
  ```
  ```shell
  {"name":"Leon"}
  ```
- 예시2: 다음은 데이터 예시 중 프로젝트 이름을 조회하는 SQL 명령 및 조회 결과입니다.
  ```shell
  Select s.projects[0].project_name from COSObject s
  ```
  ```shell
  {"project_name":"project1"}
  ```

## 헤더와 속성 이름의 대소문자 민감성

큰따옴표를 사용하여 CSV 파일의 헤더와 JSON 파일의 속성 이름을 표시하여 대소문자를 구분하는지 알 수 있습니다. 큰따옴표를 추가하지 않으면 헤더/속성 이름은 대소문자를 구분하지 않으며 명확하게 설정이 되어 있지 않은 경우 COS Select가 이상 경고를 보냅니다.

- 예시 1: 헤더/속성 이름에서 "NAME"이 있는 객체를 조회합니다.
  다음 SQL 예시는 큰따옴표를 사용하지 않았으므로 대소문자를 구분하지 않습니다. 이 헤더가 테이블에 포함되기 때문에 값이 반환될 수 있습니다.
  ```shell
  SELECT s.name from COSObject s
  ```

  다음 SQL 예시는 큰따옴표를 사용하여 대소문자를 구분합니다. 테이블에서 이 헤더를 포함하지 않아 400 오류인 `SQLParsingError`이 반환됩니다.
  ```shell
  SELECT s."name" from COSObject s
  ```

- 예시2: 헤더/속성 이름을 조회할 때 "NAME"과 "name"객체가 있습니다.
  다음 SQL 예시는 큰따옴표를 사용하지 않아 대소문자를 구분하지 않습니다. 테이블에 "NAME"과 "name" 두 개의 헤더를 함께 포함하여 조회 명령 설정이 명확하지 않으므로 AmbiguousFieldName 이상 경고가 반환될 수 있습니다.
  ```shell
  SELECT s.name from COSObject s
  ```

  다음 SQL 예시는 큰따옴표를 사용하여 대소문자를 구분합니다. 테이블에 "NAME" 헤더가 포함되기 때문에 조회 결과가 반환될 수 있습니다.
  ```shell
  SELECT s."NAME" from COSObject s
  ```

## 예약된 필드를 사용자 지정 필드로 사용하기

COS Select의 SQL 표현식에는 함수 이름, 데이터 유형, 오퍼레이터 등의 예약된 필드가 있습니다. 사용자는 예약된 필드를 CSV 파일 열 헤더 혹은 JSON 파일의 속성 이름으로 사용할 수 있는데 이때 예약된 필드와 충돌할 가능성이 있습니다. 이런 경우 큰따옴표를 사용하여 사용자 지정 필드가 사용 중임을 나타냅니다. 그렇지 않은 경우 COS가 `400 parse error` 오류를 반환할 수 있습니다.

완전한 예약된 필드 리스트를 조회해야 할 경우 [예약된 필드](https://intl.cloud.tencent.com/document/product/436/32475)를 참조하십시오.

- 예시: 조회할 객체의 헤더/속성 이름에는 예약된 필드 "CAST"가 포함되어 있습니다.
  다음 SQL 예시는 큰따옴표를 사용하여 CAST가 사용자 지정 필드임을 나타내므로 조회 결과가 성공적으로 반환될 수 있습니다.
  ```shell
  SELECT s."CAST" from COSObject s
  ```
  아래 SQL 예시는 CAST가 사용자 지정 필드임을 나타내기 위해 큰따옴표를 쓰지 않았으므로 COS는 예약된 필드로 처리를 하고 `400 parse error`로 반환합니다.
  ```shell
  SELECT s.CAST from COSObject s
  ```

## 스칼라 표현식

SELECT 명령과 WHERE 절에서 SQL 스칼라 표현식(스칼라 표현식 반환)을 사용할 수 있습니다. 현재 COS Select는 다음과 같은 형식을 지원합니다.

- **literal**: SQL 텍스트.
- **column_reference**: column_name이나 alias.column_name.
- **unary_op** **expression**: SQL 단항 오퍼레이터.
- **expression** **binary_op** **expression**: SQL 이항 오퍼레이터.
- **func_name**: 호출된 스칼라 함수 이름.
- **expression** [ NOT ] BETWEEN **expression** AND **expression**
- **expression** LIKE **expression** [ ESCAPE **expression** ]
