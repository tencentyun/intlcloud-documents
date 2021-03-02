## 기능 개요

객체 태그 기능은 객체에 키 값 쌍 형식의 식별자를 추가하여 실현하며 사용자가 버킷의 객체를 분할 관리하는 데 도움을 줍니다. 객체 태그는 태그 키(`tagKey`)와 태그 값(`tagValue`), `=`으로 구성됩니다. 예시로 `group = IT`와 같은 형식입니다. 사용자는 지정 객체에 태그 설정, 조회, 삭제 작업을 할 수 있습니다.

>객체 태그 기능 과금 항목에 대한 상세 가격은 [제품 가격](https://intl.cloud.tencent.com/document/product/436/6239) 문서를 참조하십시오.

## 사용 방법

### COS 콘솔 사용

COS 콘솔로 객체 태그를 관리할 경우 자세한 정보는 [객체 태그 설정](https://intl.cloud.tencent.com/document/product/436/35664)을 참조하십시오.

### REST API 사용

다음 API를 통해 객체 태그를 관리할 수 있습니다.

- [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709)
- [GET Object  tagging](https://intl.cloud.tencent.com/document/product/436/35710)
- [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711)

## 규격 및 제한

### 태그 키 제한

- 태그 키는 `qcs:`, `project`, `항목` 등을 첫머리 글자로 사용할 수 없습니다. 시스템에서 미리 남기는 태그 키이며 사용자가 생성할 수 없습니다.
- UTF-8 포맷은 문자 부호, 빈칸, 숫자[0-9], 특수 문자 `+ - = ._ : / @ `로 나타낼 수 있습니다.
- 태그 키 길이는 문자 부호 1-127개까지 가능합니다.(UTF-8 포맷 적용)
- 태그 키는 영어 대소문자를 구별합니다.

### 태그 값 제한

- UTF-8 포맷은 문자 부호, 빈칸, 숫자[0-9], 특수 문자 `+ - = ._ : / @ `로 나타낼 수 있습니다.
- 태그 값 길이는 문자 부호 1-127개까지 허용합니다.(UTF-8 포맷 적용)
- 태그 값은 영어 대소문자를 구분합니다.

### 태그 수 제한

- 객체의 경우: 객체 하나당 상이한 객체 태그 최대 10개까지 가능합니다.
- 태그의 경우: 제한이 없습니다.

