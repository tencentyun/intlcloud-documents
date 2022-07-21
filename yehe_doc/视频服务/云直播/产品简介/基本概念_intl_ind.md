
[](id:push)
### Push
 Push adalah proses dilakukannya push oleh host terhadap sumber video dan audio lokal ke server Tencent Video Cloud. Proses ini disebut juga sebagai "push RTMP" dalam beberapa kasus. 



[](id:play)
### Pemutaran ulang
Pemutaran ulang berarti pemutaran ulang langsung dengan melakukan pull terhadap video dan audio sumber dari server Tencent Video Cloud dan memutar ulangnya di alamat tertentu setelah push langsung diterapkan. Sumber video dibuat secara real-time. Cara ini hanya dapat digunakan jika ada pengguna yang melakukan push streaming langsung. Setelah host menghentikan streaming, URL streaming langsung akan menjadi tidak valid, dan karena streaming langsung diputar ulang secara real-time, bilah kemajuan tidak akan ditampilkan di pemutar selama pemutaran ulang. 


[](id:push_domain)
### Nama domain push
Nama domain yang digunakan untuk melakukan push streaming langsung, dan merupakan pengaturan wajib. Nama domain dapat digunakan untuk streaming langsung setelah Anda mendaftarkannya. Setelah nama domain push dikonfigurasikan, CSS akan membuat URL push yang sesuai. Informasi selengkapnya dapat dilihat di [Splicing Live Stream URLs (Menyambungkan URL Streaming Langsung)](https://intl.cloud.tencent.com/document/product/267/38393).

[](id:play_domain)
### Nama domain pemutaran ulang
Nama domain yang digunakan untuk memutar ulang streaming langsung, dan merupakan pengaturan wajib. Nama domain dapat digunakan untuk streaming langsung setelah Anda mendaftarkannya. Setelah nama domain pemutaran ulang dikonfigurasikan, CSS akan membuat URL pemutaran ulang yang sesuai. Informasi selengkapnya dapat dilihat di [Splicing Live Stream URLs (Menyambungkan URL Streaming Langsung)](https://intl.cloud.tencent.com/document/product/267/38393).


[](id:cname)
### CNAME Domain
Nama domain yang berakhiran `.liveplay.myqcloud.com` dan ditetapkan oleh sistem ke nama domain akselerasi yang dikonfigurasikan di konsol CSS. Anda harus mengonfigurasikan rekaman CNAME dengan penyedia layanan nama domain Anda. Setelah rekaman aktif, CSS akan mengatur resolusi nama domain dan semua permintaan yang dikirim ke nama domain ini akan diteruskan ke server edge CSS.

[](id:streamname)
### StreamName
ID streaming. `StreamName` dan nama domain digunakan bersama sebagai pengidentifikasi unik streaming.

### AppName[](id:appname)
Nama aplikasi streaming langsung yang digunakan untuk mengidentifikasi jalur penyimpanan file media streaming langsung. Aplikasi diberi nama `live` secara default, tetapi nama ini dapat diubah.

[](id:trans)
### Transcoding
Transcoding adalah tugas offline yang mengonversi satu bitstream video menjadi bitstream lainnya. Transcoding mengubah codec, resolusi, bitrate, dan parameter lain bitstream untuk pemutaran ulang di perangkat lain di berbagai lingkungan jaringan. Fitur ini dapat:
- Meningkatkan kompatibilitas: Lakukan transcoding video sumber ke format yang mendukung banyak tipe perangkat agar pemutaran ulang berlangsung lancar.
- Meningkatkan adaptabilitas bandwidth: Lakukan transcoding video sumber menjadi output dalam format Smooth (Lancar), SD, HD, dan UHD. Pengguna akhir dapat memilih bitrate untuk kondisi jaringannya sesuai kebutuhan.
- Mengurangi penggunaan bandwidth: Gunakan codec lanjutan untuk transcoding guna mengurangi bitrate video secara signifikan dengan tetap mempertahankan kualitas asli sehingga penggunaan bandwidth pemutaran ulang berkurang.

[](id:h264)
### H.264
Standar codec untuk video digital dengan kompresi tinggi. H.264 dikembangkan oleh ITU-T Video Coding Experts Group (VCEG) dan ISO/IEC Moving Picture Experts Group (MPEG). Transcoding dengan H.264 memiliki keunggulan sebagai berikut:
- H.264 memungkinkan transfer gambar digital SD (dengan resolusi kurang dari 1280 x 720) dengan kecepatan kurang dari 1 Mbps.
- H.264 menghasilkan kualitas gambar yang lebih baik dibandingkan codec video lain dengan bandwidth yang sama.


[](id:h265)
### H.265
H.265 dioptimalkan berdasarkan codec video H.264 dan masih memiliki beberapa fitur yang sama dengan H.264. Transcoding dengan H.265 memiliki keunggulan sebagai berikut:
- H.265 memungkinkan transfer audio/video HD umum (720p dengan resolusi 1280 x 720) dengan kecepatan 1‒2 Mbps.
- H.265 memberikan keseimbangan yang optimal antara bitstream, kualitas pengodean, latensi, dan kompleksitas algoritma.


[](id:message)
### Pemberitahuan pesan peristiwa
Ketika pemberitahuan peristiwa terpicu selama push langsung, Tencent Cloud akan mengirim permintaan ke server Anda sesuai dengan templat pesan yang telah dikonfigurasikan, lalu server akan melakukan autentikasi dan merespons permintaan tersebut. Informasi selengkapnya tentang protokol respons dapat dilihat di [Event Message Notification Protocol (Protokol Pemberitahuan Pesan Peristiwa)](https://intl.cloud.tencent.com/document/product/267/38080). Setelah autentikasi selesai, server akan memperoleh paket JSON yang berisi informasi panggilan balik yang selanjutnya akan diuraikan dan dicatat. 


[](id:link)
### Referer
 Bidang `txSecret` di URL push dan pemutaran ulang. Referer digunakan untuk mencegah penyerang memalsukan backend untuk membuat URL push dan mencuri URL pemutaran ulang Anda.
 
[](id:record)
 ### Perekaman langsung
Selama push, file video yang sudah dibuat dengan muxing streaming asal (tanpa memodifikasi informasi, seperti data audio dan video serta stempel waktu terkait) dapat disimpan di platform VOD. Untuk menggunakan fitur ini, Anda perlu mengaktifkan [VOD](https://intl.cloud.tencent.com/product/vod) terlebih dahulu.
 
[](id:watermark)
### Watermark
Untuk mencegah pelanggaran terhadap hak cipta video Anda selama push langsung, Anda dapat menambahkan watermark pada streaming video selama transcoding. Watermark dapat berupa teks atau gambar.

[](id:screenshot)
### Pengambilan tangkapan layar
Fitur ini menangkap gambar video dari streaming langsung yang di-push pada interval tertentu, lalu menyimpan file gambar yang dihasilkan di COS. Untuk mengaktifkan pengambilan tangkapan layar, Anda harus terlebih dahulu memberikan izin kepada CSS untuk menulis ke bucket COS Anda. Informasi selengkapnya dapat dilihat di [Authorizing CSS to Store Screenshots in a COS Bucket (Mengizinkan CSS Menyimpan Tangkapan Layar di Bucket COS)](https://intl.cloud.tencent.com/document/product/267/33384). 

[](id:yellow_confidence)
### Deteksi pornografi
Berdasarkan fitur pengambilan tangkapan layar, sistem dapat melakukan pengenalan konten pada tangkapan layar, lalu mengirimkan panggilan balik hasil sesuai dengan templat pengambilan tangkapan layar dan deteksi pornografi yang terikat dengan nama domain push. Informasi selengkapnya dapat dilihat di [Live Screencapture and Porn Detection (Tangkapan Layar dan Deteksi Pornografi Langsung)](https://intl.cloud.tencent.com/document/product/267/31072).
 
 [](id:95)
 ### Bandwidth persentil ke-95
Selama periode penagihan, bandwidth puncak setiap 5 menit akan diambil sebagai titik sampel. Semua titik sampel pada bulan berjalan akan disusun berdasarkan urutan menurun, dan 5% teratas akan dihilangkan. Nilai tertinggi titik sampel yang tersisa akan digunakan sebagai persentil ke-95 dari bandwidth puncak bulanan.
