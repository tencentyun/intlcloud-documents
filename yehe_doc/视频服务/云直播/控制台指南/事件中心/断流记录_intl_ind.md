Anda dapat melihat rekaman gangguan push langsung dan penyebabnya di konsol CSS.

## Prasyarat
Anda telah login ke [konsol CSS](https://console.cloud.tencent.com/live).
- Ada streaming langsung yang push-nya terganggu di akun Anda.

## Petunjuk

Di konsol, pilih **Event Center** > **[Stream Interruption Records](https://console.cloud.tencent.com/live/tools/streamevent)** (Pusat Peristiwa > Rekaman Gangguan Streaming) di bilah sisi kiri.
![](https://qcloudimg.tencent-cloud.cn/raw/7109f254ed3f4c892bd93632d9f04629.png)

Ini termasuk bidang-bidang berikut:
- **Path** (Jalur): `AppName` di URL push.
- **Stream Name** (Nama Streaming): `StreamName` di URL push.

[](id:erro_code)
## Penyebab Gangguan Streaming
Anda dapat menggunakan API [DescribeLiveStreamEventList](https://intl.cloud.tencent.com/document/product/267/30800) untuk melakukan kueri gangguan streaming.

Lihat tabel di bawah untuk mengetahui daftar penyebab gangguan streaming: 

<table border='0' >
 <tr>
<th >Penyebab</td>
 </tr>
 <tr>
<td>Kesalahan yang tidak diketahui.</td>
 </tr>
 <tr>
<td>Klien push mengganggu push terkait.</td>
 </tr>
 <tr>
<td >Kesalahan internal sistem CSS.</td>
 </tr>
 <tr>
<td>Konten protokol RTMP abnormal.</td>
 </tr>
 <tr>
<td>Ukuran frame RTMP tunggal melebihi batas atas.</td>
 </tr>
 <tr>
<td>Sistem mengganggu streaming karena tidak ada data yang dibuat untuk waktu yang lama.</td>
 </tr>
 <tr>
<td>Lapisan proxy menerima perintah gangguan.</td>
 </tr>
 <tr>
<td>Pengecualian jaringan klien push.</td>
 </tr>
 <tr  >
<td>Gagal mendapatkan informasi pengguna yang sesuai dengan URL push.</td>
 </tr>
 <tr>
<td>Layanan CSS Anda telah ditangguhkan.</td>
 </tr>
 <tr  >
<td>Layanan CSS Anda telah ditangguhkan karena pembayaran terlambat. Harap lakukan pembayaran untuk melanjutkan layanan.</td>
 </tr>
 <tr>
<td>Kami telah menangguhkan layanan CSS untuk akun Anda.</td>
 </tr>
 <tr>
<td>Push melalui alamat IP tidak diizinkan.</td>
 </tr>
 <tr>
<td>Tidak dapat mengenali nama domain push.</td>
 </tr>
 <tr>
<td>Nama domain push tidak valid.</td>
 </tr>
 <tr>
<td>Nama domain push dinonaktifkan.</td>
 </tr>
 <tr>
<td>Nama aplikasi push dinonaktifkan.</td>
 </tr>
 <tr>
<td>Streaming dinonaktifkan.</td>
 </tr>
 <tr>
<td>Mode saluran sedang digunakan, tetapi tidak ada saluran push.</td>
 </tr>
 <tr>
<td>Mode saluran sedang digunakan, tetapi saluran push saat ini dinonaktifkan.</td>
 </tr>
 <tr>
<td>Nama streaming berisi karakter yang tidak diizinkan.</td>
 </tr>
 <tr>
<td>Nama aplikasi push berisi karakter yang tidak diizinkan.</td>
 </tr>
 <tr  >
<td>IP klien push ada di daftar blokir.</td>
 </tr>
 <tr>
<td>IP klien push tidak ada di daftar izin.</td>
 </tr>
 <tr  >
<td>URL push tidak memiliki parameter waktu kedaluwarsa.</td>
 </tr>
 <tr>
<td  >Waktu kedaluwarsa tercapai.</td>
 </tr>
 <tr  >
<td>URL push tidak memiliki parameter autentikasi.</td>
 </tr>
 <tr  >
<td>Autentikasi gagal.</td>
 </tr>
 <tr  >
<td>Jumlah streaming push saat ini melebihi batas atas.</td>
 </tr>
 <tr>
<td>Jumlah streaming push dengan `StreamName` ini melebihi batas atas.</td>
 </tr>
 <tr>
<td  >Prioritas URL push lebih rendah daripada yang sudah ada.</td>
 </tr>
 <tr>
<td>Autentikasi pihak ketiga gagal.</td>
 </tr>
 <tr>
<td>CSS menerima permintaan penghentian sementara streaming dari pelanggan.</td>
 </tr>
 <tr>
<td>CSS menerima permintaan untuk menonaktifkan streaming dari pelanggan.</td>
 </tr>
 <tr>
<td>URL push baru menggantikan URL push ini.</td>
 </tr>
 <tr  >
<td>Alasan tidak diketahui.</td>
 </tr>
 <tr>
<td>Pengecualian data AMF RTMP.</td>
 </tr>
</table>


