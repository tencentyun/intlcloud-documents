ls 명령은 버킷, 버킷의 객체 및 디렉터리의 객체 목록을 쿼리하는 데 사용됩니다.

## 명령어 형식

```plaintext
./coscli ls [cos://bucketAlias[/prefix/]]
```

>? 
>- bucketAlias에 대한 자세한 내용은 [다운로드 및 설치 설정](https://intl.cloud.tencent.com/document/product/436/43265)을 참고하십시오.
>- 이 명령의 다른 일반 옵션(예시: 버킷 및 사용자 계정 전환)은 [범용 옵션](https://intl.cloud.tencent.com/document/product/436/46273)을 참고하십시오.
>

ls 명령어에는 다음과 같은 매개변수 옵션이 포함됩니다.

| 매개변수 형식          | 매개변수 용도       | 예시                 |
| ----------------- | -------------- | -------------------- |
| cos://bucketAlias | 버킷 지정     | cos://bucket1          |
| /prefix/          | 폴더 지정 | /picture/ |




## 작업 예시


### 현재 계정의 모든 버킷 나열

```plaintext
./coscli ls
```

### 파일 나열

#### bucket1의 모든 파일 나열

```plaintext
./coscli ls cos://bucket1
```

#### bucket1의 picture 폴더에 있는 모든 파일 및 폴더 나열

```plaintext
./coscli ls cos://bucket1/picture/
```


