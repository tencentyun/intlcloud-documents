<span id="que1"></span>
### Bagaimana cara kerja perekaman langsung?
![img](https://main.qcloudimg.com/raw/9c9d31c6ffec97d2b8b4042b7a673cbc.jpg)

Ketika mengaktifkan perekaman untuk streaming langsung, data audio/video akan direlai ke sistem perekaman. Setiap frame yang di-push dari telepon seluler host akan ditulis ke dalam file rekaman oleh sistem perekaman.

Jika push langsung terganggu, lapisan akses akan langsung memberi tahu server perekaman untuk merekam file yang sedang ditulis, menyimpannya ke sistem VOD, dan membuat indeks. Setelah itu, Anda dapat menemukan file rekaman baru di sistem VOD. Jika Anda sudah mengonfigurasikan pemberitahuan peristiwa perekaman di server, sistem perekaman akan mengirimkan **ID indeks** dan **URL pemutaran ulang online** ke server.

Namun, kesalahan akan terjadi dalam proses transfer dan pemrosesan file berukuran besar di cloud. Agar proses tersebut berhasil, sebuah file tidak boleh memiliki durasi lebih dari 120 menit. Anda dapat menentukan segmen yang lebih singkat menggunakan parameter `RecordInterval`.

<span id="que2"></span>
### Mengapa perekaman langsung tidak tersedia? 
Perekaman dan pemutaran ulang langsung dirancang di layanan **VOD** Tencent Cloud. Untuk menggunakan fitur ini, Anda perlu [mengaktifkan VOD](https://console.cloud.tencent.com/vod) di konsol Tencent Cloud.

<span id="que3"></span>
### Berapa lama file rekaman akan siap setelah streaming langsung berakhir? 
Anda dapat memperoleh file rekaman sekitar 5 menit setelah streaming langsung berakhir. Panggilan balik peristiwa akan terpicu ketika perekaman berakhir, yang memberikan waktu penyelesaian perekaman yang akurat. Informasi selengkapnya dapat dilihat di [Callback Configuration (Konfigurasi Callback)](https://intl.cloud.tencent.com/document/product/267/31074).

<span id="que4"></span>
### Setelah perekaman langsung selesai, bagaimana cara mendapatkan file rekaman?
File rekaman yang dihasilkan disimpan secara otomatis di sistem VOD. Setelah mengaktifkan VOD, Anda bisa mendapatkan file rekaman dengan cara berikut:
- [VOD console (Konsol VOD)](https://intl.cloud.tencent.com/document/product/267/31563#vod-console)
- [Recording event notification (Pemberitahuan peristiwa perekaman)](https://intl.cloud.tencent.com/document/product/267/31563#recording-event-notification)
- [VOD API (API VOD)](https://intl.cloud.tencent.com/document/product/267/31563#vod-api-query)

<span id="que5"></span>
### Apakah migrasi dapat dilakukan pada video CSS?
Anda dapat menggunakan alamat pengunduhan video untuk melakukan migrasi video. 

<span id="que6"></span>
### Bagaimana cara mengatur periode penyimpanan video?
Saat ini CSS tidak membatasi periode penyimpanan video. Anda dapat mengelola file video melalui konsol dan API RSETful. 

<span id="que7"></span>
### Berapa jumlah file rekaman yang dihasilkan dalam satu kali proses perekaman langsung?
- **Merekam file dalam format MP4, FLV, atau AAC**: durasi perekaman maksimum untuk satu file bervariasi mulai dari 5 menit hingga 20 menit. Anda dapat menentukan segmen yang lebih singkat menggunakan parameter `RecordIntervall` [API CreateLiveRecordTemplate](https://intl.cloud.tencent.com/document/product/267/30845).
	- Jika durasi streaming langsung terlalu singkat sehingga push berakhir sebelum perekaman diaktifkan, tidak ada file rekaman yang akan dibuat.
	- Jika streaming langsung berdurasi singkat (lebih singkat daripada `RecordInterval`) dan push tidak terganggu selama streaming langsung, hanya satu file rekaman yang akan dibuat.
	- Jika durasi streaming langsung sangat lama (lebih lama daripada `RecordInterval`), video akan dibagi menjadi beberapa segmen berdasarkan durasi waktu yang ditentukan oleh `RecordInterval`, untuk menghindari ketidakpastian waktu aliran file yang berdurasi lebih lama dalam sistem terdistribusi.
	- Jika push terganggu selama streaming langsung (SDK akan melakukan push ulang pada waktu lain), segmen baru akan dibuat setiap kali gangguan terjadi.

- **Merekam file dalam format HLS**: tidak ada batas atas. Jika file melampaui periode waktu habis mulai ulang perekaman, file baru akan dibuat untuk melanjutkan perekaman. Anda dapat mengatur periode waktu habis mulai ulang perekaman ke 0‒1800 detik.

<span id="que9"></span>
### Bagaimana cara menyambungkan segmen?
Anda dapat menyambungkan segmen menggunakan API TencentCloud. 

<span id="que10"></span>
### Bagaimana cara mengatasi masalah jika hanya satu templat perekaman yang diatur, tetapi ada dua streaming perekaman? 
Secara umum, hal ini mungkin terjadi karena terdapat dua tugas perekaman di nama domain push saat ini. Anda sebaiknya mengatasi masalah dengan cara berikut:

1. Periksa konfigurasi perekaman di konsol. Pastikan hanya satu format yang dipilih sebagai jenis file rekaman.
   -Jika Anda menggunakan konsol baru, buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), klik **Manage** (Kelola) di sebelah kanan nama domain push yang diinginkan, pilih **Template Configuration** (Konfigurasi Templat), lalu lihat "Recording Format" (Format Rekaman) templat yang terkait di bagian **Recording Configuration** (Konfigurasi Perekaman).
2. Anda dapat menggunakan salah satu metode berikut untuk merekam: [membuat tugas perekaman](https://intl.cloud.tencent.com/document/product/267/30847) atau [membuat templat perekaman](https://intl.cloud.tencent.com/document/product/267/34223). Jika Anda membuat templat perekaman sekaligus tugas perekaman untuk streaming langsung yang sama, proses perekaman akan dilakukan berulang-ulang. Periksa sudah diaktifkan atau belumnya suatu tugas perekaman di konsol dan sudah diaktifkan atau belumnya tugas perekaman lain dengan [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/30847) (API v3.0).

> ! Jika masalah berlanjut, [kirimkan tiket](https://console.cloud.tencent.com/workorder/category).
