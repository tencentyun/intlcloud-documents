
2019년 VOD 이벤트 알림 형식이 다음과 같이 수정되었습니다.
- 개정 이후 신규 등록 사용자의 API 형식은 v3.0(현재 형식)입니다.
- 개정 전에 등록된 사용자는 여전히 v2.0(레거시 형식)을 사용하고 있을 수 있습니다.

본문은 v2.0 및 v3.0 API 형식의 콜백을 비교합니다. 이 문서를 읽기 전에 콘솔에 로그인하고 [제품]>[VOD]>[[콜백 구성]](https://console.cloud.tencent.com/vod/callback)을 선택하고 이 페이지에서 다음을 확인하십시오.
- [콜백 URL]만 표시되는 경우 일반 콜백은 기본적으로 이미 v3.0에 있으므로 이 문서를 읽을 필요가 없습니다.
- [v2.0 API 형식 콜백 URL]과 [v3.0 API 형식 콜백 URL]이 모두 표시되면 v2.0 API 형식의 일반 콜백을 사용하고 있음을 의미합니다. **아래 내용을 계속 읽으십시오**.

>! 아직 v2.0 API 형식의 일반 콜백을 사용하고 있다면 v3.0 API 형식의 콜백으로 점진적으로 변경하는 것을 권장하며 v2.0 API 형식의 콜백에 대한 설명서는 더 이상 업데이트되지 않습니다.

**v2.0 및 v3.0 API 형식의 콜백을 비교**하면 다음과 같습니다.

| 이벤트 알림 | 3.0형식 | 2.0형식 |
| -- | -- | -- |
| 비디오 업로드 완료 | [링크](https://intl.cloud.tencent.com/document/product/266/33950) | [링크](#NewFileUpload) |
| URL 풀링 비디오 업로드 완료 | [링크](https://intl.cloud.tencent.com/document/product/266/33951) | [링크](#PullComplete) |
| 비디오 삭제 완료 | [링크](https://intl.cloud.tencent.com/document/product/266/33952) | [링크](#FileDeleted) |
| 태스크 플로우 상태 변경 | [링크](https://intl.cloud.tencent.com/document/product/266/33953) | [링크](#ProcedureStateChanged) |
| 비디오 편집 완료 | [링크](https://intl.cloud.tencent.com/document/product/266/33954) | - |
| 비디오 트랜스코딩 완료 | [링크](https://intl.cloud.tencent.com/document/product/266/33957) | [링크](#TranscodeComplete) |
| 시점 화면 캡처 완료 | [링크](https://intl.cloud.tencent.com/document/product/266/33958) | [링크](#CreateSnapshotByTimeOffsetComplete) |
| 스프라이트 이미지 생성 완료 | [링크](https://intl.cloud.tencent.com/document/product/266/33959) | [링크](#CreateImageSpriteComplete) |
| 비디오 클리핑 완료 | [링크](https://intl.cloud.tencent.com/document/product/266/33960) | [링크](#ClipComplete) |
| 비디오 접합 완료 | [링크](https://intl.cloud.tencent.com/document/product/266/33961) | [링크](#ConcatComplete) |

## v2.0 API 형식의 AS 이벤트 알림 목록
<span id="NewFileUpload"></span>
### 비디오 업로드 완료
#### 매개변수 설명
| 매개변수 이름 | 유형 | 설명 |
| -- | -- | -- |
| version | String | 항상 `4.0`인 콜백 버전 번호. |
| eventType | String | 항상 `NewFileUpload`인 콜백 유형. |
| data.fileId | String | 파일의 고유 ID. |
| data.fileName | String | 파일 표시 이름. |
| data.coverUrl | String | 파일 커버 주소. |
| data.fileUrl  | String | 파일 재생 주소. |
| data.author | String | 작가 정보. |
| data.sourceType | String | 파일 업로드 소스. 유효 값: Record(녹화), ClientUpload(클라이언트에서 업로드), ServerUpload(서버에서 업로드). |
| data.sourceContext | String | 업로드할 때 통과할 필드를 지정합니다. 이 필드는 현재 최대 256바이트를 포함할 수 있습니다. |
| data.streamId | String | 레코더에서 업로드할 때만 사용되는 스트림 ID입니다. |
| data.procedureTaskId | String | 비디오가 업로드된 후 지정된 프로세스가 수행되면 이 매개변수는 프로세스 작업 ID가 됩니다. |
| data.transcodeTaskId | String | 비디오가 업로드된 후 트랜스코딩이 시작되면 이 매개변수는 트랜스코딩 작업 ID가 됩니다. |

#### 예시
```
{
	"version": "4.0",
	"eventType": "NewFileUpload",
	"data": {
		"fileId": "5285890784273533167",
		"fileName": "동물의 세계",
		"coverUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.jpg",
		"fileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.flv",
		"transcodeTaskId": "transcode-0bee89b07a248e27c83fc3d5951213c1",
		"procedureTaskId": "125676836723-mango-fa2fdf6a0f850d673be119cf51a7603a",
		"sourceType": "Record",
		"sourceContext": "rtmp://54xx.livepush.myqcloud.com/live?bizid=54xx&record=mp4&xx",
		"author": "CCTV 녹화",
		"streamId": "54xx_45"
	}
}
```

<span id="PullComplete"></span>
### URL 풀링 비디오 업로드 완료
#### 매개변수 설명
| 매개변수 이름 | 유형 | 설명 |
| -- | -- | -- |
| version | String | 항상 `4.0`인 콜백 버전 번호. |
| eventType | String | 항상 `PullComplete`인 콜백 유형. |
| data | Object | 특정 콜백 데이터. |
| data.vodTaskId | String | 업로드 작업 ID 가져오기. |
| data.status | Integer | 오류 코드 .0: 성공, 기타 값: 실패. |
| data.message | String | 오류 정보.  |
| data.fileId | String | 접합 요청이 시작된 후 얻은 고유 ID. |
| data.fileUrl | String | 비디오 업로드 완료 후 획득한 URL. |
| data.transcodeTaskId | String | 비디오가 업로드된 후 트랜스코딩이 시작되면 이 매개변수는 트랜스코딩 작업 ID가 됩니다. |

#### 예시
```json
{
    "version":"4.0",
    "eventType":"PullComplete",
    "data":{
        "status":0,
        "message":"",
        "vodTaskId":"Pull-f5ac8127b3b6b85cdc13f237c6005d8",
        "fileId":"14508071098244959037",
        "fileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.flv",
        "transcodeTaskId":"transcode-0bee89b07a248e27c83fc3d5951213c1"
    }
}
```

<span id="FileDeleted"></span>
### 비디오 삭제 완료
#### 매개변수 설명
| 매개변수 이름 | 유형 | 설명 |
| -- | -- | -- |
| version | String | 항상 `4.0`인 콜백 버전 번호. |
| eventType | String | 항상 FileDeleted인 콜백 유형. |
| data.status | Integer | 삭제 반환 값. 0: 성공, 기타 값: 실패 |
| data.message | String | 삭제 오류 메시지. |
| data.fileInfo | Array | 삭제된 파일의 정보. |
| data.fileInfo.n.fileId | String | 삭제된 파일의 ID. |

#### 예시
```json
{
    "version":"4.0",
    "eventType":"FileDeleted",
    "data":{
        "status":0,
        "message":"",
        "fileInfo":[
            {
                "fileId":"24961954183381008"
            }
        ]
    }
}
```

<span id="ProcedureStateChanged"></span>
### 태스크 플로우 상태 변경
#### 매개변수 설명
| 매개변수 이름 | 유형 | 설명 |
| -- | -- | -- |
| version | String | 항상 `4.0`인 이벤트 알림 버전 번호. |
| eventType | String | 항상 `ProcedureStateChanged`인 이벤트 유형. |
| data | Object | 특정 콜백 데이터. |
| data.status | String | 태스크 플로우 상태. 유효 값: PROCESSING, FINISH. |
| data.errCode | Integer | 오류 코드. 0: 성공, 다른 값: 실패. |
| data.message | String | 오류 정보. |
| data.fileId | String | 파일 ID. |
| data.metaData | Object | 지정해야 하는 비디오 메타데이터. 이 필드에 대한 자세한 내용은 [metaData(비디오 메타데이터)](#metadata.EF.BC.88.E8.A7.86.E9.A2.91.E5.85.83.E4.BF.A1.E6.81.AF.EF.BC.89)를 참고하십시오. |
| data.contentReviewList | Array | 콘텐츠 심사 결과 목록입니다. 이 필드에 대한 자세한 내용은 [contentReviewList(콘텐츠 심사 목록)](#contentreviewlist.EF.BC.88.E5.86.85.E5.AE.B9.E5.AE.A1.E6.A0.B8.E5.88.97.E8.A1.A8.EF.BC.89)을 참고하십시오. |
| data.aIAnalysisList | Array | 스마트 분석 결과 목록입니다. 이 필드에 대한 자세한 내용은 [aIAnalysisList(스마트 분석 목록)](#aianalysislist.EF.BC.88.E6.99.BA.E8.83.BD.E5.88.86.E6.9E.90.E5.88.97.E8.A1.A8.EF.BC.89)을 참고하십시오. |
| data.drm | Object | 파일 암호화 정보. 이 필드는 태스크 플로우를 시작할 때 [트랜스코딩 제어 매개변수](https://intl.cloud.tencent.com/document/product/266/34125#transcode.EF.BC.88.E8.BD.AC.E7.A0.81.E6.8E.A7.E5.88.B6.E5.8F.82.E6.95.B0.EF.BC.89)에 암호화를 지정한 경우에만 존재합니다. 이 필드에 대한 자세한 내용은 [drm(비디오 암호화 정보)](#drm.EF.BC.88.E8.A7.86.E9.A2.91.E5.8A.A0.E5.AF.86.E4.BF.A1.E6.81.AF.EF.BC.89)를 참고하십시오. |
| data.processTaskList | Array | 태스크 플로우에 포함된 작업 목록. 이 필드에 대한 자세한 내용은 [processTaskList(작업 목록)](#processtasklist.EF.BC.88.E4.BB.BB.E5.8A.A1.E5.88.97.E8.A1.A8.EF.BC.89)를 참고하십시오. |

##### metaData(비디오 메타데이터)
| **매개변수 이름** | **유형** | **설명** |
| -- | -- | -- |
| size | Integer | 비디오 크기. 단위: 바이트. |
| container | String | M4A 및 MP4와 같은 컨테이너 유형. |
| bitrate | Integer | 비디오 스트림의 평균 비트 레이트와 오디오 스트림의 비트 레이트의 합계. 단위: kbps |
| height | Integer | 비디오 스트림의 최대 높이 값. 단위: px. |
| width | Integer | 비디오 스트림의 최대 너비 값. 단위: px. |
| md5 | String | 비디오의 MD5 값. |
| duration | Integer | 비디오 지속 시간. 단위: 초. |
| rotate | Integer | 비디오 녹화 중 선택한 각도. 단위: 도. |
| videoStreamList | Array | 비디오 스트림 정보. |
| videoStreamList.bitrate | Integer | 비디오 스트림의 비트 레이트. 단위: kbps. |
| videoStreamList.height | Integer | 비디오 스트림의 높이. 단위: px. |
| videoStreamList.width | Integer | 비디오 스트림의 너비. 단위: px. |
| videoStreamList.codec | String | H.264와 같은 비디오 스트림의 인코더. |
| videoStreamList.fps | Integer | 프레임 속도. 단위: Hz. |
| audioStreamList | Array | 오디오 스트림 정보. |
| audioStreamList.bitrate | Integer | 오디오 스트림의 비트 레이트. 단위: kbps |
| audioStreamList.samplingRate | Integer | 오디오 스트림의 샘플 속도. 단위: Hz. |
| audioStreamList.codec | String | AAC와 같은 오디오 스트림의 인코더. |

##### drm(비디오 암호화 정보)
| **매개변수 이름** | **유형** | **설명** |
| -- | -- | -- |
| definition | Integer | 암호화 템플릿 ID. |
| keySource | String | 항상 `VodBuildInKMS`인 KMS 유형. |
| getKeyUrl | String | 복호화 키를 가져오기 위한 URL. |
| edkList | Array | 암호화된 데이터 키 목록. |

##### contentReviewList(콘텐츠 심사 목록)
콘텐츠 심사 정보 목록입니다. 현재는 [포르노 정보 감지](#porn.EF.BC.88.E9.89.B4.E9.BB.84.EF.BC.89)만 지원됩니다.

##### Porn(음란물 감지)
| **매개변수 이름** | **유형** | **설명** |
| -- | -- | -- |
| taskType | String | 항상 `Porn`인 작업 유형. |
| status | String | 작업 상태. 유효 값: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | 오류 코드. 0: 성공. 다른 값: 실패. 특히 30009 소스 파일 예외로 인한 실패, 30010 시스템 오류 또는 알 수 없는 오류. |
| message | String | 오류 정보. |
| input | Object | 작업 정보 입력. |
| input.definition | Integer | 포르노 정보 감지 템플릿 ID |
| output | Object | 작업이 성공한 경우에만 존재하는 작업의 출력 정보. |
| output.confidence | Float | 비디오에서 감지된 포르노 정보의 점수. 값 범위: 0 – 100. |
| output.suggestion | String | 감지된 포르노 정보에 대한 제안. 유효 값: 통과, 검토, 차단. |
| output.segments | Array | 감지된 포르노 정보가 포함된 비디오 세그먼트. |
| output.segments.startTimeOffset | Float | 의심되는 세그먼트의 시작 시간 오프셋. 단위: 초. |
| output.segments.endTimeOffset | Float | 의심되는 세그먼트의 시작 시간 오프셋. 단위: 초. |
| output.segments.confidence | Float | 의심되는 포르노 세그먼트의 점수. |
| output.segments.suggestion | Float | 의심되는 세그먼트의 포르노 정보 감지에 대한 제안. 유효 값: 통과, 검토, 차단. |
| output.segments.url | String | 의심되는 이미지의 URL(영구적으로 저장되지 않고 일정 시간이 지나면 만료됨). |
| output.segments.picUrlExpireTimeStamp | Integer | 의심되는 이미지 URL의 만료 시간(Unix 타임스탬프) |

##### aIAnalysisList(스마트 분석 목록)
스마트 분석 정보 목록입니다. 현재 다음 유형을 사용할 수 있습니다.
- [Classification(지능형 분류)](#classification.EF.BC.88.E6.99.BA.E8.83.BD.E5.88.86.E7.B1.BB.EF.BC.89)
- [Tag(지능형 태그)](#tag.EF.BC.88.E6.99.BA.E8.83.BD.E6.A0.87.E7.AD.BE.EF.BC.89)

##### Classification(지능형 분류)
| **매개변수 이름** | **유형** | **설명** |
| -- | -- | -- |
| taskType | String | 항상 `Classification`인 작업 유형. |
| status | String | 작업 상태. 유효 값: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | 오류 코드. 0: 성공, 다른 값: 실패, 특히 `30009` 소스 파일 예외로 인한 실패, `30010` 시스템 오류 또는 알 수 없는 오류. |
| message | String | 오류 정보. |
| input | Object | 작업 정보 입력. |
| input.definition | Integer | 지능형 분류 템플릿 ID. |
| output | Object | 작업이 성공한 경우에만 존재하는 작업의 출력 정보. |
| output.classifications | Array | 카테고리 정보 목록. |
| output.classifications.classification | String | 카테고리 이름. |
| output.classifications.confidence | Float | 분류 신뢰도. |

##### Tag(지능형 태그)
| **매개변수 이름** | **유형** | **설명** |
| -- | -- | -- |
| taskType | String | 항상 `Tag`인 작업 유형. |
| status | String | 작업 상태. 유효 값 PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | 오류 코드. 0: 성공, 다른 값: 실패, 특히 `30009` 소스 파일 예외로 인한 실패, `30010` 시스템 오류 또는 알 수 없는 오류. |
| message | String | 오류 정보. |
| input | Object | 작업 정보 입력. |
| input.definition | Integer | 지능형 태그 템플릿 ID |
| output | Object | 작업이 성공한 경우에만 존재하는 작업의 출력 정보. |
| output.tags | Array | 정렬 |
| output.tags.tag | String | 태그 이름. |
| output.tags.confidence | Float | 태그 신뢰도. |

##### processTaskList(작업 목록)
작업 정보 목록입니다. 현재 다음 유형을 사용할 수 있습니다.
- [Trancode(트랜스코딩 작업)](#trancode.EF.BC.88.E8.BD.AC.E7.A0.81.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [AnimatedGraphics(애니메이션 이미지 생성 작업)](#animatedgraphics.EF.BC.88.E8.BD.AC.E5.8A.A8.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [SampleSnapshot(샘플링된 화면 캡처 작업)](#samplesnapshot.EF.BC.88.E9.87.87.E6.A0.B7.E6.88.AA.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [CoverBySnapshot(커버 생성 작업)](#coverbysnapshot.EF.BC.88.E6.88.AA.E5.9B.BE.E5.9B.BE.E7.89.87.E4.BD.9C.E4.B8.BA.E8.A7.86.E9.A2.91.E5.B0.81.E9.9D.A2.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [SnapshotByTimeOffset(시점 화면 캡처 작업)](#snapshotbytimeoffset.EF.BC.88.E6.8C.89.E6.97.B6.E9.97.B4.E7.82.B9.E6.88.AA.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)
- [ImageSprites(스프라이트 이미지 생성 작업)](#imagesprites.EF.BC.88.E9.9B.AA.E7.A2.A7.E5.9B.BE.E6.88.AA.E5.9B.BE.E4.BB.BB.E5.8A.A1.EF.BC.89)


##### Trancode(트랜스코딩 작업)
| **매개변수 이름** | **유형** | **설명** |
| -- | -- | -- |
| taskType | String | 항상 `Transcode`인 작업 유형 |
| status | String | 작업 상태. 유효 값: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | 오류 코드. 0: 성공, 다른 값: 실패. 특히 `30009` 소스 파일 예외로 인한 실패, `30010` 시스템 오류 또는 알 수 없는 오류. |
| message | String | 오류 정보. |
| input | Object | 작업 정보 입력. |
| input.definition | Integer | 트랜스코딩 템플릿 ID. |
| input.watermark | Integer | 워터마크 설정 여부. 1: 네, 0: 아니요. 트랜스코딩 구성에 따라 다름. |
| input.mosaicList | Array | 요소가 단일 모자이크 정보인 모자이크 목록. |
| input.mosaicList.width | String | 모자이크 폭. |
| input.mosaicList.height | String | 모자이크 높이. |
| input.mosaicList.left | String | 비디오에서 모자이크의 왼쪽 상단 모서리의 수평 위치. |
| input.mosaicList.top | String | 비디오에서 모자이크의 왼쪽 상단 모서리의 수직 위치. |
| input.mosaicList.startTimeOffset | Float | 비디오에서 모자이크의 시작 시간. |
| input.mosaicList.endTimeOffset | Float | 비디오에서 모자이크의 종료 시간. |
| output | Object | 작업이 성공한 경우에만 존재하는 작업의 출력 정보. |
| output.url | String | 비디오 URL. |
| output.size | Integer | 비디오 크기. 단위: bytes. |
| output.container | String | M4A 및 MP4와 같은 컨테이너 유형. |
| output.bitrate | Integer | 비디오 스트림의 비트레이트와 오디오 스트림의 비트레이트의 합. 단위: kbps. |
| output.height | Integer | 비디오 스트림의 최대 높이 값. 단위: px. |
| output.width | Integer | 비디오 스트림의 최대 너비 값. 단위: px. |
| output.md5 | String | 비디오의 MD5 값. |
| output.duration | Integer | 비디오 지속 시간. 단위: 초. |
| output.videoStreamList | Array | 요소 필드가 메타데이터의 videoStreamList와 동일한 비디오 스트림 정보. |
| output.audioStreamList | Array | 요소 필드가 메타데이터의 audioStreamList와 동일한 오디오 스트림 정보. |

#### AnimatedGraphics(애니메이션 이미지 생성 작업)
| **매개변수 이름** | **유형** | **설명** |
| -- | -- | -- |
| taskType | String | 항상 `AnimatedGraphics`인 작업 유형. |
| status | String | 작업 상태. 유효 값: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | 오류 코드. 0: 성공, 다른 값: 실패, 특히 `30009` 소스 파일 예외로 인한 실패, `30010` 시스템 오류 또는 알 수 없는 오류. |
| message | String | 오류 정보. |
| input | Object | 작업 정보 입력. |
| input.definition | Integer | 애니메이션 이미지 생성 템플릿 ID. |
| input.startTime | Integer | 비디오에서 애니메이션 이미지의 시작 시간. 단위: 초. |
| input.endTime | Integer | 비디오에서 애니메이션 이미지의 종료 시간. 단위: 초. |
| output | Object | 작업이 성공한 경우에만 존재하는 작업의 출력 정보. |
| output.url | String | 애니메이션 이미지 URL. |
| output.container | String | 애니메이션 이미지 유형. 유효 값: GIF, WEBP. |
| output.fps | Integer | 애니메이션 이미지의 프레임 속도. 단위: fps. |
| output.height | Integer | 애니메이션 이미지의 높이. 단위: px. |
| output.width | Integer | 애니메이션 이미지의 너비. 단위: px. |

#### SampleSnapshot(샘플링된 화면 캡처 작업)
| **매개변수 이름** | **유형** | **설명** |
| -- | -- | -- |
| taskType | String | 항상 `SampleSnapshot`인 작업 유형. |
| status | String | 작업 상태. 유효 값: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | 오류 코드. 0: 성공, 다른 값: 실패, 특히 `30009` 소스 파일 예외로 인한 실패, `30010` 시스템 오류 또는 알 수 없는 오류. |
| message | String | 오류 정보. |
| input | Object | 작업 정보 입력. |
| input.definition | Integer | 샘플링된 화면 캡처 템플릿 ID. |
| input.watermarkDefinition | Array | 정수 배열인 워터마킹 템플릿 ID 목록. |
| output | Object | 작업이 성공한 경우에만 존재하는 작업의 출력 정보. |
| output.imageUrls | Array | 문자열 배열인 생성된 스크린샷의 URL 목록. |

#### SnapshotByTimeOffset(시점 화면 캡처 작업)
| **매개변수 이름** | **유형** | **설명** |
| -- | -- | -- |
| taskType | String | 항상 `SnapshotByTimeOffset`인 작업 유형. |
| status | String | 작업 상태. 유효 값: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | 오류 코드. 0: 성공, 다른 값: 실패, 특히 `30009` 소스 파일 예외로 인한 실패, `30010` 시스템 오류 또는 알 수 없는 오류. |
| message | String | 오류 정보. |
| input | Object | 작업 정보 입력. |
| input.definition | Integer | 시점 화면 캡처 템플릿 ID. |
| input.timeOffset | Array | 정수 배열인 밀리초 단위의 화면 캡처 시간 오프셋 |
| input.watermarkDefinition | Array | 정수 배열인 워터마킹 템플릿 ID 목록. |
| output | Object | 작업이 성공한 경우에만 존재하는 작업의 출력 정보. |
| output.imgInfo | Array | 생성된 스크린샷의 정보 목록. |
| output.imgInfo.timeOffset | Integer | 스크린샷의 시간 오프셋. 단위: 밀리초. |
| output.imgInfo.url | String | 스크린샷 URL. |

#### CoverBySnapshot(커버 생성 작업)

| **매개변수 이름** | **유형** | **설명** |
| -- | -- | -- |
| taskType | String | 항상 `CoverBySnapshot`인 작업 유형. |
| status | String | 작업 상태. 유효 값: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | 오류 코드. 0: 성공, 다른 값: 실패, 특히 `30009` 소스 파일 예외로 인한 실패, `30010` 시스템 오류 또는 알 수 없는 오류. |
| message | String | 오류 정보. |
| input | Object | 작업 정보 입력. |
| input.definition | Integer | 샘플링된 화면 캡처 템플릿 ID. |
| input.positionType | String | 화면 캡처 모드. Time: 시점별 화면 캡처. Percent: 백분율로 화면 캡처. |
| input.position | Integer | 스크린 캡처 위치. 시점 화면 캡처의 경우 지정된 시점(초 단위)에서 스크린샷을 캡처하여 커버로 사용하는 것을 의미합니다. 스크린샷 캡처 비율의 경우 지정된 비율의 비디오 재생 시간으로 스크린샷을 찍어 커버로 사용하는 것을 의미합니다. |
| input.watermarkDefinition | Array | 정수 배열인 워터마킹 템플릿 ID 목록. |
| output | Object | 작업이 성공한 경우에만 존재하는 작업의 출력 정보. |
| output.imageUrl | Array | 커버로 사용되는 스크린샷의 URL. |

#### PullFile(비디오 파일 풀링 작업)
| **매개변수 이름** | **유형** | **설명** |
| -- | -- | -- |
| taskType | String | 항상 `PullFile`인 작업 유형. |
| status | String | 작업 상태. 유효 값: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | 오류 코드. 0: 성공, 다른 값: 실패. |
| message | String | 오류 정보. |
| input | Object | 작업 정보 입력. |
| input.url | String | 가져올 동영상의 URL. |
| input.fileName | String | 비디오 파일 이름. |
| input.md5 | Integer | 비디오 파일의 MD5 값. |
| output | Object | 작업이 성공한 경우에만 존재하는 작업의 출력 정보. |
| output.fileId | String | 비디오 파일 ID. |
| output.fileSize | String | 비디오 파일 크기. |
| output.url | String | 비디오 파일 재생 주소. |

#### ImageSprites(스프라이트 이미지 생성 작업)
| **매개변수 이름** | **유형** | **설명** |
| -- | -- | -- |
| taskType | String | 항상 `ImageSprites`인 작업 유형. |
| status | String | 작업 상태. 유효 값: PROCESSING, SUCCESS, FAIL. |
| errCode | Integer | 오류 코드. 0: 성공, 다른 값: 실패. |
| message | String | 오류 정보. |
| input | Object | 작업이 성공한 경우에만 존재하는 작업의 입력 정보. |
| input.definition | Integer | 스프라이트 이미지 생성 템플릿 ID. |
| output | Object | 작업의 정보 출력. |
| output.totalCount | Integer | 스프라이트 이미지의 총 서브 이미지 수 |
| output.urlList | Array | 문자열 배열. 생성된 스프라이트 이미지의 URL 목록. |
| output.webVttUrl | String | 스프라이트 이미지의 서브 이미지 간의 위치-시간 관계에 대한 WebVtt 파일의 주소. |

#### 예시
```json
{
    "version":"4.0",
    "eventType":"ProcedureStateChanged",
    "data":{
        "vodTaskId":"125676836723-xxx-25f5aac63",
        "status":"PROCESSING",
        "message":"",
        "errCode":0,
        "fileId":"14508071098244959037",
        "metaData":{
            "size":10556,
            "container":"m4a",
            "bitrate":246035,
            "height":480,
            "width":640,
            "md5":"b3ae6ed07d9bf4efeeb94ed2d37ff3e3",
            "duration":3601,
            "videoStreamList":[
                {
                    "bitrate":246000,
                    "height":480,
                    "width":640,
                    "codec":"h264",
                    "fps":22
                }
            ],
            "audioStreamList":[
                {
                    "codec":"aac",
                    "samplingRate":44100,
                    "bitrate":35
                }
            ]
        },
        "drm":{
            "definition":10,
            "getKeyUrl":"https://123.xxx.com/getkey",
            "keySource":"VodBuildInKMS",
            "edkList":[
                "232abc30"
            ]
        },
        "contentReviewList":[
            {
                "taskType":"Porn",
                "status":"SUCCESS",
                "errCode":0,
                "message":"",
                "input":{
                    "definition":10
                },
                "output":{
                    "confidence":98,
                    "suggestion":"block",
                    "segments":[
                        {
                            "startTimeOffset":20,
                            "endTimeOffset":120,
                            "confidence":98,
                            "suggestion":"block",
                            "url":"http://125676836723.vod2.myqcluod.com/xxx/xxx/xx.jpg",
                            "picUrlExpireTimeStamp":1530005146
                        },
                        {
                            "startTimeOffset":120,
                            "endTimeOffset":130,
                            "confidence":54,
                            "suggestion":"review",
                            "url":"http://125676836723.vod2.myqcluod.com/xxx/xxx/xx.jpg",
                            "picUrlExpireTimeStamp":1530005146
                        }
                    ]
                }
            }
        ],
        "processTaskList":[
            {
                "taskType":"Transcode",
                "status":"PROCESSING",
                "errCode":0,
                "message":"",
                "input":{
                    "definition":10,
                    "watermark":1
                }
            },
            {
                "taskType":"Transcode",
                "status":"SUCCESS",
                "errCode":0,
                "message":"",
                "input":{
                    "definition":20,
                    "watermark":1
                },
                "output":{
                    "url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f20.mp4",
                    "size":10556,
                    "container":"m4a",
                    "md5":"b3ae6ed07d9bf4efeeb94ed2d37ff3e3",
                    "bitrate":246035,
                    "height":480,
                    "width":640,
                    "duration":3601,
                    "videoStreamList":[
                        {
                            "bitrate":246000,
                            "height":480,
                            "width":640,
                            "codec":"h264",
                            "fps":20
                        }
                    ],
                    "audioStreamList":[
                        {
                            "codec":"aac",
                            "samplingRate":44100,
                            "bitrate":35
                        }
                    ]
                }
            },
            {
                "taskType":"SampleSnapshot",
                "status":"SUCCESS",
                "errCode":0,
                "message":"",
                "input":{
                    "definition":10
                },
                "output":{
                    "imageUrls":[
                        "http://125676836723.vod2.myqcloud.com/xxx/xxx/shotup/xx1.png",
                        "http://125676836723.vod2.myqcloud.com/xxx/xxx/shotup/xx2.png",
                        "http://125676836723.vod2.myqcloud.com/xxx/xxx/shotup/xx3.png"
                    ]
                }
            }
        ]
    }
}
```

<span id="TranscodeComplete"></span>
### 비디오 트랜스코딩 완료
#### 매개변수 설명
| 매개변수 이름 | 유형 | 설명 |
| -- | -- | -- |
| version | String | 항상 `4.0`인 이벤트 알림 버전 번호. |
| eventType | String | 항상 `TranscodeComplete`인 이벤트 유형. |
| data | Object | 특정 콜백 데이터. |
| data.status | Integer | 오류 코드. 0: 성공, 다른 값: 실패. |
| data.message | String | 오류 정보  |
| data.fileId | String | 트랜스코딩된 파일 ID. |
| data.vodTaskId | String | 트랜스코딩 작업 ID. |

#### 예시
```json
{
    "version": "4.0",
    "eventType": "TranscodeComplete",
    "data": {
        "status": 0,
        "message": "",
        "vodTaskId": "Transcode-1edb7eb88a599d05abe451cfc541cfbd",
        "fileId": "14508071098244931831",
        "fileName": "동물의 세계",
        "duration": 599,
        "coverUrl": "http://125676836723.vod2.myqcloud.com/0/xxx/640",
        "playSet": [
            {
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
                "definition": 0,
                "vbitrate": 246000,
                "vheight": 480,
                "vwidth": 640
            },
            {
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f10.mp4",
                "definition": 10,
                "vbitrate": 149193,
                "vheight": 240,
                "vwidth": 320
            },
            {
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f20.mp4",
                "definition": 20,
                "vbitrate": 297656,
                "vheight": 480,
                "vwidth": 640
            },
            {
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f30.mp4",
                "definition": 30,
                "vbitrate": 899976,
                "vheight": 960,
                "vwidth": 1280
            }
        ]
    }
}
```

<span id="CreateSnapshotByTimeOffsetComplete"></span>
### 시점 화면 캡처 완료
#### 매개변수 설명
| 매개변수 이름 | 유형 | 설명 |
| -- | -- | -- |
| version | String | 항상 `4.0`인 콜백 버전 번호. |
| eventType | String | 항상 `CreateSnapshotByTimeOffsetComplete`인 콜백 유형. |
| data | Object | 특정 콜백 데이터. |
| data.vodTaskId | String | 시점 화면 캡처 작업 ID.  |
| data.fileId | String | 지정된 시점 스크린샷의 FileId.  |
| data.definition | Integer | 시점 스크린샷 사양. 자세한 내용은 [시점 화면 캡처를 위한 매개변수 템플릿](https://intl.cloud.tencent.com/document/product/266/33940#.E6.97.B6.E9.97.B4.E7.82.B9.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF)을 참고하십시오. |
| data.picInfo | Array | 지정된 시점 스크린샷의 정보. |

data.picInfo 배열의 각 요소는 Object이며 매개변수의 의미는 다음과 같습니다.

| 매개변수 이름 | 유형 | 설명 |
| -- | -- | -- |
| timeOffset | Integer | 스크린샷의 특정 시점. 단위: 밀리초. |
| url | String | 스크린샷 파일 URL.  |
| status | Integer | 오류 코드. 0: 성공, 다른 값: 실패. |

#### 예시
```json
{
    "version": "4.0",
    "eventType": "CreateSnapshotByTimeOffsetComplete",
    "data": {
        "vodTaskId": "CreateSnapshotByTimeOffset-1edb7eb88a599d05abe451cfc541cfbd",
        "fileId": "14508071098244929440",
        "definition": 10,
        "picInfo": [
            {
                "status": 0,
                "timeOffset": 10000,
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/1.png"
            },
            {
                "status": 0,
                "timeOffset": 20000,
                "url": "http://125676836723.vod2.myqcloud.com/xxx/xxx/2.png"
            }
        ]
    }
}
```

<span id="CreateImageSpriteComplete"></span>
### 스프라이트 이미지 생성 완료
#### 매개변수 설명
| 매개변수 이름 | 유형 | 설명 |
| -- | -- | -- |
| version | String | 항상 `4.0`인 콜백 버전 번호. |
| eventType | String | 항상 `CreateImageSpriteComplete`인 콜백 유형. |
| data | Object | 특정 콜백 데이터. |
| data.status | Integer | 오류 코드. 0: 성공, 다른 값: 실패. |
| data.message | String | 오류 정보. |
| data.vodTaskId | String | 스프라이트 이미지 생성 작업 ID. |
| data.fileId | String | 생성된 스프라이트 이미지의 FileId. |
| data.definition | Integer | 스프라이트 이미지 사양. 자세한 내용은 [스프라이트 이미지 생성 템플릿](https://intl.cloud.tencent.com/document/product/266/33940#.E9.9B.AA.E7.A2.A7.E5.9B.BE.E6.A8.A1.E6.9D.BF)을 참고하십시오. |
| data.totalCount | Integer | 스프라이트 이미지의 총 서브 이미지 수. |
| data.imageSpriteUrl | Array | 생성된 스프라이트 이미지의 정보. |
| data.webVttUrl | String | 스프라이트 이미지의 서브 이미지 간의 위치와 시간 관계에 대한 WebVtt 파일의 주소. |

#### 예시
```json
{
    "version":"4.0",
    "eventType":"CreateImageSpriteComplete",
    "data":{
        "status":0,
        "message":"",
        "vodTaskId":"CreateImageSprite-1edb7eb88a599d05abe451cfc541cfbd",
        "fileId":"14508071098244929440",
        "definition":10,
        "totalCount":106,
        "imageSpriteUrl":[
            "http://125676836723.vod2.myqcloud.com/xxx/xxx/1.png",
            "http://125676836723.vod2.myqcloud.com/xxx/xxx/2.png"
        ],
        "webVttUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.vtt"
    }
}
```

<span id="ClipComplete"></span>
### 비디오 클리핑 완료
#### 매개변수 설명
| 매개변수 이름 | 유형 | 설명 |
| -- | -- | -- |
| version | String | 항상 `4.0`인 콜백 버전 번호. |
| eventType | String | 항상 `ClipComplete`인 콜백 유형. |
| data | Object | 특정 콜백 데이터. |
| data.vodTaskId | String | 클리핑 작업 ID.  |
| data.srcFileId | String | 클리핑 작업에 대한 소스 파일의 FileId. |
| data.fileInfo | Object | 출력 비디오 파일의 정보. |

data.fileInfo에 있는 매개변수의 구체적인 의미는 다음과 같습니다.

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| fileType | String | 클리핑 파일 유형. |
| status | Integer | 이 유형의 파일에 대한 오류 코드. 0: 성공, 다른 값: 실패. |
| message | String | 오류 정보. |
| fileId | String | 클리핑 파일의 fileId. |
| fileID |String | 클리핑 파일의 URL. |

#### 예시
```json
{
    "version": "4.0",
    "eventType": "ClipComplete",
    "data": {
        "vodTaskId": "clipVideo-0a78cf44c4285026a4c",
        "srcFileId": "16092504232103571364",
        "fileInfo": {
            "fileType": "mp4",
            "status": 0,
            "message": "",
            "fileId": "14508071098244929440",
            "fileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
        }
    }
}
```


<span id="ConcatComplete"></span>
### 비디오 접합 완료
#### 매개변수 설명
| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| version | String | 항상 `4.0`인 콜백 버전 번호. |
| eventType | String | 항상 `ConcatComplete`인 콜백 유형. |
| data | Object | 특정 콜백 데이터. |
| data.vodTaskId | String | 접합 작업 ID. |
| data.fileInfo | Array | 접합된 비디오 파일의 정보. |

data.fileInfo 배열의 각 요소는 Object이며 매개변수의 의미는 다음과 같습니다.

| 매개변수 이름 | 유형 | 설명 |
|---------|---------|---------|
| fileType | String | 접합된 파일 유형. |
| status | Integer | 작업 실행 결과. 0 성공, -1 또는 4 실패. |
| message | String | 오류 정보. |
| fileId | String | 접합된 파일의 FileId. |
| fileUrl | String | 접합된 파일의 URL. |

#### 예시
```json
{
    "version": "4.0",
    "eventType": "ConcatComplete",
    "data": {
        "vodTaskId": "Concat-1edb7eb88a599d05abe451cfc541cfbd",
        "fileInfo": [
            {
                "fileType": "m3u8",
                "status": 0,
                "message": "",
                "fileId": "14508071098244931831",
                "fileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/playlist.f6.m3u8"
            },
            {
                "fileType": "mp4",
                "status": 0,
                "message": "",
                "fileId": "14508071098244929440",
                "fileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
            }
        ]
    }
}
```
