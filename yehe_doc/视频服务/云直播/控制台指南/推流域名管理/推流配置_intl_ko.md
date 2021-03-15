## 작업 시나리오
푸시 스트리밍 설정을 통해 해당 푸시 스트리밍 도메인의 푸시 스트리밍 주소를 생성할 수 있으며, 푸시 스트리밍 주소로 푸시 스트리밍하여 라이브 방송 스트림이 LVB 서비스로 전송, 즉 라이브 방송 비디오 업로드가 실행됩니다.

## 전제 조건
- [LVB 콘솔](https://console.cloud.tencent.com/live)에 로그인되어 있어야 합니다.
- 푸시 스트리밍 도메인이 추가되어 있어야 합니다.

## 푸시 스트리밍 주소 생성기
1. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동하여 설정할 푸시 스트리밍 도메인 또는 [Manage]를 클릭해 도메인 상세 페이지로 이동합니다.
![](https://main.qcloudimg.com/raw/f57795fb5a6497ff59a1612c5d805ad2.png)
2. [푸시 스트리밍 설정]>[푸시 스트리밍 주소 생성기]를 선택하여 다음과 같이 설정합니다.
	1. 만료 시간을 선택합니다. (예시: `2019-10-31 23:59:59`)
	2. 사용자 정의 스트림 이름 StreamName을 작성합니다. (예시: `liveteststream`)
	3. [스트리밍 주소 생성]을 클릭하면 StreamName이 있는 RTMP 푸시 스트리밍 주소가 생성됩니다.
![](https://main.qcloudimg.com/raw/a12dc5bb7d739ca7d526f35e9f22e81e.png)
RTMP 푸시 스트리밍 주소 포맷은 
```
rtmp://domain/live/StreamName?txSecret=Md5(key+StreamName+hex(time))&txTime=hex(time)
```
입니다. 다음을 참고하십시오.
		- `domain`: 라이브 방송 푸시 스트리밍 도메인
		- `AppName`: 라이브 방송 애플리케이션 이름. 기본값은 live이고 사용자 정의 가능합니다.
		- `StreamName`: 스트림 이름. 사용자 정의가 가능하며 라이브 방송 스트림을 식별하는데 사용됩니다.
		- `txSecret`: 푸시 스트리밍 인증을 활성화하면 생성되는 인증 문자열입니다.
		- `txTime`: 푸시 스트리밍 주소에 설정된 타임스탬프. 콘솔 푸시 스트리밍 주소의 유효 시간입니다.

3. 비즈니스 시나리오에 따라 [라이브 방송 푸시 스트리밍](https://intl.cloud.tencent.com/document/product/267/31558) 을 구현한 후, [스트림 관리](https://intl.cloud.tencent.com/document/product/267/31068)에서 테스트 및 비활성화, 삭제 작업을 진행할 수 있습니다.

> 
>- 생성된 푸시 스트리밍 주소는 설정된 만료 시간 내에서 사용할 수 있으며, 만료 후에는 다시 새로운 스트리밍 주소를 생성해야 합니다.
>- 푸시 스트리밍 주소를 생성하면 푸시 스트리밍 라이브 방송을 시작할 수 있습니다. 그러나 라이브 방송을 시청하려면 재생 주소를 획득해야 합니다. 자세한 내용은 [재생 설정](https://intl.cloud.tencent.com/document/product/267/31058)을 참조하십시오.


## 푸시 스트리밍 주소 예시 코드
Tencent Cloud가 제공하는 PHP 및 Java 언어 푸시 스트리밍 주소 예시 코드는 직접 해당 코드를 참조하여 푸시 스트리밍 주소를 연결할 수 있습니다. 자세한 작업 방법은 다음과 같습니다.
1. [Domain Management](https://console.cloud.tencent.com/live/domainmanage)로 이동합니다.
2. 푸시 스트리밍 도메인 또는 오른쪽 [Manage]를 클릭하여 도메인 상세 페이지로 이동합니다.
3. [푸시 스트리밍 설정]을 선택하고 스크롤을 끝까지 내려 [푸시 스트리밍 주소 예시 코드] 부분을 확인합니다.
4. 전환 탭을 클릭하여 PHP/Java 예시 코드를 확인합니다.

**푸시 스트리밍 예시 코드(PHP)**
```
/**
    * 푸시 스트리밍 주소 획득
    * key와 만료 시간을 전달하지 않는 경우 링크 도용 방지 url 리턴
    * @param domain 푸시 스트리밍에 사용하는 도메인
    *        streamName 각 푸시 스트리밍 주소를 구분하는 고유한 스트림 이름
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
```
**푸시 스트리밍 예시 코드(Java)**
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
