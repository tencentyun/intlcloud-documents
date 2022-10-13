Adaptive Bitrate Streaming(ABR)은 소스 콘텐츠가 여러 비트 레이트 또는 해상도로 인코딩되는 HTTP를 통한 스트리밍 방법입니다. 플레이어에게 전달되는 비트레이트는 네트워크 상태에 따라 다릅니다. 이렇게 하면 끊김을 줄이고 스트리밍 경험을 개선할 수 있습니다.

어댑티브 비트레이트 스트리밍을 활성화하려면 **Channel Management** 페이지에서 대상 **Channel**을 찾고 **Edit**를 클릭합니다. **Output Group Setting** 페이지로 이동할 때까지 **Next**를 클릭합니다. 이 페이지에서 다양한 비트 레이트 또는 프로토콜의 출력을 구성할 수 있습니다. 자세한 지침은 4단계 [Configure Output Groups](https://www.tencentcloud.com/document/product/1048/49584)를 참고하십시오.

다음 섹션에서는 HLS 출력에 대한 어댑티브 비트레이트 스트리밍을 구성하는 방법을 보여줍니다.

1. 먼저 트랜스코딩 템플릿을 구성해야 합니다. 오디오 템플릿은 AAC **Acodec**만 지원합니다. 오디오 **Bitrate**를 지정합니다. 입력이 TS 파일이고 Pid Selector가 지정된 경우 Mainfest에 표시되는 **Language 코드**를 구성할 수도 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/29069263bb248e573abafb9ad89ff6b9.png)

2. 어댑티브 비트레이트 스트리밍 기능은 비디오의 비트 레이트가 더 높고 네트워크 조건의 영향을 받을 가능성이 더 높기 때문에 비디오에 더 적합합니다. H.264 및 H.265 **Vcodec**이 지원되며 ABR 및 CBR의 두 가지 **Rate Control Mode** 중 하나를 선택할 수 있습니다. 또한 **Top Speed Codec Transcoding**을 활성화하여 더 낮은 비트 레이트에서 동일한 시청 경험을 제공할 수 있습니다. 최고속 코덱을 활성화한 후에는 **Rate Control Mode**를 수정할 수 없습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/5a224587b665cf507a18b65bf5949c65.png)

3. 트랜스코딩 템플릿을 구성한 후 **Outputs** 영역에서 다중 비트 레이트 출력을 구성할 수 있습니다.
![](https://qcloudimg.tencent-cloud.cn/raw/e32e9111691a28ce11bd9aa3b561d4be.png)

4. 구성 후 **완료 Done**을 클릭합니다. 이제 채널의 입력은 2개의 비트 레이트로 HLS 출력을 생성합니다.

