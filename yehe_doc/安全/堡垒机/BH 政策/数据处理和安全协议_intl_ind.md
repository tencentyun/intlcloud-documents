## 1\. **LATAR BELAKANG**

Modul ini berlaku jika Anda menggunakan fitur Bastion Host (“**Fitur**”). Modul ini tergabung dalam Perjanjian Pemrosesan dan Keamanan Data yang terdapat di (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347 )”). Istilah-istilah yang digunakan tetapi tidak didefinisikan dalam Modul ini memiliki arti yang sama dengan yang ditetapkan dalam DPSA. Jika terdapat perbedaan antara DPSA dengan Modul ini, Modul inilah yang akan berlaku apabila terjadi ketidaksesuaian.

## 2\. **PEMROSESAN**

Kami akan memproses data berikut sehubungan dengan Fitur:

| **Informasi Pribadi**                                     | **Penggunaan**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Informasi manajemen aset:** IP host, OS host, port host, akun host, IP basis data, jenis basis data, Port basis data, akun basis data, grup aset, kata sandi aset | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda sesuai konfigurasi spesifik Anda. Harap diperhatikan bahwa data ini disimpan di fitur MySQL kami. |
| **Data catatan pembayaran:** ID instans, IP klien, nomor instans, waktu kedaluwarsa, wilayah, operasi | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda sesuai konfigurasi spesifik Anda. Harap diperhatikan bahwa data ini disimpan di fitur MySQL kami. |
| **Informasi kontrol akses:** nama otoritas, status, nama pengguna, akun aset, tindakan yang diizinkan, perintah berisiko tinggi | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda sesuai konfigurasi spesifik Anda. Harap diperhatikan bahwa data ini disimpan di fitur MySQL kami. |
| **Informasi manajemen pengguna:** nama, nomor telepon, metode verifikasi, email, grup pengguna, waktu akses | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda sesuai konfigurasi spesifik Anda. Harap diperhatikan bahwa data ini disimpan di fitur MySQL kami. |
| **Informasi pemeliharaan:** id/nama tugas, metode eksekusi, periode eksekusi, waktu eksekusi, perintah eksekusi, informasi aset | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda sesuai konfigurasi spesifik Anda. Harap diperhatikan bahwa data ini disimpan di fitur MySQL kami. |
| **Log operasi:** IP aset, IP sumber, akun aset, waktu, nama aset, nama pengguna, durasi sesi\ukuran sesi, jumlah perintah\jumlah perintah pemblokiran, status, pemutaran ulang operasi | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda sesuai konfigurasi spesifik Anda. Harap diperhatikan bahwa data ini disimpan di fitur MySQL kami. |
| **Log akses sistem:** waktu, nama pengguna, IP sumber, metode login, hasil login, resolusi, mode akses. | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda sesuai konfigurasi spesifik Anda. Harap diperhatikan bahwa data ini disimpan di fitur MySQL kami. |
| **Log audit:** Waktu, akun auditor, IP sumber, ID aset yang diaudit, IP aset yang diaudit, operasi, jenis sesi, detail audit | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda sesuai konfigurasi spesifik Anda. Harap diperhatikan bahwa data ini disimpan di fitur MySQL kami. |
| **Log peristiwa risiko:** Jenis peristiwa, deskripsi acara, waktu    | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda sesuai konfigurasi spesifik Anda. Harap diperhatikan bahwa data ini disimpan di fitur MySQL kami. |
| **Konfigurasi sistem:** daftar putih, pengaturan keamanan (durasi tidak aktif web, jumlah kesalahan kata sandi,  durasi pemblokiran), verifikasi pengaturan (kompleksitas kata sandi, panjang kata sandi minimum, tanggal kedaluwarsa kata sandi, kata sandi historis yang sama, autentikasi dua faktor, informasi LDAP) | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda sesuai konfigurasi spesifik Anda. Harap diperhatikan bahwa data ini disimpan di fitur MySQL kami. |
| **Log cadangan:** Log login sistem (waktu, nama pengguna、IP sumber、metode login, hasil login), log login aset (IP aset, IP sumber, akun aset, waktu, nama aset, nama pengguna, durasi sesi) | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda sesuai konfigurasi spesifik Anda. Harap diperhatikan bahwa data ini dicadangkan di fitur Pusat Operasi Keamanan kami. |

## 3\. **WILAYAH LAYANAN**

Sebagaimana ditentukan dalam DPSA.

## 4\. **SUB-PROSESOR**

Sebagaimana ditentukan dalam DPSA.

## 5\. **RETENSI DATA**

Kami akan menyimpan data pribadi yang diproses sehubungan dengan Fitur sebagai berikut (kecuali diwajibkan lain oleh Undang-Undang Perlindungan Data yang berlaku):

| **Informasi Pribadi**         | **Kebijakan Retensi**                                         |
| -------------------------------- | ------------------------------------------------------------ |
| **Informasi manajemen aset** | Kami menyimpan data tersebut sampai Anda mengakhiri langganan untuk Fitur, di mana data tersebut akan dihapus dalam waktu 7 hari. |
| **Data catatan pembayaran**         | Kami menyimpan data tersebut sampai Anda mengakhiri langganan untuk Fitur, di mana data tersebut akan dihapus dalam waktu 7 hari. |
| **Informasi kontrol akses**   | Kami menyimpan data tersebut sampai Anda mengakhiri langganan untuk Fitur, di mana data tersebut akan dihapus dalam waktu 7 hari. |
| **Informasi manajemen pengguna**  | Kami menyimpan data tersebut sampai Anda mengakhiri langganan untuk Fitur, di mana data tersebut akan dihapus dalam waktu 7 hari. |
| **Informasi pemeliharaan**      | Kami menyimpan data tersebut sampai Anda mengakhiri langganan untuk Fitur, di mana data tersebut akan dihapus dalam waktu 7 hari. |
| **Log operasi**                | Kami menyimpan data tersebut sampai Anda mengakhiri langganan untuk Fitur, di mana data tersebut akan dihapus dalam waktu 7 hari. |
| **Log akses sistem**            | Kami menyimpan data tersebut sampai Anda mengakhiri langganan untuk Fitur, di mana data tersebut akan dihapus dalam waktu 7 hari. |
| **Log audit**                    | Kami menyimpan data tersebut sampai Anda mengakhiri langganan untuk Fitur, di mana data tersebut akan dihapus dalam waktu 7 hari. |
| **Log peristiwa risiko**               | Kami menyimpan data tersebut sampai Anda mengakhiri langganan untuk Fitur, di mana data tersebut akan dihapus dalam waktu 7 hari. |
| **Konfigurasi sistem**         | Kami menyimpan data tersebut sampai Anda mengakhiri langganan untuk Fitur, di mana data tersebut akan dihapus dalam waktu 7 hari. |
| **Log cadangan**                   | Kami menyimpan data tersebut sampai Anda mengakhiri langganan untuk Fitur, di mana data tersebut akan dihapus dalam waktu 7 hari. |

Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.

## 6\. **PERSYARATAN KHUSUS**

Anda mengakui, memahami, dan menyetujui bahwa (i) kami tidak membuat pernyataan atau jaminan apa pun atau menjanjikan apa pun bahwa Fitur ini akan mematuhi hukum atau peraturan yang berlaku, (ii) Anda telah memperoleh lisensi, pendaftaran, atau persetujuan yang mungkin diperlukan sehubungan dengan atau terkait penggunaan Fitur (seperti yang sehubungan dengan aktivitas pemrosesan pembayaran, catatan yang dapat dianggap sebagai bagian dari fungsi Fitur), dan (iii) setiap ketergantungan pada atau penggunaan Fitur ini adalah mutlak risiko Anda.