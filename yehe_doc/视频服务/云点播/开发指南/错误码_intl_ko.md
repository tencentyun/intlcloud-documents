## 오류 코드 리스트
### 비디오 처리 유형 오류 코드

| 오류 코드 | 의미 |
| -- | -- |
| InvalidInput | 유효하지 않은 매개변수. 입력한 매개변수를 확인하십시오. |
| InvalidInput.InvalidTimeOffset | 유효하지 않은 매개변수: 지정한 시간이 유효하지 않습니다. |
| InvalidInput.DefinitionNotExist | 유효하지 않은 매개변수: 지정한 템플릿 ID가 존재하지 않습니다. |
|InvalidInput.ConfigurationUnsupported|잘못된 입력 매개변수입니다: 이유는 다음을 포함하지만 이에 국한되지 않습니다:<li>미등록 사용자.</li><li>잘못된 입력 매개변수 값(형식, 값 범위 등의 오류).</li><li>잘못된 매개변수 템플릿 구성.</li><li>비디오 처리 작업 미지정.</li>|
|InvalidInput.TaskDuplicated|잘못된 입력 매개변수: 중복 작업.|
|InvalidInput.PermissionDenied|잘못된 입력 매개변수: 이 기능을 사용할 권한이 없습니다. 먼저 권한을 신청하십시오.|
|InvalidInput.ResultFileSizeTooLarge|잘못된 입력 매개변수: 여러 파일을 입력한 후 접합된 파일이 너무 큽니다.|
| SourceFileError | 잘못된 소스 파일: 예를 들어 비디오 데이터가 손상되었습니다. 소스 파일이 정상인지 확인하십시오. |
| SourceFileError.NoVideoMedia | 잘못된 소스 파일: 비디오 이미지가 없습니다. |
| SourceFileError.NoVideoResolutio | 잘못된 소스 파일: 소스 파일의 해상도를 얻을 수 없습니다. |
|SourceFileError.ContentMalformed|잘못된 소스 파일: 입력 내용에 오류가 있습니다. 예를 들어 파일이 존재하지 않거나, 파일이 손상되었거나, 미디어 파일을 디코딩할 수 없습니다.|
|SourceFileError.ContentUnsupported|잘못된 소스 파일: 지원되지 않는 파일 형식, 크기, 기간 또는 기타 이유로 인해 입력 파일이 잘못되었습니다.|
|SourceFileError.DownloadNotAccessible|잘못된 소스 파일: 다운로드하는 동안 파일에 액세스할 수 없습니다. 소스 파일의 가용성을 확인하십시오.|
| InternalError | 내부 서비스 오류. 다시 시도하십시오. |
