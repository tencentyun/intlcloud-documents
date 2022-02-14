CSS 푸시 도메인은 라이브 방송 푸시 스트림 정보 보안을 위해 푸시 스트림 인증이 기본적으로 활성화되어 있습니다. 푸시 스트림 주소 상세 페이지 상의 푸시 스트림 주소 생성기를 통해 해당하는 푸시 스트림 주소를 온라인으로 생성할 수 있습니다. 푸시 스트림 주소를 사용한 온라인 푸시 스트림을 통해 라이브 방송 스트림을 CSS 서비스로 전송하여 라이브 방송 비디오를 업로드할 수 있습니다.

## 주의 사항

- CSS에서 기본적으로 테스트 도메인 `xxxx.tlivepush.com`을 제공합니다. 해당 도메인으로 푸시 스트림을 테스트할 수 있습니다. 단, 정식 서비스에서 해당 도메인을 푸시 도메인으로 사용하는 것은 권장하지 않습니다. 
- RTMP 형식의 푸시 스트림 주소 생성만 지원합니다.
- 생성된 푸시 스트림 주소는 설정된 만료 시간 내에서 사용할 수 있으며, 만료 후에는 다시 새로운 주소를 생성해야 합니다.

## 전제 조건

CSS 활성화 및 실명인증을 완료해야 합니다.

## 인증 설정
1.  [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 **푸시 도메인** 또는 **관리**를 클릭해 도메인 상세 페이지로 이동합니다. 
2.  **푸시 스트림 설정**을 클릭하고 **인증 설정** 탭에서 오른쪽에 있는 **편집**을 클릭합니다.
	![](https://main.qcloudimg.com/raw/f57795fb5a6497ff59a1612c5d805ad2.png)
3.  푸시 스트림 인증 설정 페이지로 이동한 후 ![](https://main.qcloudimg.com/raw/5637a9d55de965fa5d35725a955f4c00.png) 버튼을 클릭해 푸시 스트림 인증 활성화/비활성화를 선택합니다.
4. 메인 KEY와 서브 KEY 정보를 수정하고 **저장**을 클릭하면 적용됩니다.
![](https://main.qcloudimg.com/raw/a12dc5bb7d739ca7d526f35e9f22e81e.png)
>? 메인 KEY는 필수 입력 항목이며, 서브 KEY는 옵션 항목입니다. 메인/서브 KEY는 KEY가 유출될 경우 즉시 KEY를 변경하여 비즈니스에 영향을 미치지 않습니다.

## 푸시 스트림 주소 생성기

### 작업 단계
1. [**도메인 관리**](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 푸시 스트림 도메인 또는 **관리**를 클릭해 도메인 상세 페이지로 이동합니다.
2. **푸시 스트림 설정** > **푸시 스트림 주소 생성기**를 선택하여 다음과 같이 설정합니다
   1. 만료 시간을 선택합니다. (예시: `2021-06-30 19:26:02`)
   2. 사용자 정의 스트림 이름 StreamName을 작성합니다. (예시: `liveteststream`)
   3. **푸시 스트림 주소 생성**을 클릭하면 StreamName이 있는 RTMP 푸시 스트림 주소가 생성됩니다.
![](https://main.qcloudimg.com/raw/6f5ac8dcac2082aedca950c5341946ab.png)
3. 푸시 도메인의 재생 인증을 아직 활성화하지 않은 경우, **푸시 스트림 설정** > **푸시 스트림 주소 리졸브** 탭에서 해당 재생 도메인의 RTMP, UDP의 두 가지 재생 주소 주소를 확인할 수 있습니다. 푸시 스트림 주소 상의 StreamName(스트림 이름)을 변경하여 재생 주소와 연결하면 재생 주소로 라이브 방송 화면을 확인할 수 있습니다. 
![](https://main.qcloudimg.com/raw/aa129bd839cb307993bfed247e636a41.png)



### 푸시 스트림 주소 설명

RTMP 푸시 스트림 주소 형식:
```
rtmp://domain/AppName/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
그중에서,
- domain: 라이브 방송 푸시 스트림 도메인.
- AppName: 라이브 방송 애플리케이션 이름으로, 기본값은 live이고 사용자 정의 가능합니다.
- StreamName: 스트림 이름. 사용자 정의가 가능하며 라이브 방송 스트림을 식별하는데 사용됩니다.
- txSecret: 푸시 스트림 인증을 활성화하면 생성되는 인증 문자열입니다.
- txTime: 푸시 스트림 주소에 설정된 타임스탬프. 콘솔 푸시 스트림 주소의 유효 시간입니다.

>!
>- 도메인 인증을 활성화한 경우 실제 만료 시간은 txTime + Key 유효 시간입니다.
>- 콘솔에서는 사용 편의를 위해 설정하는 시간이 곧 실제 만료시간이 됩니다. **도메인 인증을 활성화한 경우 재생 주소 연산 시 공식에 따라 txTime을 역산출합니다**.
>- 푸시/풀 스트림은 만료 시간 이전에 수행되며, 푸시/풀 스트림이 끊어지거나 중지되지 않는 한 만료 시간 후에도 푸시/풀 스트림 상태를 정상적으로 유지할 수 있습니다.



## 푸시 스트림 주소 예시 코드

Tencent Cloud가 제공하는 PHP 및 Java 언어 푸시 스트림 주소 예시 코드는 직접 해당 코드를 참고하여 푸시 스트림 주소를 연결할 수 있습니다. 자세한 작업 방법은 다음과 같습니다.

1. **[도메인 관리](https://console.cloud.tencent.com/live/domainmanage)**로 이동합니다.
2. 푸시 스트림 도메인 또는 오른쪽 **관리**를 클릭하여 도메인 상세 페이지로 이동합니다.
3. **푸시 스트림 설정**을 선택하고 스크롤을 끝까지 내려 **푸시 스트림 주소 예시 코드** 탭을 확인합니다.
4. 탭 전환 버튼을 클릭하여 아래와 같이 PHP/Java 예시 코드를 확인합니다.
<dx-codeblock>
::: PHP php
```
/**
    * 푸시 스트림 주소 획득
    * key와 만료 시간을 전달하지 않는 경우 링크 도용 방지 url 반환
    * @param domain 푸시 스트림에 사용하는 도메인
    *        streamName 각 푸시 스트림 주소를 구분하는 고유한 스트림 이름
    *        key 보안 키
    *        time 만료 시간 sample 2016-11-12 12:00:00. 만료 타임스탬프. 단위: s
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
```
:::
::: Java java
```
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
```
:::
</dx-codeblock>



## 후속 작업
푸시 스트림 주소를 생성한 후 비즈니스 시나리오에 따라 라이브 방송 스트림을 사용할 수 있습니다. 자세한 작업 방법은 [라이브 방송 푸시 스트림](https://intl.cloud.tencent.com/document/product/267/31558)을 참고하십시오.

