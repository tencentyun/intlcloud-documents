Tencent Real-Time Communication (TRTC) features two major solutions: low-latency interactive live streaming and audio/video call. It has a wide variety of capabilities, such as low-latency live streaming, real-time recording, screen sharing, beauty filters, and stereo sound, and can be seamlessly connected to CDN. It is ideal for scenarios like interactive co-anchoring, cross-room communication, radio, karaoke, online class, voice chat, video chat, and online conferencing. This document describes the business scenarios covered by the two major solutions.



## Interactive Audio Live Streaming

### Audio chat room

TRTC allows up to 50 users to mic on and chat at the same time and smoothly mic on/off with a latency below 300 ms. It supports multiple audio effects such as voice changing, sound effects, and reverb, creating a rich audio chat experience. It can be integrated with Tencent Cloud IM to support various interactions such as public chat, private chat, group chat, liking, and gifting. It also provides a scenario-based voice chat room component, which can be directly reused to minimize development costs. For more information on how to use the component, see. [Audio Chat Room](https://intl.cloud.tencent.com/zh/document/product/647/37287).




### Radio

TRTC supports 48 kHz sample rate, 128 Kbps bitrate, and stereo sound, delivering clear sound that is comparable to CD quality. It can play back local music in various formats such as MP3, AAC, and WAV as the background music, allowing you to build a high-quality radio station. It offers a rich set of voice changing effects which make radio shows more entertaining. In addition, it provides a scenario-based radio component, which can be directly reused to minimize your development costs. For more information on how to use the component, see [Audio Chat Room](https://intl.cloud.tencent.com/zh/document/product/647/37287).



### Online karaoke

TRTC supports 48 kHz sample rate, 128 Kbps bitrate, and stereo sound, delivering an online karaoke experience with sound quality that is comparable to that of a recording studio. It features ultra-low latency below 300 ms, making it ideal for group singing. Multiple sync mechanisms such as message passthrough and timestamp help to ensure that the accompaniment, vocals, and lyrics are precisely synced during online karaoke. It also supports in-ear monitoring to help users carry a tune with ease.




## Interactive Video Live Streaming

### Live shows

TRTC delivers latency below 300 ms for cross-room communication and enables seamless interaction between viewers and anchors, which helps meet requirements for frequent interactions during live streamed shows. It supports smart beauty filters which make shows more attractive and allow anchors and guests to look their best. In addition, it provides a scenario-based live show streaming component, which can be directly reused to minimize your development costs. For more information on how to use the component, see [Interactive Video Streaming](https://intl.cloud.tencent.com/document/product/647/36060).



### Interactive large class

TRTC allows up to 100,000 students to watch an online class at the same time with latency below 300 ms. Teachers and students can smoothly mic on/off for uninterrupted discussion and interaction during the class. It supports various features such as screen sharing, interactive whiteboard, and recording and playback, allowing teachers to use diverse teaching aides. In addition, it provides a scenario-based interactive large class component, which can be directly reused to minimize your development costs. For more information on how to use the component, see [Real-Time Interactive Teaching](https://cloud.tencent.com/document/product/647/45465).



### Interactive small class

TRTC supports multiple small class sizes, including classes for 1, 2, 6, and 32 students, and teachers and students can interact with each other with a latency below 300 ms. It offers various features like screen sharing, courseware sharing, and interactive whiteboard, allowing teachers to use diverse teaching methods during online classes. The entire lecture can be recorded and then played back later, so students can rewatch the class and improve their learning experience.





### Mini program live streaming

TRTC supports interconnection across mini programs, applications, and PC, so live streaming content can be quickly delivered to users on different platforms. By integrating with features such as instant messaging, video-on-demand, and UGSV, it supports a diversity of features like live room on-screen commenting, liking, gifting, LVB recording, and recording playback, which improve the Mini Program live streaming experience. Moreover, it is capable of intelligently detecting porn in videos and images, and it can process non-compliant contents within seconds to help ensure content compliance and business security.




### Q&A live streaming

TRTC supports low-latency live streaming under high-concurrency, making it ideal for Q&A scenarios in which questions need to be displayed synchronously on viewer clients. It supports multiple sync mechanisms such as message passthrough, timestamp, and signaling channel so that audio, images, and questions are in sync, meeting the requirements for ultra-high-concurrence IM interaction. It also supports quiz interaction, result statistics collection, and co-anchoring in live streaming, making online Q&A more exciting. In addition, it can filter keywords and answer hints during interactive live streaming in real time, which helps improve the user experience and reduce the risks of non-compliance.




## Audio Call

### Group audio call

TRTC allows 300 users to join a group call at the same time, and up to 50 users can mic on at the same time. With a sample rate of 48 kHz, a bitrate of 128 Kbps, and integration with Tencent Cloud's 3A processing technologies, it delivers a smooth and high-quality audio call experience. In addition, it provides a scenario-based group audio call component, which can be directly reused to minimize your development costs. For more information on how to use the component, see [Audio Call](https://intl.cloud.tencent.com/document/product/647/36067).



### One-to-One audio call

With a call latency of less than 300 ms, packet loss prevention rate of over 80%, and network jitter prevention of over 1,000 ms, TRTC enables smooth and stable one-to-one audio calls even in weak network environments. Integrating with the rich variety of call signaling management APIs provided by Tencent Cloud IM makes it ideal for a wide variety of audio call scenarios. In addition, it provides a scenario-based one-to-one audio call component, which can be directly reused to minimize your development costs. For more information on how to use the component, see [Audio Call](https://intl.cloud.tencent.com/document/product/647/36067).



### Party games

With a call latency of less than 300 ms, a packet loss prevention rate of over 80%, and prevention of network jitter over 1,000 ms, TRTC guarantees smooth and stable party games even in weak network environments. It supports real-time monitoring of user network status so as to ensure an outstanding gaming experience. It can also test user audio devices to eliminate abnormal audio and further improve the gaming experience.



### Audio conferencing

TRTC supports cross-platform compatibility, enabling users to join meetings on their mobile phones, PCs, tablets, and from WeChat. With outstanding 3A processing technologies, it can eliminate echoes and howling and ensure smooth and clear conference calls. It also supports interactive whiteboard and file sharing, allowing participants to communicate more efficiently during audio conferences.




## Video Call

### Group video call

TRTC supports group video calls and provides HD image quality of 720p and 1080p. A single room can sustain up to 300 concurrent online users, and up to 50 users can turn on their videos at the same time. It has diverse features such as instant messaging, video on-demand, recording, and porn detection, making it ideal for many scenarios. In addition, it provides a scenario-based multi-person video call component, which can be directly reused to minimize the development costs. For more information on how to use the component, see [Video Call](https://intl.cloud.tencent.com/document/product/647/36065).



### One-to-One video call

TRTC supports one-to-one video calls and provides HD image quality of 720p and 1080p. It includes a range of features such as instant messaging, screen sharing, recording, and interactive whiteboard, making it ideal for many use cases. In addition, it provides a scenario-based one-to-one video call component, which can be directly reused to minimize the development costs. For more information on how to use the component, see [Video Call](https://intl.cloud.tencent.com/document/product/647/36065).



### Online conferencing

TRTC supports features such as screen sharing, file sharing, and interactive whiteboard, making online conferencing more efficient. By integrating with Tencent Cloud IM, it offers multiple discussion methods like text/image-based communications without interrupting the conferencing process. In addition, it provides a scenario-based online conferencing component, which can be directly reused to minimize the development costs. For more information on how to use the component, see [Group Audio/Video Room](https://intl.cloud.tencent.com/zh/document/product/647/37284).



### Online healthcare

TRTC supports 1080p FHD image quality and allows you to flexibly adjust the video device focus. This makes online medical diagnosis and other online healthcare services comparable to the experience of going to a real hospital. It has many convenient features such as file sharing, screen sharing, and instant messaging for medical records and image sharing, greatly improving the efficiency of diagnosis. In addition, it supports multi-person video calls, so multiple physicians can join an online diagnostic session, helping deliver better healthcare communication and collaboration for patients.



### Video customer service

With a call latency of less than 300 ms, packet loss prevention rate of over 70%, and network jitter prevention of over 1,000 ms, TRTC guarantees smooth and stable calls even in weak network environments. It enables interconnection across various platforms such as mobile apps, PC, mini programs, and web, making video customer service accessible any time, anywhere. It can record and play back video calls, which helps greatly improve the quality of customer service.



### Financial audiovisual recording

TRTC provides real-time on-cloud recording throughout the entire call. It supports recording file storage, playback, and download as well as deployment on local servers, helping ensure your business compliance. In addition, by leveraging Tencent's 21 years of experience in data security, it can guarantee data security at its best.
