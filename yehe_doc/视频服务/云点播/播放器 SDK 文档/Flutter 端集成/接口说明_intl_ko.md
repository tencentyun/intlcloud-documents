## SuperPlayerPlugin 클래스

### setGlobalLicense

**설명**

이 API는 License 설정에 사용됩니다

License 신청 및 취득 후 다음 API를 이용하여 초기화할 수 있습니다. 애플리케이션 시작 중에 이 API를 호출하는 것이 좋습니다. License가 설정되지 않은 경우 동영상 재생이 실패합니다.

**API**

```dart
static Future<void> setGlobalLicense(String licenceUrl, String licenceKey) async;
```

**매개변수 설명**

| 매개변수     | 유형   | 설명          |
| ---------- | ------ | -------------- |
| licenceUrl | String | licence의 url |
| licenceKey | String | licence의 key |

**반환값**

없음


### createVodPlayer

**설명**

이 API는 네이티브 레이어에서 VOD 플레이어 인스턴스를 생성하는 데 사용됩니다. `TXVodPlayerController`를 사용하는 경우 이미 인스턴스를 통합하므로 다른 인스턴스를 생성할 필요가 없습니다.

**API**

```dart
static Future<int?> createVodPlayer() async;
```

**매개변수 설명**

없음

**반환값**

| 반환값 | 유형   | 설명               |
| ------ | ------ | ------------------ |
| playerId | int | 플레이어 ID |


### createLivePlayer

**설명**

이 API는 네이티브 레이어에서 라이브 플레이어 인스턴스를 생성하는 데 사용되며, `TXVodPlayerController`를 사용하는 경우 이미 인스턴스를 통합하므로 다른 인스턴스를 생성할 필요가 없습니다

**API**

```dart
static Future<int?> createLivePlayer() async;
```

**매개변수 설명**

없음

**반환값**

| 반환값 | 유형   | 설명               |
| ------ | ------ | ------------------ |
| playerId | int | 플레이어 ID |


### setConsoleEnabled

**설명**

이 API는 플레이어 네이티브 log 출력을 활성화/비활성화하는 데 사용됩니다

**API**

```dart
static Future<int?> setConsoleEnabled() async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| enabled | bool | 플레이어 log 활성화/비활성화 |

**반환값**

없음


### releasePlayer

**설명**

이 API는 플레이어 리소스를 릴리스하는 데 사용됩니다.

**API**

```dart
static Future<int?> releasePlayer(int? playerId) async;
```

**매개변수 설명**

없음

**반환값**

없음


### setGlobalMaxCacheSize

**설명**

이 API는 플레이어 엔진의 최대 캐시 크기를 설정하는 데 사용됩니다. 설정 후 백엔드는 설정 값에 따라 Cache 디렉터리의 파일을 자동으로 정리합니다

**API**

```dart
static Future<void> setGlobalMaxCacheSize(int size) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| size | int | 최대 캐시 크기(단위: MB) |

**반환값**

없음


### setGlobalCacheFolderPath

**설명**

이 API는 기본적으로 App의 샌드박스 디렉터리로 설정된 캐시 경로를 설정하는 데 사용됩니다. 매개변수에 대한 전체 절대 경로 대신 상대 캐시 디렉터리만 전달하면 됩니다.

**API**

```dart
static Future<bool> setGlobalCacheFolderPath(String postfixPath) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| postfixPath | String | 기본적으로 app의 샌드박스 디렉터리로 설정되는 캐시 경로. postfixPath에 대한 전체 절대 경로 대신 상대 캐시 디렉터리만 전달하면 됩니다. Android에서 동영상는 sdcard의 Android/data/your-pkg-name/files/testCache 디렉터리에 캐시됩니다. iOS에서 동영상는 샌드박스의 Documents/testCache 디렉터리에 캐시됩니다. |

**반환값**

없음


### setLogLevel

**설명**

이 API는 log 출력 수준을 설정하는 데 사용됩니다.

**API**

```dart
static Future<void> setLogLevel(int logLevel) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| logLevel | int | 0: 모든 수준의 log </br> 1: DEBUG,INFO,WARNING,ERROR 및 FATAL log </br> 2: INFO,WARNNING,ERROR 및 FATAL log </br> 3: WARNNING,ERROR 및 FATAL log </br> 4: ERROR 및 FATAL log </br> 5: FATAL log만 </br> 6: sdk log가 없음|

**반환값**

없음


### setBrightness

**설명**

이 API는 밝기를 설정하는 데 사용됩니다. 현재 app에만 적용됩니다

**API**

```dart
static Future<void> setBrightness(double brightness) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| brightness | double | 밝기 수준. 값 범위: 0.0–1.0 |

**반환값**

없음


### restorePageBrightness

**설명**

이 API는 UI 밝기를 복원하는 데 사용됩니다. 현재 app에만 적용됩니다.

**API**

```dart
static Future<void> restorePageBrightness() async;
```

**매개변수 설명**

없음

**반환값**

없음


### getBrightness

**설명**

이 API는 현재 UI의 밝기 수준을 가져오는 데 사용됩니다.

**API**

```dart
static Future<double> getBrightness() async;
```

**매개변수 설명**

없음

**반환값**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| brightness | double | 밝기 수준. 값 범위: 0.0–1.0 |


### setSystemVolume

**설명**

이 API는 현재 시스템의 볼륨 레벨을 설정하는 데 사용됩니다

**API**

```dart
static Future<void> setSystemVolume(double volume) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| volume | double | 볼륨 수준. 값 범위: 0.0–1.0 |

**반환값**

없음


### getSystemVolume

**설명**

이 API는 현재 시스템의 볼륨 레벨을 설정하는 데 사용됩니다

**API**

```dart
static Future<double> getSystemVolume() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| volume | double | 볼륨 수준. 값 범위: 0.0–1.0 |


### abandonAudioFocus

**설명**

이 API는 오디오 포커스를 릴리스하는 데 사용되며 Android에만 적용됩니다.

**API**

```dart
static Future<double> abandonAudioFocus() async;
```

**매개변수 설명**

없음

**반환값**

없음


### requestAudioFocus

**설명**

이 API는 오디오 포커스를 요청하는 데 사용되며, Android에만 적용됩니다.

**API**

```dart
static Future<void> requestAudioFocus() async ;
```

**매개변수 설명**

없음

**반환값**

없음


### isDeviceSupportPip

**설명**

이 API는 현재 장치가 PiP(Picture-in-Picture) 모드를 지원하는지 확인하는 데 사용됩니다.

**API**

```dart
static Future<int> isDeviceSupportPip() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| isDeviceSupportPip | int | 0 PiP 모드 활성화 가능</br> -101  android 버전이 너무 낮음 </br>  -102  PiP 권한이 비활성화되었거나 장치가 PiP를 미지원 </br> -103  현재 UI가 종료됨|


### getLiteAVSDKVersion

**설명**

이 API는 현재 네이티브 레이어 플레이어 SDK의 버전 번호를 가져오는 데 사용됩니다.

**API**

```dart
static Future<String?> getLiteAVSDKVersion() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| sdkVersion | String | 현재 플레이어 SDK의 버전 |


### setGlobalEnv

**설명**

이 API는 liteav SDK 연결 환경을 설정하는 데 사용됩니다.
Tencent Cloud의 글로벌 배포 환경은 해당 리전의 해당 법률 및 규정에 따라 서로 다른 리전의 액세스 포인트에 연결되어야 합니다.

**참고**

타깃 시장이 중국 대륙인 사용자는 이 API를 호출하지 마십시오. 타깃 시장이 중국 대륙 외부에 있는 경우 당사에 문의하여 App이 GDPR을 준수하도록 env_config를 구성하는 방법을 알아보실 수 있습니다.

**API**

```dart
static Future<int> setGlobalEnv(String envConfig) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| envConfig | String | 연결할 환경이며, SDK는 기본적으로 중국 대륙 환경에 연결되어 있음 |

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| result | int | 1 설정 완료, 2 설정 실패 |



## TXVodPlayerController 클래스


### initialize

**설명**

이 API는 controller를 초기화하고 공유 텍스처 할당을 요청하는 데 사용됩니다

**API**

```dart
Future<void> initialize({bool? onlyAudio}) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| onlyAudio | bool | 선택사항. 플레이어가 오디오 전용 플레이어인지 여부 |

**반환값 설명**

없음


### startVodPlay

**참고**

10.7 버전 부터 startPlay는 startVodPlay로 대체되며 {@link SuperPlayerPlugin#setGlobalLicense}를 사용하여 Licence를 설정한 후에만 재생이 성공합니다. 그렇지 않으면 재생에 실패합니다(검은 화면이 나타남). Licence는 전역적으로 한 번만 설정하면 됩니다. CSS, UGSV 또는 동영상 재생에 Licence를 사용할 수 있습니다. 그러한 Licence가 없다면 빠르게 [무료 평가판 Licence 신청](https://www.tencentcloud.com/document/product/266/51098) 또는 공식 Licence를 [구매](https://www.tencentcloud.com/document/product/266/51098#.E8.B4.AD.E4.B9.B0.E5.B9.B6.E6.96.B0.E5.BB.BA.E6.AD.A3.E5.BC.8F.E7.89.88-license)할 수 있습니다.

**설명**

이 API는 url을 통해 동영상을 재생하는 데 사용됩니다

**API**

```dart
Future<bool> startVodPlay(String url) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| url | String | 재생할 동영상의 url |

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| result | bool | 생성 성공 여부 |


### startVodPlayWithParams

**참고**

10.7 버전 부터 startPlay는 startVodPlay로 대체되며 {@link SuperPlayerPlugin#setGlobalLicense}를 사용하여 Licence를 설정한 후에만 재생이 성공합니다. 그렇지 않으면 재생에 실패합니다(검은 화면이 나타남). Licence는 전역적으로 한 번만 설정하면 됩니다. CSS, UGSV 또는 동영상 재생에 Licence를 사용할 수 있습니다. 그러한 Licence가 없다면 [빠르게 무료 평가판 Licence 신청](https://www.tencentcloud.com/document/product/266/51098) 또는 공식 Licence를 [구매](https://www.tencentcloud.com/document/product/266/51098#.E8.B4.AD.E4.B9.B0.E5.B9.B6.E6.96.B0.E5.BB.BA.E6.AD.A3.E5.BC.8F.E7.89.88-license)할 수 있습니다.

**설명**

이 API는 field를 통해 동영상을 재생하는 데 사용됩니다.

**API**

```dart
Future<void> startVodPlayWithParams(TXPlayInfoParams params) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| appId | int | 애플리케이션 appId. 필수 입력 |
| fileId | String | 파일 id. 필수 입력 |
| timeout | String | 16진수 소문자 문자열로 변환되는 암호화된 링크 제한 시간 타임스탬프로, CDN 서버는 타임스탬프를 기반으로 링크 유효 여부를 결정 |
| exper | String | 미리보기 지속 시간, 단위: 초 |
| us | String | 링크 고유성을 높이는 고유 ID 요청 |
| sign | String | 링크 도용 방지 서명. 자세한 내용은 [개요](https://www.tencentcloud.com/document/product/266/33984)를 참고하십시오. |
| https | String | https 요청 사용 여부. 기본값: false |

**반환값 설명**

없음


### pause

**설명**

이 API는 재생 중에 동영상을 일시 중지하는 데 사용됩니다

**API**

```dart
Future<void> pause() async;
```

**매개변수 설명**

없음

**반환값 설명**

없음


### resume

**설명**

이 API는 일시 중지된 동영상 재생을 재개하는 데 사용됩니다

**API**

```dart
Future<void> resume() async;
```

**매개변수 설명**

없음

**반환값 설명**

없음


### stop

**설명**

이 API는 재생 중에 동영상을 중지하는 데 사용됩니다

**API**

```dart
Future<bool> stop({bool isNeedClear = false}) async;
```
**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| isNeedClear | bool | 마지막 프레임 이미지 삭제 여부 |

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| result | bool | 정지 성공 여부 |


### setIsAutoPlay

**설명**

이 API는 동영상 URL을 로딩하기 위해 startVodPlay를 호출한 후 동영상을 자동으로 재생할지 여부를 설정하는 데 사용됩니다

**API**

```dart
Future<void> setIsAutoPlay({bool? isAutoPlay}) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| isAutoPlay | bool | 자동 재생 여부 |

**반환값 설명**

없음


### isPlaying

**설명**

이 API는 플레이어가 현재 동영상을 재생하고 있는지 여부를 쿼리하는 데 사용됩니다

**API**

```dart
Future<bool> isPlaying() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| isPlaying | bool | 재생이 진행 중 여부 |


### setMute

**설명**

이 API는 현재 재생을 음소거할지 여부를 설정하는 데 사용됩니다

**API**

```dart
Future<void> setMute(bool mute) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| mute | bool | 재생 음소거 여부 |

**반환값 설명**

없음


### setLoop

**설명**

이 API는 동영상 재생이 끝난 후 동영상 재생을 반복할지 여부를 지정하는 데 사용됩니다

**API**

```dart
Future<void> setLoop(bool loop) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| loop    |bool  |동영상 재생 반복 여부 |

**반환값 설명**

없음


### seek

**설명**

이 API는 재생 진행을 조정하여 지정 시점을 재생하기 위해 사용됩니다

**API**

```dart
_controller.seek(progress);
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| progress | double | 대상 재생 시간(초). |

**반환값 설명**

없음


### setRate

**설명**

이 API는 재생 속도를 설정하는 데 사용됩니다

**API**

```dart
Future<void> setRate(double rate) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| rate | double | 동영상 재생 속도. 기본값: 1.0 |

**반환값 설명**

없음


### getSupportedBitrates

**설명**

이 API는 재생 중인 동영상에서 지원하는 비트레이트를 가져오는 데 사용됩니다

**API**

```dart
Future<List?> getSupportedBitrates() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 반환값 | 유형   | 설명               |
| ------ | ------ | ------------------ |
| index | int | 비트레이트 번호 |
| width | int | 비트레이트의 동영상 너비 |
| height | int | 비트레이트의 동영상 높이 |
| bitrate | int | 비트레이트 값 |

### getBitrateIndex

**설명**

이 API는 설정된 비트레이트 번호를 가져오는 데 사용됩니다

**API**

```dart
Future<int> getBitrateIndex() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 반환값 | 유형   | 설명               |
| ------ | ------ | ------------------ |
| index | int | 비트레이트 번호 |


### setBitrateIndex

**설명**

이 API는 비트레이트 번호로 현재 비트레이트를 설정하는 데 사용됩니다

**API**

```dart
Future<void> setBitrateIndex(int index) async;
```

**매개변수 설명**

| 반환값 | 유형   | 설명               |
| ------ | ------ | ------------------ |
| index | int | 비트레이트 번호. -1: 어댑티브 비트레이트 스트리밍 활성화. |

**반환값 설명**

없음


### setStartTime

**설명**

이 API는 재생 시작 시간을 지정하는 데 사용됩니다

**API**

```dart
Future<void> setStartTime(double startTime) async;
```

**매개변수 설명**

| 반환값 | 유형   | 설명               |
| ------ | ------ | ------------------ |
| startTime | double | 재생 시작 시간(초) |

**반환값 설명**

없음


### setAudioPlayoutVolume

**설명**

이 API는 동영상 볼륨 레벨을 설정하는 데 사용됩니다

**API**

```dart
Future<void> setAudioPlayoutVolume(int volume) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| volume | int | 동영상 볼륨 레벨, 값 범위: 0–100 |

**반환값 설명**

없음


### setRequestAudioFocus

**설명**

이 API는 오디오 포커스를 설정하는 데 사용되며, Android에만 적용됩니다

**API**

```dart
Future<bool> setRequestAudioFocus(bool focus) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| focus | bool | 오디오 포커스 설정 여부 |

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| result | bool | 포커스 설정 성공 여부 |


### setConfig

**설명**

이 API는 플레이어를 구성하는 데 사용됩니다

**API**

```dart
Future<void> setConfig(FTXVodPlayConfig config) async ;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| config | FTXVodPlayConfig | 자세한 내용은 'FTXVodPlayConfig' 클래스 참고 |


**반환값 설명**

없음


### getCurrentPlaybackTime

**설명**

이 API는 현재 재생 시간을 초 단위로 가져오는 데 사용됩니다

**API**

```dart
Future<double> getCurrentPlaybackTime() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| playbackTime | double | 현재 재생 시간(초) |


### getBufferDuration

**설명**

이 API는 현재 버퍼링된 동영상 재생 시간을 초 단위로 가져오는 데 사용됩니다

**API**

```dart
 Future<double> getBufferDuration();
```

**매개변수 설명**

없음

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| playbackTime | double | 현재 버퍼링된 동영상 재생 시간(초) |


### getPlayableDuration

**설명**

이 API는 재생 중인 동영상의 재생 가능한 시간을 초 단위로 가져오는 데 사용됩니다

**API**

```dart
 Future<double> getPlayableDuration() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| playableDuration | double | 현재 재생 가능한 동영상 재생 시간(초) |


### getWidth

**설명**

이 API는 재생 중인 동영상의 너비를 가져오는 데 사용됩니다

**API**

```dart
Future<int> getWidth() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| width | int | 현재 동영상 너비 |


### getHeight

**설명**

이 API는 재생 중인 동영상의 높이를 가져오는 데 사용됩니다

**API**

```dart
Future<int> getHeight() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| height | int | 현재 동영상 높이 |


### setToken

**설명**

이 API는 HLS 암호화를 위한 token을 설정하는 데 사용되며, token이 설정되면 플레이어는 URL의 파일 이름 앞에 voddrm.token을 자동으로 추가합니다

**API**

```dart
Future<void> setToken(String? token) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| token | String | 동영상 재생 token |

**반환값 설명**

없음


### isLoop

**설명**

이 API는 플레이어의 현재 재생 루프 상태를 가져오는 데 사용됩니다

**API**

```dart
Future<bool> isLoop() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| isLoop | bool | 플레이어가 루프 상태인지 여부 |


### enableHardwareDecode

**설명**

이 API는 하드웨어 디코딩을 기반으로 재생을 활성화/비활성화하는 데 사용되며, 값을 설정한 후에는 동영상 재생을 다시 시작할 때까지 적용되지 않습니다

**API**

```dart
Future<bool> enableHardwareDecode(bool enable);
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| enable | bool | 하드웨어 디코딩 활성화 여부 |

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| result | bool | 하드웨어/소프트웨어 디코딩 설정 결과 |


### dispose

**설명**

이 API는 controller를 종료하는 데 사용되며, 호출 후 모든 알림 이벤트가 종료되고 플레이어가 릴리스됩니다

**API**

```dart
void dispose() async;
```

**매개변수 설명**

없음

**반환값 설명**

없음


### getDuration

**설명**

이 API는 총 동영상 재생 지속 시간을 가져오는 데 사용됩니다

**API**

```dart
Future<double> getDuration() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| duration | double | 총 동영상 재생 지속 시간(초) |


### enterPictureInPictureMode

**설명**

이 API는 PiP 모드로 들어가는 데 사용됩니다

**API**

```dart
Future<int> enterPictureInPictureMode({String? backIconForAndroid, String? playIconForAndroid, String? pauseIconForAndroid, String? forwardIconForAndroid}) async;
```

**매개변수 설명**

매개변수는 android에만 적용됩니다

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| backIcon | String | 뒤로 가기 아이콘, 최대 크기 1MB(android 제한), 선택사항, 미설정 시 시스템 아이콘이 사용됨 |
| playIcon | String | 재생 아이콘, 최대 크기 1MB(android 제한), 선택사항, 미설정 시 시스템 아이콘이 사용됨 |
| pauseIcon | String | 일시 중지 아이콘, 최대 크기 1MB(android 제한), 선택사항, 미설정 시 시스템 아이콘이 사용됨 |
| forwardIcon | String | 앞으로 가기 아이콘, 최대 크기 1MB(android 제한), 선택사항, 미설정 시 시스템 아이콘이 사용됨 |

**반환값 설명**

| 매개변수 | 코드   | 설명               |
| ------ | ------ | ------------------ |
| NO_ERROR | 0 | 시작 성공, 오류 없음 |
| ERROR_PIP_LOWER_VERSION | -101 | android 버전이 낮음, PiP 모드 미지원 |
| ERROR_PIP_DENIED_PERMISSION | -102 | PiP 모드 권한이 활성화되지 않았거나 현재 장치가 PiP 미지원 |
| ERROR_PIP_ACTIVITY_DESTROYED | -103 | 현재 UI가 폐기됨 |
| ERROR_IOS_PIP_DEVICE_NOT_SUPPORT | -104 | 장치 모델 또는 시스템 버전이 PiP를 지원하지 않음(iPad iOS9+ 에서만 지원됨), 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_PLAYER_NOT_SUPPORT | -105 | 플레이어가 PiP를 지원하지 않음, 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_VIDEO_NOT_SUPPORT | -106 | 동영상이 PiP를 지원하지 않음, 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_IS_NOT_POSSIBLE | -107 | PiP 컨트롤러를 사용할 수 없음, 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_FROM_SYSTEM | -108 | PiP 컨트롤러에서 오류를 보고함, 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_PLAYER_NOT_EXIST | -109 | 플레이어 객체가 존재하지 않음, 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_IS_RUNNING | -110 | PiP 기능이 이미 실행 중임, 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_NOT_RUNNING | -111 | PiP 기능이 시작되지 않았음, 이 오류는 iOS에만 적용됨 |



## FTXVodPlayConfig 클래스

#### 속성 구성 설명


| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| connectRetryCount | int | 플레이어 재접속 횟수, SDK가 예외로 인해 서버에서 연결이 끊어지면 SDK는 서버에 다시 연결을 시도함 |
| connectRetryInterval | int | 두 플레이어 재접속 사이의 간격, SDK가 예외로 인해 서버에서 연결이 끊어지면 SDK는 서버에 다시 연결을 시도함 |
| timeout | int | 플레이어 연결 제한 시간 |
| playerType | int | 플레이어 유형. 0 VOD, 1 라이브 스트리밍, 2 라이브 스트림 리플레이 |
| headers | Map | 사용자 지정 http headers |
| enableAccurateSeek | bool | 정확한 seek 활성화 여부, 기본값: true |
| autoRotate | bool | true로 설정하면 PLAY_EVT_CHANGE_ROTATION 이벤트에서 얻을 수 있는 파일에 설정된 회전 각도에 따라 mp4 파일이 자동으로 회전됨. 기본값: true |
| smoothSwitchBitrate | bool | 원활한 멀티 비트레이트 HLS 스트림 전환 활성화 여부. false(기본값)로 설정하면 멀티 비트레이트 URL이 더 빨리 열리고, true로 설정하면 IDR 프레임이 정렬되었을 때 비트레이트를 부드럽게 전환할 수 있음 |
| cacheMp4ExtName | String | 캐시된 mp4 파일 이름 확장자, 기본값: mp4 |
| progressInterval | int | 진행률 콜백 간격(밀리초), 설정되지 않은 경우 SDK는 0.5초마다 한 번씩 진행 상황을 콜백함 |
| maxBufferSize | int | 재생 버퍼의 최대 크기(MB), 이 설정은 playableDuration에 영향을 미치며, 값이 클수록 미리 버퍼링된 데이터가 많음 |
| maxPreloadSize | int | 최대 사전 로딩 버퍼 크기(MB) |
| firstStartPlayBufferTime | int | 첫 번째 버퍼링 중에 로딩해야 하는 동영상 데이터 지속 시간(ms), 기본값: 100ms |
| nextStartPlayBufferTime | int | 버퍼링 시 버퍼링 중지까지의 최소 버퍼 데이터 크기(버퍼링이 부족한 데이터에 대한 보조 버퍼링 또는 seek으로 인한 진행률 표시줄 드래그 버퍼링)(ms), 기본값: 250ms |
| overlayKey | String | HLS 보안 강화 암호화 및 암호 해독 key |
| overlayIv | String | HLS 보안 강화 암호화 및 복호화 Iv|
| extInfoMap | Map | 일부 특수 구성 항목 |
| enableRenderProcess | bool | 포스트 렌더링 및 포스트 프로덕션 기능 허용 여부, 기본값: 활성화, 초고해상도 플러그인이 활성화된 후 존재하는 경우 해당 플러그인은 기본적으로 로딩됨 |
| preferredResolution | int | 우선적으로 재생에 사용되는 동영상의 해상도, preferredResolution = width * height |


## TXLivePlayerController 클래스


### initialize

**설명**

이 API는 controller를 초기화하고 공유 텍스처 할당을 요청하는 데 사용됩니다

**API**

```dart
Future<void> initialize({bool? onlyAudio}) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| onlyAudio | bool | 선택사항. 플레이어가 오디오 전용 플레이어인지 여부 |

**반환값 설명**

없음


### startLivePlay

**참고**

10.7 버전 부터 startPlay는 startLivePlay로 대체되며 {@link SuperPlayerPlugin#setGlobalLicense}를 사용하여 Licence를 설정한 후에만 재생이 성공합니다. 그렇지 않으면 재생에 실패합니다(검은 화면이 나타남). Licence는 전역적으로 한 번만 설정하면 됩니다. CSS, UGSV 또는 동영상 재생에 Licence를 사용할 수 있습니다. 그러한 Licence가 없다면 [빠르게 무료 평가판 Licence 신청](https://www.tencentcloud.com/document/product/266/51098) 또는 공식 Licence를 [구매](https://www.tencentcloud.com/document/product/266/51098#.E8.B4.AD.E4.B9.B0.E5.B9.B6.E6.96.B0.E5.BB.BA.E6.AD.A3.E5.BC.8F.E7.89.88-license)할 수 있습니다.

**설명**

이 API는 url을 통해 동영상을 재생하는 데 사용됩니다

**API**

```dart
Future<bool> play(String url, {int? playType}) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| url | String | 재생할 동영상의 url |
| playType | int | 선택사항. 지원되는 재생 유형. 기본적으로 RTMP 라이브 스트리밍이 사용되며 LIVE_RTMP, LIVE_FLV, LIVE_RTMP_ACC 및 VOD_HLS 지원. 자세한 내용은 TXPlayType 참고 |

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| result | bool | 생성 성공 여부 |


### pause

**설명**

이 API는 재생 중에 동영상을 일시 중지하는 데 사용됩니다

**API**

```dart
Future<void> pause() async;
```

**매개변수 설명**

없음

**반환값 설명**

없음


### resume

**설명**

이 API는 일시 중지된 동영상 재생을 재개하는 데 사용됩니다


**API**

```dart
Future<void> resume() async;
```

**매개변수 설명**

없음

**반환값 설명**

없음


### stop

**설명**

이 API는 재생 중에 동영상을 중지하는 데 사용됩니다

**API**

```dart
Future<bool> stop({bool isNeedClear = false}) async;
```
**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| isNeedClear | bool | 마지막 프레임 이미지 삭제 여부 |

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| result | bool | 정지 성공 여부 |


### setIsAutoPlay

**설명**

이 API는 동영상 URL을 로딩하기 위해 startVodPlay를 호출한 후 동영상을 자동으로 재생할지 여부를 설정하는 데 사용됩니다

**API**

```dart
Future<void> setIsAutoPlay({bool? isAutoPlay}) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| isAutoPlay | bool | 동영상 자동 재생 여부 |

**반환값 설명**

없음


### isPlaying

**설명**

이 API는 플레이어가 현재 동영상을 재생하고 있는지 여부를 쿼리하는 데 사용됩니다

**API**

```dart
Future<bool> isPlaying() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| isPlaying | bool | 재생 진행 중 여부 |


### setMute

**설명**

이 API는 현재 재생을 음소거할지 여부를 설정하는 데 사용됩니다

**API**

```dart
Future<void> setMute(bool mute) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| mute | bool | 음소거 여부 |

**반환값 설명**

없음


### setVolume

**설명**

이 API는 동영상 볼륨 레벨을 설정하는 데 사용됩니다

**API**

```dart
 Future<void> setVolume(int volume);
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| volume | int | 동영상 볼륨 레벨, 값 범위: 0–100 |

**반환값 설명**

없음


### setLiveMode

**설명**

이 API는 라이브 스트리밍 모드를 설정하는 데 사용됩니다

**API**

```dart
Future<void> setLiveMode(TXPlayerLiveMode mode) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| mode | int | 자동 모드, 고속 모드, 원활 모드를 포함한 라이브 스트리밍 모드 |

**반환값 설명**

없음


### setAppID

**설명**

이 API는 클라우드 기반 제어를 위한 appID를 설정하는 데 사용됩니다

**API**

```dart
Future<void> setAppID(int appId) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| appId | int | appId |

**반환값 설명**

없음


### resumeLive

**설명**

이 API는 타임 시프트 재생에서 라이브 재생을 다시 시작하는 데 사용됩니다

**API**

```dart
Future<int> resumeLive() async;
```

**매개변수 설명**

없음

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| result | int | 1 성공, 0 실패 |


### setConfig

**설명**

이 API는 플레이어를 구성하는 데 사용됩니다

**API**

```dart
Future<void> setConfig(FTXLivePlayConfig config) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| config | FTXLivePlayConfig | 자세한 내용은 'FTXLivePlayConfig' 클래스 참고 |

**반환값 설명**

없음


### enableHardwareDecode

**설명**

이 API는 하드웨어 디코딩을 기반으로 재생을 활성화/비활성화하는 데 사용되며, 값을 설정한 후에는 동영상 재생을 다시 시작할 때까지 적용되지 않습니다

**API**

```dart
Future<bool> enableHardwareDecode(bool enable);
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| enable | bool | 하드웨어 디코딩 활성화 여부 |

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| result | bool | 하드웨어/소프트웨어 디코딩 설정 결과 |


### enterPictureInPictureMode

**설명**

이 API는 PiP 모드로 들어가는 데 사용됩니다. Android에만 적용되며, 현재 iOS의 라이브 스트리밍은 PiP 모드를 지원하지 않습니다.

**API**

```dart
Future<int> enterPictureInPictureMode({String? backIconForAndroid, String? playIconForAndroid, String? pauseIconForAndroid, String? forwardIconForAndroid}) async;
```

**매개변수 설명**

매개변수는 android에만 적용됩니다

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| backIcon | String | 뒤로 가기 아이콘, 최대 크기 1MB(android 제한), 선택사항, 미설정 시 시스템 아이콘이 사용됨 |
| playIcon | String | 재생 아이콘, 최대 크기 1MB(android 제한), 선택사항, 미설정 시 시스템 아이콘이 사용됨 |
| pauseIcon | String | 일시 중지 아이콘, 최대 크기 1MB(android 제한), 선택사항, 미설정 시 시스템 아이콘이 사용됨 |
| forwardIcon | String | 앞으로 가기 아이콘, 최대 크기 1MB(android 제한), 선택사항, 미설정 시 시스템 아이콘이 사용됨 |

**반환값 설명**

| 매개변수 | 코드   | 설명               |
| ------ | ------ | ------------------ |
| NO_ERROR | 0 | 시작 성공, 오류 없음 |
| ERROR_PIP_LOWER_VERSION | -101 | android 버전이 너무 낮음, PiP 모드 미지원 |
| ERROR_PIP_DENIED_PERMISSION | -102 | PiP 모드 권한이 활성화되지 않았거나 현재 장치가 PiP 미지원 |
| ERROR_PIP_ACTIVITY_DESTROYED | -103 | 현재 UI가 폐기됨 |
| ERROR_IOS_PIP_DEVICE_NOT_SUPPORT | -104 | 장치 모델 또는 시스템 버전이 PiP를 지원하지 않음(iPad iOS9+ 에서만 지원됨), 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_PLAYER_NOT_SUPPORT | -105 | 플레이어가 PiP를 지원하지 않음, 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_VIDEO_NOT_SUPPORT | -106 | 동영상이 PiP를 지원하지 않음, 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_IS_NOT_POSSIBLE | -107 | PiP 컨트롤러를 사용할 수 없음, 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_FROM_SYSTEM | -108 | PiP 컨트롤러에서 오류를 보고함, 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_PLAYER_NOT_EXIST | -109 | 플레이어 객체가 존재하지 않음, 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_IS_RUNNING | -110 | PiP 기능이 이미 실행 중임, 이 오류는 iOS에만 적용됨 |
| ERROR_IOS_PIP_NOT_RUNNING | -111 | PiP 기능이 시작되지 않았음, 이 오류는 iOS에만 적용됨 |


### dispose

**설명**

이 API는 controller를 종료하는 데 사용됩니다. 호출 후 모든 알림 이벤트가 종료되고 플레이어가 릴리스됩니다.

**API**

```dart
void dispose() async;
```

**매개변수 설명**

없음

**반환값 설명**

없음



### switchStream

**설명**

이 API는 재생되는 스트림을 전환하는 데 사용됩니다

**API**

```dart
Future<int> switchStream(String url) async;
```

**매개변수 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| url | String | 전환할 동영상 소스|

**반환값 설명**

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| result | int | 전환 결과 |


## FTXLivePlayConfig 클래스

#### 속성 구성 설명

| 매개변수      | 유형   | 설명               |
| ------ | ------ | ------------------ |
| cacheTime | double | 플레이어 캐시 시간(초), 값은 0보다 커야 함, 기본값: 5 |
| maxAutoAdjustCacheTime | double | 자동 캐시 시간 조정 최대 시간(초), 값은 0보다 커야 함, 기본값: 5 |
| minAutoAdjustCacheTime | double | 자동 캐시 시간 조정 최소 시간(초), 값은 0보다 커야 함, 기본값: 1 |
| videoBlockThreshold | int | 플레이어 동영상 랙에 대한 알람 임계값(밀리초), 렌더링 간격이 이 임계값을 초과하는 경우에만 PLAY_WARNING_VIDEO_PLAY_LAG 알림이 전송됨 |
| connectRetryCount | int | 플레이어의 연결이 끊어졌을 때 SDK가 다시 연결을 시도하는 기본 횟수, 값 범위: 1 – 10, 기본값: 3. |
| connectRetryInterval | int | 네트워크 재연결 사이의 간격(초), 값 범위: 3 – 30, 기본값: 3. |
| autoAdjustCacheTime | bool | 플레이어 캐시 시간 자동 조정 여부. 기본값: true. true: 자동 조정 활성화. maxCacheTime 및 minCacheTime을 사용하여 각각 최대 및 최소 캐시 시간 지정 가능. false: 자동 조정 비활성화, 기본 캐시 시간(1초) 적용. cacheTime을 사용하여 캐시 시간 변경 가능. |
| enableAec | bool | AEC(음향 반향 제거) 활성화 여부, 기본값: false |
| enableMessage | bool | 메시지 채널 활성화 여부, 기본값: true |
| enableMetaData | bool | MetaData 콜백 활성화 여부. 기본값: NO. true: SDK는 EVT_PLAY_GET_METADATA 메시지를 통해 동영상 스트림의 MetaData 전달. false: SDK가 동영상 스트림의 MetaData를 발생시키지 않음. |
| flvSessionKey | String | HTTP 헤더 정보 콜백 활성화 여부, 기본값: “” |
