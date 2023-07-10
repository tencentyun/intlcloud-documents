## 기능 개요

객체 태그 기능은 객체에 키 값 쌍을 식별자로 추가하여, 사용자가 버킷에 있는 객체를 그룹화하고 관리하는 데 도움이 되도록 설계되었습니다. 객체 태그는 태그 키(`tagKey`)와 태그 값(`tagValue`), 그리고 `=`로 연결되어 구성됩니다(예: `group=IT`). 사용자는 지정 객체의 태그 설정, 조회, 삭제 작업을 할 수 있습니다.

>! 객체 태그 기능은 과금 항목이며, 자세한 가격은 [제품 가격](https://intl.cloud.tencent.com/pricing/cos) 문서를 참조하십시오.
>

## 사용 방법

### COS 콘솔 사용

Cloud Object Storage(COS) 콘솔로 객체 태그를 관리할 경우 자세한 정보는 [객체 태그 설정](https://intl.cloud.tencent.com/document/product/436/35664)을 참고하십시오.

### REST API 사용

다음 API를 통해 객체 태그를 관리할 수 있습니다.

- [PUT Object tagging](https://intl.cloud.tencent.com/document/product/436/35709)
- [GET Object  tagging](https://intl.cloud.tencent.com/document/product/436/35710)
- [DELETE Object tagging](https://intl.cloud.tencent.com/document/product/436/35711)

## 규격 및 제한

### 태그 키 제한


- UTF-8 포맷은 문자 부호, 빈칸, 숫자[0-9], 특수 문자 `+ - = ._ : / @ `로 나타낼 수 있습니다.
- 태그 키 길이는 문자 부호 1-127개까지 가능합니다.(UTF-8 포맷 적용)
- 태그 키는 영어 대소문자를 구별합니다.

### 태그 값 제한

- UTF-8 포맷은 문자 부호, 빈칸, 숫자[0-9], 특수 문자 `+ - = ._ : / @ `로 나타낼 수 있습니다.
- 태그 값 길이는 문자 부호 1-255개까지 허용합니다.(UTF-8 포맷 적용)
- 태그 값은 영어 대소문자를 구분합니다.

### 태그 수 제한

- 객체의 경우: 객체 하나당 상이한 객체 태그 최대 10개까지 가능합니다.
- 태그의 경우: 제한이 없습니다.

