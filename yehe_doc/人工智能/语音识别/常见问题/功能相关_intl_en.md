
### Which ASR service should I choose in different scenarios?
- Real-time speech recognition is applicable to scenarios with requirements for real-timeness, such as voice input method, voice robot, and meeting recording.

### Are far-field and offline speech recognition features supported?
No. Currently, only real-time speech recognition supports offline speech recognition on mobile devices. If you have such needs, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Does ASR support recognizing speeches in Chinese-English mix and dialects?
- The Mandarin engine can recognize speeches in Chinese-English mix (at the word level) and accented Mandarin.
- ASR supports recognizing Mandarin and English.

>?For recognition of Malaysian, Vietnamese, Hindi, Turkish, Arabic, and other languages, [submit a ticket](https://console.tencentcloud.com/workorder/category).

### How long can an ASR input audio be?
- In real-time speech recognition, each audio segment of a data packet in the audio stream is 200 ms in length.

### What audio attributes does ASR support?
For the detailed specifications of ASR on audio attributes, see [ASR](https://intl.cloud.tencent.com/product/asr).

### In real-time speech recognition, if the audio contains multiple sentences, how do I increase the recognition accuracy?
We recommend you enable the voice activity detection (VAD) feature for audio segmentation. If the audio contains multiple sentences, VAD can detect the pauses between them and automatically divide the audio into different sentences, achieving a higher recognition accuracy.

### Does ASR support sync result call?
- Real-time speech recognition supports sync recognition result return.

### Does ASR support evaluation?
No.

### Can I copy the text returned by ASR?
No. You need to develop the text copy feature on your frontend by yourself after connecting to ASR.

### Can I set the longest recognition time for real-time speech recognition?
No, but you can directly stop recognition at any time.

### Does ASR support the MRCP protocol?
Currently, MRCP is not open to external businesses. If you want to use it, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Is ASR available as an SaaS service?
ASR supports on-premises deployment. If you need this, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
