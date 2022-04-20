### How do I connect to ASR?
ASR currently supports connection via API and SDK (recommended). For more information, see [Quick Server API Access](https://intl.cloud.tencent.com/document/product/1118/43356) and [Quick SDK Integration and Run](https://intl.cloud.tencent.com/document/product/1118/43382)

### How do I try out the features of ASR?
To try ASR out, search for "Tencent Cloud AI Voice" on WeChat Mini Program and select ASR, or upload files or use URLs in the feature trial module in the [ASR console](https://console.cloud.tencent.com/asr). For more information, see [Feature Trial](https://intl.cloud.tencent.com/document/product/1118/43359).

### How do I update a file over 5 MB in size to the ASR console to try ASR out?
You can try ASR out by using an audio URL in the feature trial section in the [ASR console](https://console.cloud.tencent.com/asr/demonstrate). **We recommend you upload the audio file to a URL and keep the audio length below 5 hours.**

### Which ASR service should I choose in different scenarios?
- Real-Time speech recognition is applicable to scenarios with requirements for real-timeness, such as voice input method, voice robot, and meeting recording.
- One-Sentence recognition is suitable for scenarios where audio files within 60 seconds need to be recognized, such as voice SMS and voice search.
- Recording file recognition is applicable to scenarios with lengthy speeches but low requirements for real-timeness, such as customer service quality inspection and video subtitles generation.

### Are far-field and offline speech recognition features supported?
Recording file recognition, one-sentence recognition, and real-time speech recognition don't support far-field and offline speech recognition features.

### Does ASR support recognizing speeches in Chinese-English mix and dialects?
- The Mandarin engine can recognize speeches in Chinese-English mix (at the word level) and accented Mandarin.
- Real-Time speech recognition supports Mandarin, English, Cantonese, Korean, Japanese, Thai, and Shanghainese.
- One-Sentence recognition and recording file recognition support Mandarin, English, Cantonese, Japanese, and Shanghainese.

>?If you want to recognize other dialects such as Sichuan, Nanjing, or Nanchang dialect, fill out the [form](https://cloud.tencent.com/apply/p/75h8nunsh9) for application.

### How long can an ASR input audio be?
- One-Sentence recognition supports audio within 60 seconds in each call.
- Recording file recognition supports audio within 5 hours in each call.
- In real-time speech recognition, each audio segment of a data packet in the audio stream is 200 ms in length.

### What should I do if HTTP requests to ASR APIs return an authentication failure?
You can check whether your parameters are uploaded correctly against the parameter table. For quick connection, we recommend you use the SDK provided at our official website.

### Do ASR APIs have restrictions on the sample rate of audio files?
APIs don't restrict the sample rate of audio files, but if the sample rate is non-compliant, the recognition effect will be compromised.

