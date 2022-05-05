bucket-tagging 명령은 버킷 태그 생성(수정), 가져오기 및 삭제에 사용됩니다.

## 명령 옵션
bucket-tagging 명령에는 다음과 같은 flag 옵션이 포함됩니다.

|flag 약칭|flag 전체 명칭| flag 용도|
|----|----|----|
|-m|--method|put, get 및 delete 등 수행할 작업 지정   |

>? 이 명령의 다른 일반 옵션(예시: 버킷 및 사용자 계정 전환)은 [Common Options](https://intl.cloud.tencent.com/document/product/436/46273)를 참고하십시오.
>

## 버킷 태그 추가 또는 수정

버킷 태그는 Key-Value 쌍으로 표시됩니다. 버킷 소유자와 PutBucketTagging 권한이 있는 사용자만 버킷 태그를 추가하거나 수정할 수 있습니다. 다른 사용자에게는 오류 코드 403 AccessDenied가 반환됩니다.

### 명령어 형식

```plaintext
./coscli bucket-tagging --method put cos://<BucketName-APPID> key1#value1 key2#value2
```
여기서 `key#value`는 `#`으로 구분된 태그 Key-Value 쌍을 나타냅니다. 버킷에 태그가 없는 경우 이 명령은 지정된 태그를 버킷에 추가합니다. 그렇지 않으면 기존 태그를 덮어씁니다.

### 작업 예시

1과 2의 key와 각각 111과 222의 value를 사용하여 버킷 exmapplebucket-1250000000에 대해 두 개의 태그를 구성하려면 다음 명령을 실행합니다.

```plaintext
./coscli bucket-tagging --method put cos://exmaplebucket-1250000000 1#111 2#222
```

## 버킷 태그 조회
### 명령어 형식

```plaintext
./coscli bucket-tagging --method get cos://<BucketName-APPID>
```

### 작업 예시

```plaintext
./coscli bucket-tagging --method get cos://exmaplebucket-1250000000
```

다음 출력 결과는 exmapplebucket-1250000000에 1과 2의 key와 각각 111과 222의 value를 가진 두 개의 태그가 있음을 보여줍니다.

```plaintext
  KEY | VALUE  
------+--------
    1 |   111  
    2 |   222 
```

## 버킷 태그 삭제

### 명령어 형식
```plaintext
./coscli bucket-tagging --method delete cos://<BucketName-APPID>
```


### 작업 예시

```plaintext
./coscli bucket-tagging --method delete cos://exmaplebucket-1250000000
```
