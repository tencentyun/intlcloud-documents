CSS menyediakan LVB sebagai layanan streaming cloud yang profesional, stabil, dan cepat untuk kasus penggunaan umum. Anda dapat mengintegrasikan [SDK MLVB](https://intl.cloud.tencent.com/document/product/1071) ke berbagai aplikasi, web, dan platform lain untuk mengaktifkan streaming langsung dengan cepat.

[](id:app)

## Aplikasi	
Anda dapat mengintegrasikan SDK MLVB dengan berbagai aplikasi di klien iOS atau Android untuk push dan pemutaran ulang langsung.

- **Live push on apps** (Push langsung di aplikasi): mendukung pengambilan tangkapan layar kamera atau ponsel, dan kemudian melakukan push pada konten ke platform CSS menggunakan protokol RTMP. Untuk informasi selengkapnya, silakan pelajari [Publishing (Camera) (Penerbitan (Kamera))](https://intl.cloud.tencent.com/document/product/1071/38157) dan [Publishing (Screen Recording) (Penerbitan (Perekaman Layar))](https://intl.cloud.tencent.com/document/product/1071/41878).
- **Live playback on apps** (Pemutaran ulang langsung di aplikasi): mendukung protokol pemutaran ulang, termasuk RTMP, HTTP-FLV, dan HLS. Anda dapat mengintegrasikan SDK MLVB dengan LVB untuk membuat aplikasi streaming langsung dengan cepat. Untuk informasi selengkapnya, silakan pelajari [Playback (Pemutaran Ulang)](https://intl.cloud.tencent.com/document/product/1071/38159).

>? SDK MLVB menggunakan CSS, IM, TRTC, dan layanan lainnya untuk komunikasi audiovisual latensi rendah untuk banyak pihak. SDK MLVB menawarkan co-anchoring untuk interaksi antara pemirsa, dan pemirsa lain yang tidak bergabung dengan co-anchoring juga dapat menonton streaming langsung. Untuk informasi selengkapnya, silakan pelajari [Co-anchoring](https://intl.cloud.tencent.com/document/product/1071/39888).



[](id:web)

## Web
Anda dapat menggunakan cara berikut untuk mencapai push dan pemutaran ulang langsung di situs web Anda:
- **Live push on web** (Push langsung di web): Anda dapat menggunakan protokol WebRTC standar untuk merancang dan melakukan mux pada streaming, serta menyisipkan potongan kode ke situs web untuk mengaktifkan push langsung. Informasi mendetail dapat dilihat di [WebRTC Push (Push WebRTC)](https://intl.cloud.tencent.com/document/product/267/41620).
> ! Push WebRTC menggunakan codec audio Opus. Jika Anda menggunakan protokol streaming langsung standar (RTMP, HTTP-FLV, atau HLS) untuk pemutaran ulang, backend CSS akan secara otomatis mengonversi streaming audio ke format AAC untuk memastikan pemutaran ulang berjalan normal, dan konversi otomatis ini akan dikenai biaya transcoding audio. Informasi selengkapnya dapat dilihat di [Live Transcoding > Audio Transcoding](https://intl.cloud.tencent.com/document/product/267/39604) (Transcoding Langsung > Transcoding Audio).


