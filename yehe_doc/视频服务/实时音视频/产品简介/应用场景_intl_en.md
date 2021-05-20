Tencent Real-Time Communication (TRTC) features two major solutions: low-latency interactive live streaming and audio/video call. It has a wide variety of capabilities, such as low-latency live streaming, real-time recording, screen sharing, beauty filters, and stereo sound, and can be seamlessly connected to CDN. It is ideal for business scenarios like interactive co-anchoring, cross-room competition, radio, karaoke, small/big online class, voice chat, video chat, and online conferencing. This document describes the business scenarios covered by the two major solutions.



## Interactive Audio Live Streaming

### Voice chat room

TRTC allows up to 50 users to mic on and chat at the same time and smoothly mic on/off with a latency below 300 ms, and supports multiple audio effects such as voice changing, ambient sound effects, and reverb, enriching and diversifying the voice chat experience. It can be integrated with Tencent Cloud IM to support various message interaction methods such as public chat, private chat, group chat, liking, and gifting, delivering an excellent interactive chat experience. In addition, it provides a scenario-based voice chat room component, which can be directly reused to minimize the development costs. For more information on how to use the component, please see [Voice Chat Room](https://intl.cloud.tencent.com/zh/document/product/647/37287).




### Radio

TRTC supports 48 kHz sample rate, 128 Kbps bitrate, and stereo sound, delivering an authentic sound experience comparable to CD. It can play back local music in various formats such as MP3, AAC, and WAV as the background music, allowing you to easily build a high-quality radio station. It offers a rich set of voice changing effects like middle-aged man and little girl, making the radio more entertaining. In addition, it provides a scenario-based radio component, which can be directly reused to minimize the development costs. For more information on how to use the component, please see [Voice Chat Room](https://intl.cloud.tencent.com/zh/document/product/647/37287).



### Online karaoke

TRTC supports 48 kHz sample rate, 128 Kbps bitrate, and stereo sound, delivering a smooth online karaoke experience comparable to recording studio. It features an ultra-low latency below 300 ms, making it ideal for multi-person singing. It provides multiple sync mechanisms such as message passthrough and timestamp, helping precisely align the accompaniment, vocal, and lyrics during online karaoke. It also supports in-ear monitoring to help users carry a tune with ease.




## Interactive Video Live Streaming

### Show live streaming

TRTC delivers a latency below 300 ms for cross-room co-anchoring competition and enables viewers to co-anchor with the anchor and mic-on/off smoothly, which help meet the frequent interaction needs in show live streaming scenarios. It supports smart beauty filters, making the show more charming. In addition, it provides a scenario-based show live streaming component, which can be directly reused to minimize the development costs. For more information on how to use the component, please see [Video Interactive Live Streaming](https://intl.cloud.tencent.com/document/product/647/36060).



### Interactive big class

TRTC allows 100,000 students to watch at the same time with a latency below 300 ms and enables teacher-student co-anchoring and smooth mic-on/off for a favorable class interaction experience. It supports various class application features such as screen sharing, interactive whiteboard, and recording and playback, enriching and diversifying teaching methods in interactive online big classes. In addition, it provides a scenario-based interactive big class component, which can be directly reused to minimize the development costs. For more information on how to use the component, please see [Real-Time Interactive Teaching](https://cloud.tencent.com/document/product/647/45465).



### Interactive small class

TRTC supports interactive small classes in multiple sizes such as **1-to-1**, **1-to-2**, **1-to-6**, and **1-to-32**, where the teacher can interact with students with a latency below 300 ms, delivering a smoother teaching experience. It offers various class application features like screen sharing, courseware sharing, and interactive whiteboard, enriching and diversifying the online teaching methods. The entire lecture can be recorded and then played back on demand later, helping enhance the learning results.





### Mini Program live streaming

TRTC supports interconnection across Mini Program, application, and PC, so the live streaming content can be quickly delivered to users on different platforms. By integrating with features such as instant messaging, video on-demand, and UGSV, it supports a diversity of features like live room on-screen commenting, liking, gifting, LVB recording, and recording playback, which improve the Mini Program live streaming experience. Moreover, it is capable of intelligently detecting porn in videos and images, which can process non-compliant contents within seconds and ensure content compliance and business security.




### Q&A live streaming

TRTC supports low-latency live streaming under high concurrence, which minimizes the viewers' watch latency and is suitable for displaying questions synchronously on viewer clients. It supports multiple sync mechanisms such as message passthrough, timestamp, and signaling channel so as to precisely display the audio, images, and questions in sync, meeting the ultra-high-concurrence IM interaction needs. It also supports quiz interaction, result statistics collection, and co-anchoring in live streaming, making online Q&A more interesting. Plus, it can filter keywords and answer hints during interactive live streaming in real time, which helps improve the user experience and reduce the risks of business non-compliance.




## Audio Call

### Multi-person audio call

TRTC allows 300 users to call at the same time and up to 50 of them to mic on at the same time. With a sample rate of 48 kHz, a bitrate of 128 Kbps, and integration with Tencent Cloud's outstanding 3A processing technologies, it can deliver a smooth and high-quality audio call experience. In addition, it provides a scenario-based multi-person audio call component, which can be directly reused to minimize the development costs. For more information on how to use the component, please see [Real-Time Audio Call](https://intl.cloud.tencent.com/document/product/647/36067).



### One-to-One audio call

With a call latency of less than 300 ms, packet loss prevention rate of over 80%, and network jitter prevention of over 1,000 ms, TRTC can deliver a smooth and stable one-to-one audio call experience even in weak network environments. By integrating with the rich variety of call signaling management APIs provided by Tencent Cloud IM, it is ideal for various audio call scenarios. In addition, it provides a scenario-based one-to-one audio call component, which can be directly reused to minimize the development costs. For more information on how to use the component, please see [Real-Time Audio Call](https://intl.cloud.tencent.com/document/product/647/36067).



### Werewolf

With a call latency of less than 300 ms, packet loss prevention rate of over 80%, and network jitter prevention of over 1,000 ms, TRTC guarantees smooth and stable werewolf gameplay even in weak network environments. It supports real-time monitoring of user network status in so as to ensure an outstanding gaming experience. Plus, it can test user audio devices to eliminate exceptional muting and further improve the gaming experience.



### Audio conferencing

TRTC supports cross-platform compatibility, enabling users to flexibly join meetings on mobile phones, PCs, tablets, and WeChat. By leveraging its outstanding 3A processing technologies, it can eliminate echoes and howling, ensuring smooth and clear conferencing. It also supports interactive whiteboard and file sharing, making communication in audio conferencing more efficient.




## Video Call

### Multi-person video call

TRTC supports multi-person video call and provides HD image quality of 720p and 1080p, with one single room able to sustain up to 300 concurrent online users and allow 50 users to enable video at the same time. It has diverse features such as instant messaging, video on-demand, recording, and porn detection, making it ideal for a lot of use cases. In addition, it provides a scenario-based multi-person video call component, which can be directly reused to minimize the development costs. For more information on how to use the component, please see [Real-Time Video Call](https://intl.cloud.tencent.com/document/product/647/36065).



### One-to-One video call

TRTC supports one-to-one video call and provides HD image quality of 720p and 1080p, delivering a high-quality video call service. It has diverse features such as instant messaging, screen sharing, recording, and interactive whiteboard, making it ideal for a lot of use cases. In addition, it provides a scenario-based one-to-one video call component, which can be directly reused to minimize the development costs. For more information on how to use the component, please see [Real-Time Video Call](https://intl.cloud.tencent.com/document/product/647/36065).



### Online conferencing

TRTC supports conferencing application features such as screen sharing, file sharing, and interactive whiteboard, making online conferencing more efficient. By integrating with Tencent Cloud IM, it offers multiple discussion methods like text/image-based communications without interrupting the conferencing process. In addition, it provides a scenario-based online conferencing component, which can be directly reused to minimize the development costs. For more information on how to use the component, please see [Video Conferencing](https://intl.cloud.tencent.com/zh/document/product/647/37284).



### Online healthcare

TRTC supports 1080p FHD image quality and allows you to flexibly adjust the video device focus, which is highly comparable to the medical diagnosis experience in hospitals. It has a lot of convenient features such as file sharing, screen sharing, and instant messaging for medical record and image sharing, greatly improving the diagnosis efficiency. Moreover, it supports multi-person video call, where multiple physicians and patients can join an online diagnosis session, helping deliver a smooth healthcare communication and collaboration experience.



### Video customer service

With a call latency of less than 300 ms, packet loss prevention rate of over 70%, and network jitter prevention of over 1,000 ms, TRTC guarantees smooth and stable call communication even in weak network environments. It enables interconnection across various platforms such as mobile application, PC, Mini Program, and web, making the video customer service accessible any time, any where. Plus, it can record and play back the video service process, which helps greatly improve the service quality.



### Financial audiovisual recording

TRTC provides a real-time on-cloud recording feature throughout the entire call that supports recording file storage, playback, and download as well as deployment on local servers, helping ensure your business compliance. In addition, by leveraging Tencent's 21 years of experience in data security, it can guarantee data security at its best.

