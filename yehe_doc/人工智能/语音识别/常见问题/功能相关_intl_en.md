
### Which ASR service should I choose in different scenarios?
- Real-Time speech recognition is applicable to scenarios with requirements for real-timeness, such as voice input method, voice robot, and meeting recording.
- Recording file recognition is applicable to scenarios with lengthy speeches but low requirements for real-timeness, such as customer service quality inspection and video subtitles generation.
- Ultrafast recording file recognition is applicable to scenarios with lengthy speeches and high requirements for real-timeness, such as real-time subtitling and quasi-real-time quality inspection.
- One-Sentence recognition is suitable for scenarios where audio files within 60 seconds need to be recognized, such as voice SMS and voice search.
- Async audio stream recognition is applicable to scenarios where audio streams are recognized in quasi-real time and text results are returned asynchronously, such as live streaming moderation and audio/video moderation.

### A conversation of two people was recorded as a mono-channel audio file. Can ASR separate the two people's speeches in the recognition result?
ASR supports speaker separation in a Mandarin mono-channel two-people conversation recording file at a sample rate of 8 or 16 kHz.

### Are far-field and offline speech recognition features supported?
No. Currently, only real-time speech recognition supports offline speech recognition on mobile devices. If you have such needs, [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

### Does ASR support recognizing speeches in Chinese-English mix and dialects?
- The Mandarin engine can recognize speeches in Chinese-English mix (at the word level) and accented Mandarin.
- Real-Time speech recognition supports Mandarin, English, Cantonese, Korean, Japanese, Thai, and Shanghainese.
- One-Sentence recognition and recording file recognition support Mandarin, English, Cantonese, Japanese, and Shanghainese.

>?If you want to recognize other dialects such as Sichuan, Nanjing, or Nanchang dialect, fill out the [form](https://cloud.tencent.com/apply/p/75h8nunsh9) for application.

### How long can an ASR input audio be?
- One-Sentence recognition supports audio within 60 seconds in each call.
- Recording file recognition supports audio within 5 hours in each call.
- In real-time speech recognition, each audio segment of a data packet in the audio stream is 200 ms in length.

### What audio attributes does ASR support?
For the detailed specifications of ASR on audio attributes, see [ASR Details](https://cloud.tencent.com/product/asr/details).

### What audio data transfer methods and formats are supported for one-sentence recognition and recording file recognition?
The one-sentence recognition and recording file recognition services transfer audio data over the HTTP protocol in POST method in the following two ways:
1. The audio data is Base64-encoded and carried by the HTTP message body for transfer.
2. If a URL is used for download, you can leave the body empty and enter the audio URL in the request parameters.

### In real-time speech recognition, if the audio contains multiple sentences, how do I increase the recognition accuracy?
We recommend you enable the voice activity detection (VAD) feature for audio segmentation. If the audio contains multiple sentences, VAD can detect the pauses between them and automatically divide the audio into different sentences, achieving a higher recognition accuracy.

### Does ASR support sync result call?
- Real-Time speech recognition supports sync recognition result return.
- One-Sentence recognition supports quick recognition result return.
- Recording file recognition supports two async call methods: callback and polling.

### Can ASR convert Mandarin recording files into English text?
No.

### Does ASR support evaluation?
No.

### Can I copy the text returned by ASR?
No. You need to develop the text copy feature on your frontend by yourself after connecting to ASR.

### How do I import a file for recognition after purchasing a recording file recognition resource package?
You can go to the [ASR console](https://console.cloud.tencent.com/asr) and enter the feature trial page to import a file. You can also call an API or connect to the SDK for file import.

### What file formats are supported by the recording transcription feature?
The recording transcription feature supports the following file formats: WAV, MP3, M4A, FLV, MP4, WMA, 3GP, AMR, AAC, Ogg Opus, and FLAC.

### Can I output the recording recognition result as a Word file?
Currently, only PDF files can be output.

### Can I set the longest recognition time for real-time speech recognition?
No, but you can directly stop recognition at any time.

### Does ASR support the MRCP protocol?
Currently, MRCP is not open to external businesses. If you want to use it, [contact us](https://cloud.tencent.com/online-service?from=sales&source=PRESALE) for assistance.

### Is ASR available as an SaaS service?
ASR supports private cloud deployment. If you need this, [contact us](https://cloud.tencent.com/online-service?from=sales&source=PRESALE) for assistance.
