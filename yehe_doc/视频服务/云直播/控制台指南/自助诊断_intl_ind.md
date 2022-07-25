 CSS menawarkan alat diagnosis mandiri yang dapat Anda gunakan untuk mendeteksi dan memecahkan dengan cepat masalah push dan pemutaran ulang yang berkaitan dengan pengguna, URL, nama domain, streaming, dan faktor lainnya. Fitur ini masih dalam pengujian beta sekarang. Hasil diagnosis disampaikan hanya sebagai referensi.

## Prasyarat
- Tersedia URL push/pemutaran ulang [yang disambungkan oleh Anda](https://intl.cloud.tencent.com/document/product/267/38393) atau yang dibuat oleh [Address Generator (Pembuat Alamat)](https://intl.cloud.tencent.com/document/product/267/31084).
- URL push telah digunakan untuk [push](https://intl.cloud.tencent.com/document/product/267/31558).


## Petunjuk
Ikuti langkah-langkah di bawah ini untuk mendiagnosis masalah push/pemutaran ulang dalam streaming langsung:
1. Login ke konsol CSS dan pilih **[Self-Diagnosis](https://console.cloud.tencent.com/live/tools/selfcheck)** (Diagnosis Mandiri) di bilah sisi kiri.
2. Masukkan URL push atau pemutaran ulang yang ingin Anda diagnosis.
3. Klik **Execute Diagnosis** (Jalankan Diagnosis).

![](https://main.qcloudimg.com/raw/90fc6fce80283550af50214782c25b3c.png)

## Hasil
Hasil diagnosis dan saran untuk mengatasi masalah yang ditemukan akan ditampilkan.

<table>
<thead><tr><th width=15%>Item</th><th width=15%>Sub-Item</th><th>Deskripsi</th></tr></thead>
<tbody><tr>
<td rowspan=2>Informasi Pelanggan</td>
<td>APPID</td>
<td>ID aplikasi pelanggan</td>
</tr><tr>
<td>Status</td>
<td>Status akun pelanggan</td>
</tr><tr>
<td rowspan=3>Nama Domain</td>
<td>Nama Domain</td>
<td>Nama Domain</td>
</tr><tr>
<td>Jenis Nama Domain</td>
<td>Domain Push/Pemutaran Ulang</td>
</tr><tr>
<td>CNAME</td>
<td>Informasi resolusi CNAME</td>
</tr><tr>
<td rowspan=2>Status Streaming</td>
<td>Streaming</td>
<td>ID Streaming</td>
</tr><tr>
<td>Status</td>
<td>Status streaming</td>
</tr><tr>
<td rowspan=12>URL</td>
<td>URL</td>
<td>URL Push/Pemutaran Ulang</td>
</tr><tr>
<td>AppName</td>
<td>Jalur URL</td>
</tr><tr>
<td>StreamName</td>
<td>Nama streaming, yang digunakan untuk menghitung `txSecret`</td>
</tr><tr>
<td rowspan=3>Konfigurasi Autentikasi</td>
<td>Diaktifkan atau tidaknya autentikasi</td>
</tr><tr>
<td>Kunci utama</td>
</tr><tr>
<td>Kunci cadangan</td>
</tr><tr>
<td rowspan=6>Autentikasi Push/Pemutaran Ulang</td>
<td>Berhasil atau tidaknya autentikasi</td>
</tr><tr>
<td>Penyebab</td>
</tr><tr>
<td>StreamName Autentikasi</td>
</tr><tr>
<td>txSecret: String autentikasi yang dibuat setelah autentikasi push/pemutaran ulang diaktifkan.</td>
</tr><tr>
<td>txTime: Stempel waktu kedaluwarsa yang ditetapkan untuk URL push/pemutaran ulang</td>
</tr><tr>
<td>Waktu kedaluwarsa aktual URL</td>
</tr><tr>
<td rowspan=4>Bandwidth Akses</td>
<td rowspan=2>Konfigurasi Batas Pemakaian Bandwidth</td>
<td>Ditetapkan atau tidaknya batas pemakaian untuk bandwidth</td>
</tr><tr>
<td>Wilayah Akselerasi</td>
</tr><tr>
<td rowspan=2>Kunjungan IP</td>
<td>Status</td>
</tr><tr>
<td>Bandwidth Saat Ini</td>
</tr><tr>
<td rowspan=6>Aplikasi</td>
<td rowspan=3>Klien</td>
<td>
<li/>Push dari PC: Kami menyarankan Anda menggunakan <a href="https://intl.cloud.tencent.com/document/product/267/31569">OBS untuk push</a> untuk menguji push.
 <li/>Pemutaran ulang di PC: Kami menyarankan Anda menggunakan <a href="https://intl.cloud.tencent.com/document/product/267/32483">VLC player</a> (pemutar VLC) untuk menguji pemutaran ulang.</td>
</tr><tr>
<td>
<li/>Push dari web: Kami menyarankan Anda menggunakan <a href="https://console.cloud.tencent.com/live/tools/webpush">Push Web</a> untuk menguji push.</td>
</tr><tr>
<td>
<li/>Push dari aplikasi seluler: Instal <a href="https://intl.cloud.tencent.com/document/product/1071/38147">Aplikasi TCToolkit</a>, lalu pilih "RTMP for push" (RTMP untuk push) untuk menguji push.
<li/>Pemutaran ulang di aplikasi seluler: Instal <a href="https://intl.cloud.tencent.com/document/product/1071/38147">Aplikasi TCToolkit</a>, lalu pilih "Standard Live Broadcast" (Siaran Langsung Standar) untuk menguji pemutaran ulang.</td>
</tr><tr>
<td>Pembatasan IP</td>
<td>Periksa pengecualian yang disebabkan oleh daftar izin/daftar blokir IP atau pembatasan wilayah</td>
</tr><tr>
<td>Data Streaming</td>
<td>Menganalisis data pemantauan real-time streaming langsung untuk mengetahui pengecualian disebabkan oleh kemacetan jaringan, gangguan, atau alasan lain. <a href="https://console.cloud.tencent.com/live/analysis/stream">Lihat data streaming</a></td>
</tr>
</tbody></table>


>? Jika laporan diagnosis tidak dapat mengatasi masalah Anda, silakan [kirimkan tiket](https://console.cloud.tencent.com/workorder/category) atau hubungi dukungan teknis Tencent Cloud.
