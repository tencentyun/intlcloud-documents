사운드 모듈은 매우 복잡한 모듈이며 SDK는 사운드 장치의 수집 및 재생 로직을 엄격하게 제어해야 합니다. 일부 시나리오에서 원격 사용자의 오디오 데이터 또는 로컬 마이크에서 수집한 오디오 데이터를 가져와야 할 때 이 기능은 실시간 음성 채팅방에서 실시간 오디오 스트림의 원시 형식 데이터를 가져올 수 있습니다.

## 전제 조건
- **음성 채팅 서비스 활성화**: [서비스 활성화](https://intl.cloud.tencent.com/document/product/607/10782)를 참고하십시오.

- **GME SDK에 액세스**: 핵심 API 및 음성 채팅 API에 대한 액세스를 포함합니다. 자세한 내용은 [Native SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/40858), [Unity SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/44544), [Unreal SDK 빠른 통합](https://intl.cloud.tencent.com/document/product/607/44545)을 참고하십시오.

- 이 기능은 실시간 음성 채팅방에 성공적으로 입장한 후에만 사용할 수 있습니다.


## 사용 프로세스

![](https://write-document-release-1258344699.cos.ap-guangzhou.tencentcos.cn/100027871376/1dc8dd42b75e11eda534525400c56988.png?q-sign-algorithm=sha1&q-ak=AKIDFgIwuCfIDr5bP0rXPSfBL-S99muzsUzE20G2ZzbEUHvIGUkMdHU_Nop0TBDetPRF&q-sign-time=1677640756;1677644356&q-key-time=1677640756;1677644356&q-header-list=&q-url-param-list=&q-signature=ed3e047ea2878a0f8c8d9af9505565973d668c72&x-cos-security-token=bK7rgYee6Vlrw9RJjpxrtdfDlY04DBKac15ccaada6282f9fde255a9532440997OaKmfZJKditLmR-Y5Yin3VA61izb_gR6LLNXiXgtF1268WFaHXvX45EF7W2KLHtzymJBTgPwIjHcXPzuunGhbeOIMce_jGCg4u0SvP8yEE4ZuGmpoyn8Jbc5DBBiY9Q3eAJkHmCQIfuNJrtWHm_S8BBNsclzTRGRV_y1J2WN8Kqjcwokmn2ogm1S_hx3lFGSic3PX2_MGnPvl2o12JywhVxXaCfYIZlvTPivBe7ZN5UAu4Dc5JiZgcZEcE9C0zE25rfQRvS83cXtSg_Xay7XhLTRaHpm_3v91ttcdVTDnCqWhWmDfVitIv1UedniDoEGHGyGgdjLcV83GdOBJmzSmqa-NlMf0ihJc1vpfFlCEUEeeLHkVNR0_0z2BjoIw7pa)

## 호출 프로세스

### 코드 가져오기

Android 플랫폼은 ITMGAudioDataObserver를 가져와야 합니다. Unity 플랫폼은 헤더 파일 ITMGEngine_Adv.cs를 가져와야 합니다.


【Java】
``` java
import com.tencent.TMG.advance.ITMGAudioDataObserver;
```

### 원본 오디오 데이터 가져오기 기능 스위치 켜기

#### 예시 코드




【Unity】
``` csharp
SetAdvanceParams("AllowDumpCapture", "1");
```

> **참고:**
> 

> 방 입장 API(EnterRoom)를 호출하기 전에 SetAdvanceParams를 호출해야 합니다.
> 


### 원본 오디오 데이터 매개변수 설정

이 API를 통해 원본 오디오 데이터 매개변수를 설정합니다.

#### 함수 프로토타입




【Unity】
``` csharp
public abstract int SetAudioDataFormat(Audio_Data_Type audioType, int sampleRate, int channelCount);
```

#### API 매개변수 목록
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>

<td rowspan="1" colSpan="1" >유형</td>

<td rowspan="1" colSpan="1" >설명</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioType</td>

<td rowspan="1" colSpan="1" >Audio_Data_Type</td>

<td rowspan="1" colSpan="1" >설정할 원본 오디오 데이터 유형</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sampleRate</td>

<td rowspan="1" colSpan="1" >int</td>

<td rowspan="1" colSpan="1" >원본 오디오 데이터의 오디오 샘플링 레이트, 48000 입력 권장</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >channelCount</td>

<td rowspan="1" colSpan="1" >int</td>

<td rowspan="1" colSpan="1" >원본 오디오 데이터의 오디오 채널 수, 2 입력 권장</td>
</tr>
</table>


#### 오디오 데이터 유형(Audio_Data_Type)
<table>
<tr>
<td rowspan="1" colSpan="1" >Audio_Data_Type 유형 열거</td>

<td rowspan="1" colSpan="1" >설명</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >AUDIO_DATA_TYPE_CAPTURE</td>

<td rowspan="1" colSpan="1" >마이크로 수집한 원본 오디오 데이터를 가져옵니다(마이크를 켜려면 먼저 EnableMic API를 호출해야 합니다).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >AUDIO_DATA_TYPE_LOOPBACK</td>

<td rowspan="1" colSpan="1" >마이크로 수집하고 음향 효과 처리한(예: 음성 변조) 원본 오디오 데이터를 가져옵니다.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >AUDIO_DATA_TYPE_SEND</td>

<td rowspan="1" colSpan="1" >업스트림 오디오 스트림(마이크로 수집되고 음향 효과를 통해 처리된 음성 및 [Accompaniment in Voice Chat](https://intl.cloud.tencent.com/document/product/607/31504) 사운드 포함)의 원본 오디오 데이터를 가져옵니다.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >AUDIO_DATA_TYPE_PLAY</td>

<td rowspan="1" colSpan="1" >스피커에서 재생되는 모든 원본 오디오 데이터를 가져옵니다(스피커를 켜려면 먼저 EnableSpeaker API를 호출해야 합니다).</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >AUDIO_DATA_TYPE_CAPTURE_PLAY</td>

<td rowspan="1" colSpan="1" >AUDIO_DATA_TYPE_CAPTURE 및 AUDIO_DATA_TYPE_PLAY의 두 가지 유형의 오디오 원본 데이터를 포함합니다. </td>
</tr>
</table>


### 오디오 원본 QHS 데이터 가져오기 시작

이 API를 통해 원본 오디오 데이터 가져오기를 시작하고 가져온 오디오 원본 데이터는 콜백을 통해 반환됩니다.

#### 함수 프로토타입




【Native】
```c
RegisteAudioDataCallback

```


【Unity】
``` csharp
public abstract int RegisteAudioDataCallback(Audio_Data_Type dataType);
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>

<td rowspan="1" colSpan="1" >유형</td>

<td rowspan="1" colSpan="1" >설명</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioType</td>

<td rowspan="1" colSpan="1" >Audio_Data_Type</td>

<td rowspan="1" colSpan="1" >원시 형식 오디오 프레임 유형</td>
</tr>
</table>


### 오디오 원본 데이터 가져오기 중지

이 API를 통해 오디오 원본 데이터 가져오기를 중지합니다.

#### 함수 프로토타입




【Native】
```c
UnRegisterAudioDataCallback
```


【Unity】
``` csharp
public abstract int UnRegisteAudioDataCallback(Audio_Data_Type dataType);
```
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>

<td rowspan="1" colSpan="1" >유형</td>

<td rowspan="1" colSpan="1" >설명</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioType</td>

<td rowspan="1" colSpan="1" >Audio_Data_Type</td>

<td rowspan="1" colSpan="1" >오디오 원본 데이터 유형</td>
</tr>
</table>


#### 예시 코드




【Objective-C】
``` objectivec

- (void)pCaptureChanged:(UISwitch *)sender {
  if (sender.on) {
      NSString *pathName = [NSString stringWithFormat:@"capture_%ld.pcm",(long)[[NSDate date] timeIntervalSince1970] * 1000];
      NSString *path = [self pcmPath:pathName];
      capFile = fopen(path.UTF8String, "wb");
      [[ITMGAudioDataObserver GetInstance] RegisteAudioDataCallback:^(int audioDatType, unsigned long long  timestamp, unsigned int sampleRate, unsigned int channelCount, int bitsType, unsigned int length, char * pcmData) {
          if (capFile) {
              fwrite(pcmData, sizeof(char), length, capFile);
          }
      }];
  } else  {
      [[ITMGAudioDataObserver GetInstance] UnRegisterAudioDataCallback];
      if (capFile) {
          fclose(capFile);
          capFile = NULL;
      }
  }
}
```


【Java】
``` java
  private void startDumpAllAudioData() {
      int nRet = ITMGAudioDataObserver.GetInstance().RegisteAudioDataCallback(this);
      showToast("RegisteAudioDataCallback AUDIO_DATA_TYPE_CAPTURE_PLAY ret:" + nRet);
      if (nRet == 0) {
          mDumpAllAudioing = true;
          mBtnDumpAll.setText("StopDumpAudioPCM");
          String dumpFilePath = String.format(Locale.getDefault(), "%s/Dump_Mic_Speaker_%d.pcm", getActivity().getExternalFilesDir(null).toString(),System.currentTimeMillis());
          try {
              File dumpFile = new File(dumpFilePath);
              mDumpAllOutputStream = new FileOutputStream(dumpFile);
          } catch (FileNotFoundException e) {
              e.printStackTrace();
          }
      }
  }

  private void stopDumpAllAudioData() {
      if (!mDumpAllAudioing) {
          return;
      }
      mDumpAllAudioing = false;
      mBtnDumpAll.setText("DumpAudioPCM");
      ITMGAudioDataObserver.GetInstance().UnRegisteAudioDataCallback();
      try {
          mDumpAllOutputStream.close();
      } catch (IOException e) {
          e.printStackTrace();
      }finally {
          mDumpAllOutputStream = null;
      }
  }
```

### 콜백 처리

원본 오디오 데이터 가져오기를 시작한 후 콜백을 통해 데이터가 반환됩니다.

#### 매개변수

콜백의 매개변수 및 설명은 다음과 같습니다.
<table>
<tr>
<td rowspan="1" colSpan="1" >매개변수</td>

<td rowspan="1" colSpan="1" >유형</td>

<td rowspan="1" colSpan="1" >설명</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >audioDatType</td>

<td rowspan="1" colSpan="1" >int</td>

<td rowspan="1" colSpan="1" >오디오 원본 데이터 유형.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >timestamp</td>

<td rowspan="1" colSpan="1" >long</td>

<td rowspan="1" colSpan="1" >오디오 프레임 처리에 사용되는 오디오 원본 데이터 타임스탬프.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >sampleRate</td>

<td rowspan="1" colSpan="1" >int</td>

<td rowspan="1" colSpan="1" >오디오 원본 데이터 샘플링 레이트.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >channelCount</td>

<td rowspan="1" colSpan="1" >int</td>

<td rowspan="1" colSpan="1" >오디오 원본 데이터 사운드 채널 수.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >bitsType</td>

<td rowspan="1" colSpan="1" >int</td>

<td rowspan="1" colSpan="1" >오디오 원본 데이터 비트, 일반적으로 16000.</td>
</tr>

<tr>
<td rowspan="1" colSpan="1" >pcmData</td>

<td rowspan="1" colSpan="1" >byte[]</td>

<td rowspan="1" colSpan="1" >오디오 원본 데이터, PCM 형식.</td>
</tr>
</table>


#### 예시 코드




【Objective-C】
``` objectivec

- (void)pCaptureChanged:(UISwitch *)sender {
  if (sender.on) {
      NSString *pathName = [NSString stringWithFormat:@"capture_%ld.pcm",(long)[[NSDate date] timeIntervalSince1970] * 1000];
      NSString *path = [self pcmPath:pathName];
      capFile = fopen(path.UTF8String, "wb");
      [[ITMGAudioDataObserver GetInstance] RegisteAudioDataCallback:^(int audioDatType, unsigned long long  timestamp, unsigned int sampleRate, unsigned int channelCount, int bitsType, unsigned int length, char * pcmData) {
          if (capFile) {
              fwrite(pcmData, sizeof(char), length, capFile);
          }
      }];
  } else  {
      [[ITMGAudioDataObserver GetInstance] UnRegisterAudioDataCallback];
      if (capFile) {
          fclose(capFile);
          capFile = NULL;
      }
  }
}
```


【Java】
``` java
  private FileOutputStream mDumpAllOutputStream;

public void OnAudioDataCallback(int audioDatType, long timestamp, int sampleRate, int channelCount, int bitsType, byte[] pcmData) {
        if(audioDatType == AUDIO_DATA_TYPE_CAPTURE_PLAY && mDumpAllOutputStream != null) {
            try {
                mDumpAllOutputStream.write(pcmData);
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
                }
```

