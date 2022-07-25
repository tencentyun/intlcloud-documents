## Ikhtisar
Open Broadcaster Software (OBS) adalah alat sumber terbuka pihak ketiga untuk streaming langsung. Alat ini praktis dan gratis serta mendukung OS X, Windows, dan Linux. OBS dapat digunakan di berbagai skenario untuk memenuhi sebagian besar kebutuhan streaming langsung tanpa penggunaan plugin tambahan. Anda dapat mengunduh versi terbaru di [situs web OBS](https://obsproject.com/download?spm=a2c4g.11186623.2.15.6aac1445JPlKR8).

## Prasyarat
- Anda telah menginstal [OBS Studio](https://obsproject.com/download?spm=a2c4g.11186623.2.15.6aac1445JPlKR8).
- Anda telah mengaktifkan [CSS](https://console.cloud.tencent.com/live) dan [menambahkan domain pemutaran ulang](https://intl.cloud.tencent.com/document/product/267/35970) dengan nomor izin ICP di konsol (untuk push, Anda dapat menggunakan domain default yang kami sediakan atau menambahkan domain Anda sendiri).

[](id:step0)
## Mendapatkan URL Push
1. Login ke konsol CSS, klik **[Address Generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator)** (Pembuat Alamat) di bilah sisi kiri, lalu ikuti langkah-langkah berikut:
   1. Pilih *Push Domain** (Domain Push) untuk **Domain Type** (Jenis Domain).
   2. Pilih nama domain yang telah Anda tambahkan di **Domain Management** (Manajemen Domain).
   3. Masukkan nama aplikasi (`AppName`), yang digunakan untuk membedakan aplikasi yang berada di domain yang sama. Nilai defaultnya adalah `live`.
   4. Masukkan nama streaming kustom (`StreamName`), misalnya `live`.
   5. Pilih waktu kedaluwarsa alamat, misalnya `2020-06-09 23:59:59`.
2. Klik **Generate Address** (Buat Alamat) untuk mendapatkan URL push OBS.


[](id:normal)
## Mengonfigurasi OBS untuk Push
### Langkah 1. Mengonfigurasi URL push[](id:step1)
1. Buka OBS dan klik **Control** > **Settings** (Kontrol > Pengaturan) di bagian bawah untuk masuk ke halaman pengaturan.
![](https://main.qcloudimg.com/raw/493a19e0f2bbea80983c341dd742a044.png)
2. Klik **Stream** (Streaming) dan pilih **Custom** (Kustom) untuk **Service** (Layanan).
3. Isilah bidang **Server** dan **Stream Key** (Kunci Streaming) dengan informasi yang diperoleh di langkah [Mendapatkan URL Push](#step0).
    - Server: Masukkan alamat push OBS (`rtmp://domain/AppName/`).
    - Kunci streaming: Masukkan nama push OBS (`StreamName?txSecret=xxxxx&txTime=5C1E5F7F`).
![](https://main.qcloudimg.com/raw/55512ddf58bf32014424fa33b6f3d31f.png)
4. Klik **OK** (Oke) untuk menyimpan informasi.

### Langkah 2. Mengonfigurasi sumber[](id:step2)
>? Untuk bitrate, perekaman, dan pengaturan lainnya, klik **Tools > Auto-Configuration Wizard** (Alat > Wizard Konfigurasi Otomatis) di bilah menu atas, lalu ikuti petunjuk yang diberikan oleh OBS untuk menyelesaikan pengaturan.

1. Temukan **Sources** (Sumber) di bilah menu di bagian bawah.
![](https://main.qcloudimg.com/raw/f8136fdb794595c8c491c995a74cdfcc.png)
2. Klik **+** dan pilih sumber yang sesuai dengan kebutuhan Anda, misalnya **Display Capture** (Pengambilan Tangkapan Tampilan).
 ![](https://main.qcloudimg.com/raw/f8136fdb794595c8c491c995a74cdfcc.png)
**Sumber streaming langsung umum**
<table>
<thead><tr><th width="20%">Source</th><th>Deskripsi</th></tr></thead>
<tbody><tr>
<td>Gambar</td>
<td>Menerbitkan gambar tunggal</td>
</tr><tr><td>Tayangan Slide Gambar</td>
<td>Menerbitkan beberapa gambar (Anda dapat menentukan urutan pemutaran ulang dan diterapkan atau tidaknya pengulangan pemutaran ulang)</td>
</tr><tr><td>Adegan</td>
<td>Penyisipan adegan secara utuh sebagai sumber untuk mengaktifkan berbagai efek streaming</td>
</tr><tr><td>Sumber Media</td>
<td>Menerbitkan file lokal</td>
</tr><tr><td>Teks</td>
<td>Menambahkan teks real-time ke streaming</td>
</tr><tr><td>Pengambilan Tangkapan Tampilan</td>
<td>Menangkap dan menerbitkan layar secara real-time</td>
</tr><tr><td>Pengambilan Tangkapan Game</td>
<td>Streaming game dari sumber tertentu secara real-time</td>
</tr><tr><td>Pengambilan Tangkapan Jendela</td>
<td>Menangkap dan menerbitkan jendela yang Anda pilih secara real-time</td>
</tr><tr><td>Sumber Warna</td>
<td>Menambahkan warna yang kuat ke adegan Anda. Anda dapat menggunakan sumber ini untuk warna latar belakang atau gradasi warna global menggunakan saluran alfa.</td>
</tr><tr><td>Perangkat Pengambilan Tangkapan Video</td>
<td>Menangkap dan menerbitkan gambar yang ditangkap kamera secara real-time</td>
</tr><tr><td>Pengambilan Tangkapan Input Audio</td>
<td>Streaming langsung audio (perangkat input audio)</td>
</tr><tr><td>Pengambilan Tangkapan Output Audio</td>
<td>Streaming langsung audio (perangkat output audio)</td>
</tr>
</tbody></table>

### Langkah 3. Menggunakan mode studio[](id:step3)
Dalam mode studio, Anda dapat mengedit streaming langsung yang sedang berjalan secara real-time dan mengonfigurasikan transisi untuk pertukaran adegan sehingga meminimalkan dampak terhadap pengalaman pengguna.
1. Klik **Controls > Studio Mode** (Kontrol > Mode Studio) di bilah menu di bagian bawah.
2. Setelah pengeditan selesai, klik **Transition** (Transisi) untuk menukar hasil pengeditan dan tayangan langsung.
![](https://main.qcloudimg.com/raw/80e9e902e0e02902d78779ca5505b2f8.png)

### Langkah 4. Memulai streaming[](id:step4)
1. Temukan **Controls** (Kontrol) di bilah menu di bagian bawah.
2. Klik **Start Streaming** (Mulai Streaming) untuk melakukan push pada video Anda ke URL push terkonfigurasi.
![](https://main.qcloudimg.com/raw/80e9e902e0e02902d78779ca5505b2f8.png)

>? 
>- Jika Anda melihat ![](https://main.qcloudimg.com/raw/a10bafc9eb0895dc4c6b542b61217253.png) di bagian bawah, push berhasil.
>- Untuk menghentikan streaming, klik **Stop Streaming** (Hentikan Streaming).

## Pengaturan Push Lainnya
### Latensi Streaming
1. Buka **Controls > Settings > Output** (Kontrol > Pengaturan > Output).
2. Pilih **Advanced** (Lanjutan) untuk **Output Mode** (Mode Output) untuk mengatur parameter, termasuk **Keyframe Interval** (Interval Keyframe).
![](https://main.qcloudimg.com/raw/5f48205da162f1230723729c36369f65.png)
3. Klik **Advanced** (Lanjutan) di bilah sisi kiri untuk mengatur **Stream Delay** (Penundaan Streaming):
![](https://main.qcloudimg.com/raw/c3ec9a71a014548eb680009d9798b1ac.png)

### Perekaman langsung lokal
Untuk merekam streaming langsung ke penyimpanan lokal Anda, ikuti langkah-langkah berikut:
1. Buka **Controls > Settings > Output** (Kontrol > Pengaturan > Output).
2. Selesaikan pengaturan di bagian **Recording** (Perekaman), lalu klik **OK** (Oke).
![](https://main.qcloudimg.com/raw/008e1ab02e2d08ee42f3a64e2e09d473.png)
3. Klik **Video** di bilah sisi kiri untuk mengatur resolusi dan frame rate.
>? Resolusi menentukan kejelasan video yang ditampilkan kepada pemirsa. Makin tinggi resolusi, makin jelas video. Frame rate (frame per detik) menentukan kelancaran pemutaran ulang. Frame rate normal berada di kisaran 24 fps hingga 30 fps. Pemutaran ulang bisa macet jika frame rate kurang dari 16 fps. Game video membutuhkan frame rate lebih tinggi dan cenderung macet jika frame rate di bawah 30 fps.

![](https://main.qcloudimg.com/raw/f736ef195b26a81f46d1e26d7935a763.png)

### Transcoding
Untuk mengubah bitrate video selama streaming, ikuti langkah-langkah berikut:
1. Klik **Controls > Settings** (Kontrol > Pengaturan) di bilah menu di bagian bawah.
2. Klik **Output** di bilah sisi kiri, lalu pilih **Simple** (Sederhana) untuk **Output Mode** (Mode Output).
3. Masukkan bitrate yang ingin Anda gunakan, lalu klik **OK** (Oke).
![](https://main.qcloudimg.com/raw/008e1ab02e2d08ee42f3a64e2e09d473.png)




## Informasi Lainnya
### Push hanya-audio
Menurut OBS Forums, OBS Studio 23.2.1 dan versi sebelumnya tidak mendukung streaming hanya-audio.
Anda dapat mengikuti langkah-langkah berikut untuk menerapkan fitur serupa. Metode ini menggunakan kanvas statis (layar kosong atau gambar) untuk konten video. Artinya, data video akan tetap ada di streaming langsung. Untuk mengurangi penggunaan bandwidth, Anda dapat mengatur frame rate dan bitrate video ke nilai minimum.
1. Sesuai dengan petunjuk di [Mengonfigurasikan sumber](#step2), pilih **Audio Input Capture** (Tangkapan Input Audio) sebagai sumber. Jangan gunakan sumber video atau gambar.

2. Buka **Controls > Settings > Video** (Kontrol > Pengaturan > Video).
3. Atur **Base (Canvas) Resolution** (Resolusi (Kanvas) Dasar) dan **Common FPS Values** (Nilai FPS Umum) ke nilai minimum, lalu klik **OK** (Oke).
    ![](https://main.qcloudimg.com/raw/cb77c3deb8d3e9831aaa1421b5b13412.png)
4. Klik **Output** di bilah sisi kiri, konfigurasikan output seperti ditampilkan di bawah ini (atur **Bitrate** ke nilai minimum), lalu klik **OK** (Oke).
    ![](https://main.qcloudimg.com/raw/008e1ab02e2d08ee42f3a64e2e09d473.png)
5. Mulai streaming sesuai dengan instruksi di [Mengonfigurasikan OBS untuk Push](#normal). Pemirsa akan mendengar audio, sedangkan video akan menampilkan layar kosong atau sebuah gambar. Karena bitrate video diatur ke nilai minimum, penggunaan bandwidth menjadi jauh lebih rendah daripada penggunaan push video.

### Pengulangan video
- **Mengulang file tunggal**
    1. Klik **+** di **Sources** (Sumber) dan pilih **Media Source** (Sumber Media). Di jendela pop-up, pilih file lokal yang akan di-streaming, pilih **Loop** (Ulang), lalu klik **OK** (Oke).
    ![](https://main.qcloudimg.com/raw/b41371c6674d4d8a2cd84fe37e3fbab4.png)
    2. Atur **Server** dan **Stream Key** (Kunci Streaming) sesuai dengan petunjuk di langkah [Mengonfigurasi URL push)](#step1).


Anda dapat menggunakan metode berikut untuk memeriksa berhasil atau tidaknya push:
- PC: Gunakan [VLC](https://intl.cloud.tencent.com/document/product/267/32483) untuk memutar streaming.
- Perangkat Seluler: Gunakan SDK [MLVB](https://intl.cloud.tencent.com/zh/document/product/1071) untuk memutar streaming.
>? Mobile Live Video Broadcasting (MLVB) memperluas layanan CSS ke perangkat seluler. MLVB tidak hanya menawarkan SDK RTMP yang mendukung integrasi cepat, tetapi juga menghadirkan solusi multi-cloud lengkap di satu tempat yang mengintegrasikan berbagai layanan Tencent Cloud, termasuk LVB, LEB, VOD, IM, dan COS.
[Live Event Broadcasting (LEB)](https://intl.cloud.tencent.com/document/product/1071/41875) merupakan LVB versi latensi ultra-rendah. LEB memberikan pengalaman pemutaran ulang terbaik dengan latensi milidetik dan cocok untuk berbagai skenario dengan kebutuhan yang tinggi terhadap latensi, misalnya kegiatan pembelajaran online, streaming pertandingan olahraga, dan kuis online.





