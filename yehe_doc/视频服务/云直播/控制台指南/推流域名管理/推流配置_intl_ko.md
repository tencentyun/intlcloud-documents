라이브 스트리밍 콘텐츠를 보호하기 위해 기본적으로 푸시 도메인에 대해 푸시 인증이 활성화되어 있습니다. 푸시 도메인의 세부 정보 페이지에서 주소 생성기를 사용하여 CSS 플랫폼에 스트림(라이브 비디오 업로드)을 푸시하는 데 사용할 수 있는 푸시 URL을 생성할 수 있습니다.

## 주의 사항

- CSS는 테스트 도메인 이름 `xxxx.tlivepush.com`을 제공합니다. 라이브 푸시를 테스트하는 데 사용할 수 있지만, 비즈니스 목적의 푸시 도메인 이름으로 사용하지 않는 것이 좋습니다. 
- 푸시 URL은 지정된 만료 시간까지 유효합니다. 만료되면 새 URL을 생성해야 합니다.

## 전제 조건

CSS 서비스를 활성화했습니다.

## 인증 설정
1.  [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **푸시 도메인** 또는 **관리**를 클릭해 도메인 상세 페이지로 이동합니다. 
2.  **푸시 설정**을 클릭하고 **인증 설정** 탭에서 **편집**을 클릭합니다.
![](https://main.qcloudimg.com/raw/f57795fb5a6497ff59a1612c5d805ad2.png)
3.  ![](https://main.qcloudimg.com/raw/5637a9d55de965fa5d35725a955f4c00.png) 팝업 창에서 푸시 인증을 활성화합니다.
4. 기본 KEY와 백업 KEY를 입력하고 **저장**을 클릭합니다.
![](https://main.qcloudimg.com/raw/a12dc5bb7d739ca7d526f35e9f22e81e.png)
>? 기본 KEY는 필수이고 백업 KEY는 선택 사항입니다. 둘 다 입력하면 하나의 KEY가 유출되었을 때 다른 KEY로 전환할 수 있습니다.

## 푸시 주소 생성기

### 작업 단계
1. [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 푸시 스트림 도메인 또는 **관리**를 클릭해 도메인 상세 페이지로 이동합니다.
2. **푸시 설정**을 선택하고 > **푸시 주소 생성기**에서 다음 설정을 완료합니다.
   1. 만료 시간을 선택합니다. (예시: `2022-11-24 16:00:35`)
   2. 사용자 정의 스트림 이름 StreamName을 입력합니다. (예: `livetest`)
   3. **푸시 주소 생성**을 클릭하여 StreamName이 포함된 푸시 URL을 생성합니다.
![](https://main.qcloudimg.com/raw/6f5ac8dcac2082aedca950c5341946ab.png)
3. 푸시 도메인에 대한 인증을 활성화하지 않은 경우 **푸시 구성** > **푸시 URL** 섹션에서 RTMP, WebRTC, SRT 및 RTMP over SRT의 4개 URL을 찾을 수 있습니다. StreamName을 귀하의 스트림 이름으로 바꾸면 해당 재생 URL을 사용하여 스트림을 재생할 수 있습니다. 
![](https://main.qcloudimg.com/raw/aa129bd839cb307993bfed247e636a41.png)


### 푸시 URL 형식

RTMP 푸시 URL은 다음과 같습니다.
```
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```

이 중,
- domain: 푸시 도메인 이름.
- AppName: 기본적으로 live이며 사용자 정의할 수 있는 라이브 스트리밍 애플리케이션 이름.
- StreamName: 라이브 스트림을 식별하는 데 사용되는 사용자 정의 스트림 이름.
- txSecret: 푸시 인증이 활성화된 후 생성된 인증 문자열.
- txTime: 콘솔에서 푸시 URL에 대해 설정된 만료 타임스탬프.

>!
>- 인증을 활성화한 경우 txTime이 유효 시간입니다.
>- 편의상 콘솔에서 설정한 시간은 실제 만료 시간입니다. **인증을 활성화하면 시스템이 푸시 URL을 생성할 때 txTime을 계산합니다**.
>- 만료 시간 전에 푸시 또는 재생을 시작하고 스트림이 중단되지 않는 한 URL이 만료된 후에도 푸시 또는 재생을 계속할 수 있습니다.

## 푸시 URL 샘플 코드
푸시 URL을 생성하기 위해 PHP, Java 및 Go 샘플 코드를 제공합니다. 코드를 보려면 다음 단계를 따르세요.

1. **[도메인 관리](https://console.cloud.tencent.com/live/domainmanage)**로 이동합니다.
2. 푸시 도메인 이름을 클릭하거나 오른쪽에 있는 **관리**를 클릭하여 세부 정보 페이지로 이동합니다.
3. **푸시 구성**을 선택하고 아래로 스크롤하여 **푸시 주소 샘플 코드**를 찾습니다.
4. 탭을 클릭하면 PHP, Java 및 Go용 샘플 코드를 볼 수 있습니다.
<dx-codeblock>
::: PHP php
/**
* 푸시 스트림 주소 획득
* key와 만료 시간을 전달하지 않는 경우 링크 도용 방지 url 반환
* @param domain 푸시 스트림에 사용하는 도메인
*        streamName 각 푸시 스트림 주소를 구분하는 고유한 스트림 이름
*        key 보안 키
*        time 만료 시간 sample 2016-11-12 12:00:00
* @return String url
*/
function getPushUrl($domain, $streamName, $key = null, $time = null){
    if($key && $time){
          $txTime = strtoupper(base_convert(strtotime($time),10,16));
          //txSecret = MD5( KEY + streamName + txTime )
          $txSecret = md5($key.$streamName.$txTime);
          $ext_str = "?".http_build_query(array(
                "txSecret"=> $txSecret,
                "txTime"=> $txTime
          ));
    }
    return "rtmp://".$domain."/live/".$streamName . (isset($ext_str) ? $ext_str : "");
}

echo getPushUrl("123.test.com","123456","69e0daf7234b01f257a7adb9f807ae9f","2016-09-11 20:08:07");
:::
::: Java java
package com.test;

import java.io.UnsupportedEncodingException;
import java.security.MessageDigest;
import java.security.NoSuchAlgorithmException;

public class Test {

      public static void main(String[] args) {
            System.out.println(getSafeUrl("txrtmp", "11212122", 1469762325L));
      }
    
      private static final char[] DIGITS_LOWER =
            {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'a', 'b', 'c', 'd', 'e', 'f'};
    
      /*
      * KEY+ streamName + txTime
      */
      private static String getSafeUrl(String key, String streamName, long txTime) {
            String input = new StringBuilder().
                              append(key).
                              append(streamName).
                              append(Long.toHexString(txTime).toUpperCase()).toString();
    
            String txSecret = null;
            try {
                  MessageDigest messageDigest = MessageDigest.getInstance("MD5");
                  txSecret  = byteArrayToHexString(
                              messageDigest.digest(input.getBytes("UTF-8")));
            } catch (NoSuchAlgorithmException e) {
                  e.printStackTrace();
            } catch (UnsupportedEncodingException e) {
                  e.printStackTrace();
            }
    
            return txSecret == null ? "" :
                              new StringBuilder().
                              append("txSecret=").
                              append(txSecret).
                              append("&").
                              append("txTime=").
                              append(Long.toHexString(txTime).toUpperCase()).
                              toString();
      }
    
      private static String byteArrayToHexString(byte[] data) {
            char[] out = new char[data.length << 1];
    
            for (int i = 0, j = 0; i < data.length; i++) {
                  out[j++] = DIGITS_LOWER[(0xF0 & data[i]) >>> 4];
                  out[j++] = DIGITS_LOWER[0x0F & data[i]];
            }
            return new String(out);
      }
}
:::
::: GO go
package a

import (
	"crypto/md5"
	"fmt"
	"strconv"
	"strings"
	"time"
)

func GetPushUrl(domain, streamName, key string, time int64)(addrstr string){
	var ext_str string
	if key != "" && time != 0{
		txTime := strings.ToUpper(strconv.FormatInt(time, 16))
		txSecret := md5.Sum([]byte(key + streamName + txTime))
		txSecretStr := fmt.Sprintf("%x", txSecret)
		ext_str = "?txSecret=" + txSecretStr + "&txTime=" + txTime
	}
	addrstr = "rtmp://" + domain + "/live/" + streamName + ext_str
	return
}
/*
*domain: 123.test.com
*streamName: streamname
*key: 69e0daf7234b01f257a7adb9f807ae9f
*time: 2022-04-26 14:57:19 CST
*/
func main(){
	domain, streamName, key := "123.test.com", "streamname", "69e0daf7234b01f257a7adb9f807ae9f"
	//CST: ChinaStandardTimeUT, "2006-01-02 15:04:05 MST" must be const
	t, err := time.Parse("2006-01-02 15:04:05 MST", "2022-04-26 14:57:19 CST")
	if err != nil{
		fmt.Println("time transfor error!")
		return
	}
	fmt.Println(GetPushUrl(domain, streamName, key, t.Unix()))
	return
}
:::
</dx-codeblock>

## 후속 작업
푸시 URL이 생성된 후 스트림 푸시를 시작할 수 있습니다. 자세한 내용은 [라이브 방송 푸시 스트림](https://intl.cloud.tencent.com/document/product/267/31558)을 참고하십시오.
