Jika Anda tidak dapat menonton streaming langsung dan tidak mengetahui masalahnya, identifikasi penyebab masalah secara cepat dengan mengikuti langkah-langkah di bawah ini:
![](https://main.qcloudimg.com/raw/54668f50b8e89909e6fc1600485723cc.png)

## Langkah 1. Periksa URL pemutaran ulang
Pertama, pastikan URL pemutaran ulang sudah benar. Kesalahan URL kemungkinan besar merupakan penyebab sebagian besar masalah. URL streaming langsung Tencent Cloud meliputi URL push dan URL pemutaran ulang. Anda harus memverifikasi terlebih dahulu **URL push tidak sengaja digunakan sebagai URL pemutaran ulang**.
![diff](https://main.qcloudimg.com/raw/44951fab55d1a8228bbc332d2713d9cf.png)
>**Playback URL for Mini CSS** (URL Pemutaran Ulang untuk Mini CSS):
>URL pemutaran ulang untuk Mini CSS dapat diperoleh melalui debugging. Anda dapat mencari kata kunci **startPlay** di pencarian global, lalu menetapkan titik perubahan debugging, yang akan membuat Mini CSS memanggil SDK RTMP. Parameter startPlay adalah URL pemutaran ulang.

## Langkah 2. Periksa streaming video
Meskipun URL pemutaran ulang sudah benar, pemutaran ulang belum tentu dapat berjalan dengan normal. Selanjutnya, Anda perlu memeriksa streaming video berjalan dengan normal atau tidak:
- Di **CSS**, URL streaming langsung tidak lagi tersedia setelah VJ menghentikan push.
- Di **VOD**, jika file video telah dihapus, Anda juga tidak dapat menonton video.

Solusi yang umum digunakan adalah melakukan pemeriksaan menggunakan VLC, sebuah pemutar sumber terbuka di PC yang mendukung banyak protokol.
![](//mc.qcloudimg.com/static/img/7923a14be5525bd37719c18d54243403/image.png)

## Langkah 3. Periksa pemutar
Jika tidak ada masalah pada streaming video, Anda perlu memeriksa bisa atau tidaknya pemutar berfungsi dengan normal secara kasus per kasus:

### 3.1 Browser web (A)
- **Format**: Browser seluler hanya mendukung URL pemutaran ulang dalam format **HLS (m3u8) dan MP4**.
- **HLS (m3u8)**: Protokol HLS Tencent Cloud dibuat berdasarkan "Lazy Start" (Mulai Lambat). Sederhananya, Tencent Cloud hanya akan memulai transcoding untuk format HLS ketika pemirsa meminta URL pemutaran ulang dalam format HLS. Tujuannya adalah untuk mencegah penggunaan sumber daya yang sia-sia. Namun, hal tersebut juga menciptakan masalah: **URL pemutaran ulang dalam format HLS tidak dapat diputar hingga 30 detik setelah pengguna pertama di dunia membuat permintaan**.

### 3.2 SDK RTMP (B)
Jika DEMO SDK RTMP berfungsi normal untuk pemutaran ulang, sebaiknya periksa kemungkinan adanya kesalahan logika antarmuka dengan melihat dokumen pemutaran ulang SDK RTMP [iOS] & [Android].

## Langkah 4. Periksa pemblokiran firewall (C)
Umumnya lingkungan jaringan perusahaan banyak pelanggan membatasi pemutaran ulang video melalui firewall yang mendeteksi apakah sumber daya yang diminta oleh HTTP merupakan sumber daya media streaming atau bukan (selain itu, tidak ada pimpinan yang ingin karyawannya menonton video selama jam kerja). Jika Anda dapat menonton streaming langsung secara normal melalui jaringan 4G, tetapi tidak dapat menontonnya melalui jaringan Wi-Fi perusahaan, artinya perusahaan Anda telah menerapkan pembatasan pada kebijakan jaringan. Dalam kasus ini, hubungi administrator untuk meminta perlakuan khusus bagi IP Anda.

## Langkah 5. Periksa pusher (D)
Jika URL streaming langsung tidak berfungsi dan tidak ada pemblokiran firewall seperti yang diuraikan dalam Langkah 4, kemungkinan push tidak berhasil. Buka Why the Push is Unsuccessful (Penyebab Push Gagal) untuk mengetahui langkah-langkah penyelesaian masalah lebih lanjut.



