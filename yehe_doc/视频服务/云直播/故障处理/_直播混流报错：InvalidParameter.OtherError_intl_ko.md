 ## 현상 설명
혼합 스트림 시작 시 `InvalidParameter.OtherError` 에러가 발생합니다.

## 예상 원인
- 혼합 스트림에 입력된 원본 스트림의 해상도가 2000 이상인 경우.
- 특정 스트림에서 동시에 20개 이상의 혼합 스트림을 전송한 경우.
- 채널 모드의 계정에서 범용 혼합 스트림 생성 인터페이스를 사용한 경우.

## 해결 방법
해당 하위 에러 코드에 따라 문제를 해결합니다. 다음은 자주 발생하는 에러의 해결 방법입니다.

[](id:error1)
#### 에러1: `"Message":"InnerErrCode : [ -10021 ],IrnerErrMsg: [ Params Error ]"`
현재 혼합 스트림 백그라운드는 2000 이하의 해상도만 지원하며, 혼합 스트림에 입력된 특정 스트림의 해상도 가로 또는 세로가 2000 이상인 경우, 일반적으로 `-10021` 에러가 발생합니다.

1. FFplay를 사용하여 라이브 방송 스트림을 재생하고 원본 스트림 해상도를 확인하십시오. 다음 이미지와 같이 `1920*1080`인 경우 제한을 트리거하지 않습니다.
   사용 명령어: `ffplay -i "재생 주소"`.
   ![](https://main.qcloudimg.com/raw/cf074af38048408dc5b35c6db451770c.png)  
2. [VLC 툴 재생](https://intl.cloud.tencent.com/document/product/267/32483)을 사용합니다.
   - [VLC]>[미디어]>[네트워크 스트리밍 열기]>[네트워크]를 열고 주소를 입력한 뒤 확인하면 네트워크 라이브 방송 스트림 풀링을 진행합니다.
   - [툴]>[미디어 정보]>[코덱]을 열어 라이브 방송 스트림 해상도를 조회할 수 있습니다.
     

[](id:error2)
#### 에러2: `"Message":"InnerErrCode:[ -41 ],InnerErrMsg: [ ]"`

현재 혼합 스트림 백그라운드는 하나의 스트림에서 최대 20개의 혼합 스트림 전송을 지원합니다. 일반적으로 여러 호스트가 제품을 추천하는 경우에만 동시에 하나의 스트림을 혼합 스트림으로 여러차례 중복 사용한 세션 입력이 필요합니다.

이러한 문제들은 대부분 혼합 스트림 세션의 생성으로 인하여 발생하며, 혼합 스트림을 취소할 필요없이 그대로 종료하면 특정 스트림 ID가 여러 혼합 스트림 세션에 공유되어 사용됩니다.

Tencent Cloud CSS 혼합 스트림 중 백그라운드 스트림이 중단된 것이 아닌 경우, 중단된 화면이 마지막 프레임에서 멈춰 혼합 스트림 화면 상단에 표시됩니다. 화면에 마지막 프레임이 남지 않도록 하려면 범용 혼합 스트림 인터페이스를 호출하여 취소해야 합니다. 백그라운드 스트림이 중단된 경우에는 화면 전체가 멈추게 됩니다.
- 15분 내 해당 스트림이 동일 스트림 ID로 다시 푸시 스트림에 성공할 경우, 혼합 스트리밍이 자동으로 복구됩니다.
- 두 스트리밍이 모두 중단되면 15분 후 혼합 스트림이 자동으로 취소됩니다.


[](id:error3)
#### 에러3: `"Message":"InnerErrCode:[ -4 ],InnerErrMsg: [ get liveconfig failed! ]"`

해당 에러는 사용자가 구 버전 콘솔의 계정(채널 모드)을 사용하면서 클라이언트 서버에서는 새로운 버전의 CSS API 3.0 [라이브 방송 혼합 스트리밍 인터페이스](https://intl.cloud.tencent.com/document/product/267/35997)를 호출했을 경우 발생합니다.

[CSS 콘솔 업그레이드](https://intl.cloud.tencent.com/zh/document/product/267)를 통해 새로운 버전(라이브 방송 코드 모드)으로 업그레이드하여 에러 문제를 해결하십시오.

[](id:error4)
#### 에러4: `"Message":"input stream num is not match the template id!"`

해당 에러는 Tencent가 제공하는 기본 혼합 스트림 템플릿 사용했으나 혼합 스트림 출력 스트림이 템플릿의 요건에 부합하지 않을 경우 발생합니다.
예를 들어, 10개의 템플릿을 사용하는 경우 2개의 입력 원본이 필요하고, 390개의 템플릿을 사용하는 경우 3개의 입력 원본, 즉 `2개의 멀티미디어 원본` + `1개의 백그라운드 캔버스`가 필요합니다.

매개변수 설정 및 사례 운영에 관한 자세한 내용은 [범용 혼합 스트림 생성> MixStreamTemplateId 인터페이스](https://intl.cloud.tencent.com/document/product/267/35997)을 참조하십시오.




[](id:error5)
#### 에러5: `"Message":"InnerErrCode:[ -300 ],InnerErrMsg: [ outputstreamid not avaliable, outputstreamid alread use as background in other sessionid ]"`

혼합 스트림 세션 sessionA가 백그라운드로 streamA를 출력한 뒤, 혼합 스트림 세션 sessionB를 출력합니다. 여기에서 또다시 streamA 스트림을 출력하게 되면 해당 에러가 발생합니다.

나중에 전송되는 혼합 스트림 세션 sessionB에서 **출력하는 OutputStreamName의 스트림 이름**을 **sessionA 세션 ID의 출력 스트림 이름**과 서로 다르게 설정하는 것을 권장합니다.



[](id:error6)
#### 에러6: `"Message":"InnerErrCode:[ -2 ],InnerErrMsg: [ small picture out of the background ]"`
작은 화면이 백그라운드 레이어 보다 큰 경우, 예를 들어, 백그라운드가 해상도 `1920*1080`의 캔버스이고 작은 화면의 가로 세로 해상도가 `1280*720`일 때, 오프셋 X`（LocationX）+ 1280 >1920` 또는 오프셋 Y`（LocationY）+ 720 >1080`인 경우, 위와 같은 에러가 발생합니다.
- 출력 화면 X 오프셋의 매개변수 권장 설정은 [범용 혼합 스트림 레이아웃 매개변수> LocationX](hhttps://intl.cloud.tencent.com/zh/document/product/267/30767#CommonMixLayoutParams)를 참조하십시오.
- 출력 화면 Y 오프셋의 매개변수 권장 설정은 [범용 혼합 스트림 레이아웃 매개변수> LocationY](hhttps://intl.cloud.tencent.com/zh/document/product/267/30767#CommonMixLayoutParams)를 참조하십시오.
- 더 다양한 클라우드 혼합 스트림 템플릿 사용 사례는 [클라우드 혼합 스트림](https://intl.cloud.tencent.com/document/product/267/37665)을 참조하십시오.


[](id:error7)
#### 에러7: `"Message":"InnerErrCode:[ -111 ],InnerErrMsg: [ output_stream_type is [0],but output_stream_id xxxxx is not in input stream list ]"`
사용자가 설정한 혼합 스트림 매개변수 중 [OutputStreamType](https://cloud.tencent.com/document/api/267/20474#CommonMixOutputParams)의 기본값이 0이나, 실제 출력되는 스트림 ID 이름이 사용자가 입력한 스트림 이름 목록에 없을 경우 발생하는 오류입니다.
다음 사항에 유의하십시오.
- 입력한 OutputStreamType 매개변수가 0이거나 입력한 매개변수 값이 없을 경우, 출력 OutputStreamName 매개변수에 입력한 스트림 이름 중 하나를 설정해야 합니다.
- 새로운 스트림의 혼합 스트림 OutputStreamName 스트림 이름을 생성하려는 경우에는 OutputStreamType 매개변수를 1로 설정하십시오.
- OutputStreamType 매개변수를 1로 설정하면 OutputStreamName이 InputStreamList에 나타나지 않으며, 라이브 방송 백그라운드에 동일한 ID의 스트림이 존재하지 않게 됩니다.

