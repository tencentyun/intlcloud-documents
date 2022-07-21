Sebagai versi LVB dengan latensi lebih rendah, LEB memberikan pengalaman streaming langsung yang sangat baik dengan latensi pemutaran ulang milidetik, jauh lebih rendah daripada latensi pemutaran ulang streaming langsung menggunakan protokol pada umumnya. LEB dirancang untuk skenario dengan kebutuhan latensi tinggi. Selain siaran langsung belanja dan kegiatan pembelajaran online, LEB juga cocok untuk skenario interaktif, seperti streaming pertandingan olahraga langsung dan streaming game langsung.

## Perbandingan Protokol

Protokol pemutaran ulang yang umum digunakan oleh LVB meliputi RTMP, HTTP-FLV, dan HLS, yang semuanya berbasis TCP. Pada penggunaan TCP, karena konfirmasi dan dukungan yang tertunda, konfirmasi tidak langsung dikirim setelah data diterima, tetapi hanya akan dikirim setelah data terakumulasi hingga mencapai ukuran tertentu. Hal ini mengakibatkan latensi yang terasa dengan jelas. Dalam kondisi jaringan yang buruk, mekanisme ini akan menyebabkan penumpukan data yang mengakibatkan kemacetan pada transfer data dan latensi selama beberapa atau puluhan detik.
![](https://qcloudimg.tencent-cloud.cn/raw/911be7d33fbffa34a92b68111810f5d8.png)

Layanan streaming langsung latensi rendah di industri ini menggunakan protokol, seperti QUIC, SRT, WebRTC, dan ORTC. Di antara protokol ini, QUIC memiliki latensi relatif tinggi karena tidak memiliki karakteristik media streaming. SRT, WebRTC, dan ORTC memiliki karakteristik media streaming dan dapat melakukan streaming dengan latensi milidetik, tetapi WebRTC lebih banyak digunakan dibandingkan dengan SRT dan ORTC. Oleh karena itu, LEB menggunakan WebRTC berbasis UDP untuk menerapkan streaming langsung dengan latensi rendah.
![](https://qcloudimg.tencent-cloud.cn/raw/19ee08b715b3a3e7198881e81f2ea9dd.png)

## Perbandingan Latensi
Untuk LVB, HTTP-FLV umumnya memiliki latensi 2‒10 detik, yang disebabkan terutama oleh ukuran GOP yang besar dan penumpukan data dalam kondisi jaringan yang buruk. Latensi HLS lebih tinggi, biasanya beberapa hingga puluhan detik, dan disebabkan oleh ukuran GOP yang besar dan segmen TS yang besar. HLS bekerja dengan mengunduh potongan data dan menghasilkan file indeks sehingga latensinya dipengaruhi oleh ukuran segmen TS. Banyak pemutar menunggu hingga 3 segmen TS diterima sebelum melakukan pemutaran ulang, yang dapat mengakibatkan latensi puluhan detik. HLS memiliki latensi tertinggi di antara protokol yang digunakan oleh LVB.

LEB menggunakan WebRTC untuk mencapai latensi rendah. Sebagian besar browser yang banyak digunakan, misalnya Chrome dan Safari, telah mendukung WebRTC sehingga kami dapat menawarkan berbagai fungsi WebRTC standar melalui browser. Selain itu, SDK WebRTC sumber terbuka yang andal membuat pengoptimalan dan penyesuaian menjadi mudah sehingga penyesuaian SDK dengan peningkatan pada fitur streaming latensi rendah dapat dilakukan. LEB umumnya memiliki latensi 300‒1.000 milidetik.
![](https://qcloudimg.tencent-cloud.cn/raw/195c8b28f1fc63240f12c1e60f1a1dbe.png)

## Keunggulan LEB

- Lebih dari 2.100 node akselerasi di seluruh dunia, yang mencakup 25 negara/wilayah
- Bandwidth ultra-tinggi (mendukung bandwidth lebih dari 100 Tbps)
- Kualitas tinggi (toleransi kehilangan paket 30%), biaya rendah, serta fitur beragam dan lengkap
- Integrasi mudah dan kompatibilitas tinggi (Anda hanya perlu memodifikasi SDK pemutaran ulang untuk dapat menggunakan serangkaian fitur lengkap)
- Streaming instan dan latensi ultra-rendah. Seperti yang ditunjukkan oleh pengujian di bawah ini, LEB dapat mempertahankan latensi agar tetap sekitar 300 milidetik atau bahkan berkurang hingga paling rendah 43 milidetik.

 ![](https://qcloudimg.tencent-cloud.cn/raw/9a8eb2a10290a8b51e93862a5eb55935.png)
