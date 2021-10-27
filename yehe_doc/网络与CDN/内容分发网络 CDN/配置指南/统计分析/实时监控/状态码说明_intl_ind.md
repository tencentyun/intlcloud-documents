<style>
table th:nth-of-type(3) {
width: 586px;
}
</style>
Tabel di bawah ini menjelaskan kode status internal CDN.

| Kode Status | Arti | Saran |
| ----- | --------------------------------------------------- | ------------------------------------------------------------ |
| 400 | Kesalahan sintaks permintaan HTTP <br/>Server tidak dapat menguraikan permintaan | Periksa apakah sintaks permintaan sudah benar.                                  |
| 403    | Permintaan ditolak                             | Periksa apakah kontrol akses seperti daftar blokir/daftar yang diizinkan, daftar blokir/daftar yang diizinkan IP, atau autentikasi referer telah dikonfigurasi. |
| 413    | Panjang konten permintaan POST melebihi batas                    | Periksa ukuran konten permintaan POST dari klien (ukuran maksimumnya adalah 32 MB secara default).           |
| 414    | Panjang URL melebihi batas                     | Ukuran URL maksimum adalah 2 KB secara default.                                        |
| 423    | Permintaan perulangan                           | Periksa konfigurasi 301/302, tarik-asal HTTPS, dan metode penulisan ulang dari server asal. |
| 499    | Klien menutup koneksi                  | Periksa status klien dan konfigurasi waktu habis.                                |
| 502    | Kesalahan Gateway                             | Periksa apakah server asal bisnis normal.                                       |
| 503    | Kontrol frekuensi COS terpicu                          | Periksa konfigurasi cache atau apakah server asal COS mengembalikan no-cache/no-store.                 |
| 504    | Waktu Habis Gateway | Silakan hubungi situs web resmi. |
| 509    | Diblokir karena serangan CC                    | [Hubungi Kami](https://intl.cloud.tencent.com/contact-sales) atau [kumpulkan tiket](https://console.cloud.tencent.com/workorder/category) untuk membuka pemblokiran.                             |
| 514    | Frekuensi akses IP melebihi batas                       | Periksa konfigurasi kontrol frekuensi akses IP di Konsol CDN.                                 |
| 531    | Kesalahan saat menyelesaikan nama domain tarik-asal dalam permintaan HTTP          | Periksa konfigurasi resolusi nama domain dari server asal.                                       |
| 532    | Gagal membuat koneksi dengan server asal dalam permintaan HTTPS              | Periksa status port 443 dari server asal, konfigurasi sertifikat, atau ketersediaan server asal.                  |
| 533    | Waktu habis pada koneksi tarik-asal dalam permintaan HTTPS              | Periksa status port 443 dari server asal, konfigurasi sertifikat, atau ketersediaan server asal.                  |
| 537    | Waktu habis pada penerimaan data server asal dalam permintaan HTTPS             | Periksa stabilitas server asal bisnis.                                         |
| 538    | SSL handshake dari permintaan HTTPS gagal                | Periksa kompatibilitas antara protokol dan algoritme server asal.                                 |
| 539    | Validasi sertifikat permintaan HTTPS gagal           | Periksa apakah sertifikat server asal dikonfigurasi dengan benar (periode validitas dan kelengkapan rantai sertifikat).       |
| 540    | Validasi nama domain sertifikat dari permintaan HTTPS gagal          | Periksa apakah sertifikat server asal dikonfigurasi dengan benar.                                  |
| 562    | Gagal membuat koneksi dalam permintaan HTTPS                | [Hubungi Kami](https://intl.cloud.tencent.com/contact-sales) dengan informasi X-NWS-LOG-UUID atau [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk penanggulangan masalah.   |
| 563    | Waktu habis pada koneksi dalam permintaan HTTPS              | [Hubungi Kami](https://intl.cloud.tencent.com/contact-sales) dengan informasi X-NWS-LOG-UUID atau [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk penanggulangan masalah.   |
| 564    | Tarik-asal dalam permintaan HTTPS gagal                | Jika HTTP dikonfigurasi sebagai protokol tarik-asal, periksa beban dan pemanfaatan bandwidth atau batas akses server asal. </br>Jika metode protocol-follow dikonfigurasi, periksa status port 443 dan konfigurasi sertifikat server asal. </br>Jika tidak ada kesalahan yang ditemukan di server asal, [hubungi kami](https://intl.cloud.tencent.com/contact-sales) dengan informasi X-NWS-LOG-UUID atau [kirim tiket ](https://console.cloud.tencent.com/workorder/category) untuk penanggulangan masalah. |
