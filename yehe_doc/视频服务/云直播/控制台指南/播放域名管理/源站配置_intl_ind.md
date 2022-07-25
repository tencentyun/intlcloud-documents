## Skenario Pengoperasian

Jika memiliki server asal dan sumber streaming langsung yang Anda buat sendiri serta ingin menyiarkan secara langsung konten Anda melalui Tencent Cloud, Anda dapat mengonfigurasikan informasi server asal untuk nama domain pemutaran ulang LVB Anda untuk origin-pull. Setelah konfigurasi berhasil, Anda dapat melakukan pull pada streaming langsung dari server asal dan mendistribusikan konten langsung melalui LVB. Dokumen ini menjelaskan caranya.

## Catatan
- Setelah konfigurasi yang diperlukan selesai, pengaturan server asal akan diterapkan dalam **30 menit**‒**satu jam**.
- Setelah konfigurasi server asal diaktifkan, berbagai fitur, seperti transcoding, perekaman, pengambilan tangkapan layar, deteksi pornografi, dan watermark tidak akan tersedia.

## Prasyarat
- Anda telah login ke [Konsol LVB](https://console.cloud.tencent.com/live).
- Anda telah membuat server asal streaming langsung.
- Anda telah menambahkan **nama domain pemutaran ulang**.

## Petunjuk
1. Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), klik **playback domain** (domain pemutaran ulang) yang akan dikonfigurasi atau **Manage** (Kelola) di sebelah kanan untuk membuka halaman detail domain.
2. Pilih **Advanced Configuration** (Konfigurasi Lanjutan) dan lihat tab **Origin Server Settings** (Pengaturan Server Asal).
3. Klik **Edit** di modul pengaturan server asal untuk mengonfigurasikan informasi server asal berikut:
 1. Aktifkan **Origin Server Settings** (Pengaturan Server Asal).
 2. Pilih **Forwarding Protocol** (Protokol Penerusan) dan centang **Playback Protocol** (Protokol Pemutaran Ulang).
 3. Masukkan **Master Origin Server Address** (Alamat Server Asal Master) (IP atau nama domain).
 4. Klik **Save** (Simpan).

>?**Forwarding Protocol** (Protokol Penerusan) adalah format yang didukung oleh LVB saat pull dilakukan pada streaming dari server asal. **Playback Protocol** (Protokol Pemutaran Ulang) adalah protokol pemutaran ulang yang digunakan untuk mendistribusikan konten langsung melalui CDN.
>- Jika FLV atau RTMP digunakan sebagai protokol penerusan, protokol pemutaran ulang dapat menggunakan FLV atau HLS.
>- Jika HLS digunakan sebagai protokol penerusan, protokol pemutaran ulang hanya dapat menggunakan HLS.
>- Untuk protokol penerusan, Anda hanya dapat memilih satu, tetapi untuk protokol pemutaran ulang, Anda dapat memilih beberapa.



![](https://main.qcloudimg.com/raw/aad1f61836b32b01822f945f8afa241e.png)

