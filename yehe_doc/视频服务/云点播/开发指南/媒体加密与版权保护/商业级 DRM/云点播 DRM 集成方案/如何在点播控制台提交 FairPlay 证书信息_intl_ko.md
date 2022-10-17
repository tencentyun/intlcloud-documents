본문에서는 다음 FairPlay 인증서 정보를 VOD 콘솔에 제출하는 방법을 보여줍니다.

- FairPlay Streaming(FPS) 인증서(형식: .cer)
- 프라이빗 키 파일(형식: .pem)
- 프라이빗 키 암호
- ASK（Application Secret Key）

아직 FairPlay 인증서가 없다면 [FairPlay 인증서 신청 및 인증서 정보 제출](https://intl.cloud.tencent.com/document/product/266/46643)을 참고하십시오.

## 작업 단계
1. VOD 콘솔에 로그인합니다.

2. 왼쪽 사이드바에서 ‘비디오 처리’를 클릭한 다음 ‘ DRM 구성 ‘을 클릭하고 ‘편집’을 클릭합니다.
   ![image-20220425210931543](https://qcloudimg.tencent-cloud.cn/raw/041b560536deebd1bd5bc986d95ed289.png)

3. 인증서 파일(`fairplay.cer`), 프라이빗 키 파일(`privatekey.pem`), 프라이빗 키 암호 및 ASK를 포함한 인증서 정보를 제출하고 ‘저장’을 클릭합니다.

   ![image-20220425211140740](https://qcloudimg.tencent-cloud.cn/raw/effefe51d8ca82e46d292112eab9a3b4.png)

4. **저장**을 클릭합니다. `FairPlay` 인증서 정보가 표시됩니다.

   ![image-20220426191830269](https://qcloudimg.tencent-cloud.cn/raw/8d64c3dbb65ac6f54a81f08314ca1473.png)

## 결론

이제 VOD 콘솔에 `FairPlay` 인증서 정보를 제출했습니다.
