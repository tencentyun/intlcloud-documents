Dengan CSS, Anda dapat melakukan push pada streaming melalui web. Anda dapat membuat URL push dengan cepat dan melakukan push pada streaming dari kamera atau layar atau melakukan push pada file lokal untuk menguji fitur CSS.

## Prasyarat
Anda telah login ke [konsol CSS](https://console.cloud.tencent.com/live).
- Anda telah menambahkan [nama domain push](https://intl.cloud.tencent.com/document/product/267/35970).
- Ada kamera yang terpasang di perangkat Anda dan browser Anda mengizinkan Flash untuk mengakses kamera tersebut.

## Petunjuk
1. Login ke konsol CSS, lalu pilih **[Web Push (Push Web)](https://console.cloud.tencent.com/live/tools/webpush)**.
2. **Pilih sumber pengambilan**, yang dapat berupa kamera, layar, atau file lokal.
<dx-tabs>
::: Kamera
Tangkap dan publikasikan audio/video dari kamera/mikrofon (yang dapat berupa perangkat periferal). Klik **Turn On** (Aktifkan) untuk **Camera**/**Mic** (Kamera/Mikrofon). Anda perlu memberikan akses browser ke kamera/mikrofon jika Anda baru melakukan tindakan ini untuk pertama kali.
![](https://qcloudimg.tencent-cloud.cn/raw/c5585e8a4ce99d65ace7af7c63e39487.png)
:::
::: Berbagi Layar
 Tangkap dan publikasikan streaming dari layar. Klik **Select Screen** (Pilih Layar) untuk memilih tab layar/jendela/browser yang akan dipublikasikan.
![](https://qcloudimg.tencent-cloud.cn/raw/75d18898089e060dc118656c539d05a3.png)
:::
::: File Lokal
Publikasikan file lokal menggunakan alat push web ke CSS. Klik **Select** (Pilih) untuk memilih file yang akan dipublikasikan. Saat ini, Anda hanya dapat memublikasikan file dalam format MP4.
![](https://qcloudimg.tencent-cloud.cn/raw/f1ae8270626dfe6cf0cbc822a907698e.png)
:::
</dx-tabs>
>! Anda tidak dapat mengubah sumber pengambilan setelah mengaktifkan pratinjau kamera atau memilih konten layar yang akan dibagikan. Untuk mengganti sumber, nonaktifkan pratinjau kamera atau batalkan berbagi layar terlebih dahulu.
3. **Konfigurasi pengambilan data**. Pengaturan default direkomendasikan, dan bervariasi berdasarkan resolusi. Anda dapat mengeklik **Edit** dan memilih **Custom** (Kustom) untuk mengatur kustomisasi pengambilan data. **Untuk kamera dan berbagi layar, pengaturan mencakup resolusi, frame rate video, dan kecepatan sampel audio, sedangkan untuk file lokal, hanya dua fitur pertama yang berlaku.**
![](https://qcloudimg.tencent-cloud.cn/raw/f126b1bf7035562517d8b6cf62c71cb0.png)
4. **Konfigurasi data push**. Pengaturan default direkomendasikan (bitrate video yang disarankan bervariasi berdasarkan resolusi, dan bitrate audio tetap). Anda dapat mengeklik **Edit** dan memilih **Custom** (Kustom) untuk mengatur kustomisasi bitrate video dan audio.
>? Push WebRTC menggunakan codec audio Opus, dan Anda sebaiknya memutar streaming yang di-push menggunakan URL WebRTC LEB. Jika Anda menggunakan protokol streaming langsung standar (RTMP, FLV, atau HLS), sistem akan secara otomatis mengonversi streaming ke AAC, yang akan dikenai biaya transcoding. Informasi mendetail dapat dilihat di [dokumen penagihan](https://intl.cloud.tencent.com/document/product/267/39604).

![](https://qcloudimg.tencent-cloud.cn/raw/bb10b3c8d970e26d45d55eec229b5fb0.png)
5. **Preview streams** (Pratinjau streaming). Setelah menyelesaikan langkah-langkah di atas, Anda dapat mengaktifkan pratinjau untuk melihat pratinjau streaming di sebelah kanan.
![](https://qcloudimg.tencent-cloud.cn/raw/efaa6ffdf3d1dac7ac6d23beac569671.png)
6. Masukkan URL push WebRTC atau klik **Generate** (Buat) dan selesaikan konfigurasi berikut:
	- Pilih domain push.
	- Masukkan `AppName` unik untuk aplikasi guna membedakannya dari aplikasi lain dengan nama domain yang sama. `AppName` diisi dengan `live` secara default.
	- Masukkan `StreamName` kustom, misalnya `test`.
	- Pilih waktu kedaluwarsa, misalnya `2021-08-28 16:16:52`.
	- Klik **Confirm** (Konfirmasi), dan URL push akan dibuat secara otomatis.
![](https://qcloudimg.tencent-cloud.cn/raw/3437d3d4e57ae021aa3e0bea3e6fc4e6.png)
7. Klik **Start Push** (Mulai Push) untuk memulai streaming. Untuk mengaktifkan/menonaktifkan video atau audio, klik ![](https://main.qcloudimg.com/raw/da098f4e5ab01021e3c4704b0de41240.png) atau ![](https://main.qcloudimg.com/raw/aa8d8d4c9c32359a249de37ed0d723be.png). Setelah Anda menonaktifkan video/audio, pengambilan data akan dilanjutkan dan push akan tetap berhasil, tetapi pratinjau streaming tidak dapat ditampilkan dan streaming tidak akan memiliki video atau audio.
>? Anda tidak dapat mengaktifkan atau menonaktifkan pratinjau setelah push berhasil, dan Anda mungkin dikenai biaya bandwidth/lalu lintas atau biaya layanan bernilai tambah lain untuk melakukan push pada streaming.

![](https://qcloudimg.tencent-cloud.cn/raw/f8e3e7571205090d9ad14a4faa280125.png)
8. Setelah push berhasil, klik **View** (Lihat) di bawah pratinjau untuk melihat statistik streaming. Anda tidak bisa mendapatkan statistik atau URL pemutaran ulang untuk URL push yang tidak ada di akun Anda. Harap gunakan domain push yang ada di akun Anda untuk membuat URL push atau streaming relai ke akun Anda.

![](https://qcloudimg.tencent-cloud.cn/raw/5ef686d9d9cb0355a8e4a5686cbcaee3.png)
9. Jika sudah menambahkan domain pemutaran ulang di **Domain Management** (Manajemen Domain), Anda dapat **memilih domain** untuk membuat URL pemutaran ulang. Untuk membuat URL streaming yang di-transcoding, Anda harus mengikatkan domain pemutaran ulang dengan templat transcoding terlebih dahulu.

![](https://qcloudimg.tencent-cloud.cn/raw/94d9969c54c3c0524e1c69f9dbf56d8d.png)
URL pemutaran ulang terdiri dari empat bagian, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/9094e537a4ae7cecc7feb9c88fb83a55.png)Protokol yang didukung meliputi RTMP, FLV, HLS, dan UDP. Anda juga dapat mengeklik ikon kode QR dan memindai kode QR menggunakan [aplikasi TCToolkit](https://intl.cloud.tencent.com/document/product/1071/38147) untuk mendapatkan URL pemutaran ulang.
![](https://qcloudimg.tencent-cloud.cn/raw/9aa53207e02123a5fa7a4afae1d07724.png)

>! Jika HTTPS diaktifkan untuk domain pemutaran ulang yang dipilih, URL FLV dan HLS yang dibuat akan dimulai dengan https.

