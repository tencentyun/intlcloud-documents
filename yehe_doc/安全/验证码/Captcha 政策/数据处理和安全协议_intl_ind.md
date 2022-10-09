## 1\. LATAR BELAKANG

Modul ini berlaku jika Anda menggunakan fitur Captcha (“**Fitur**”). Modul ini tergabung dalam Perjanjian Keamanan dan Pemrosesan Data yang terdapat di  (“[DPSA](https://intl.cloud.tencent.com/document/product/301/17347)”). Istilah-istilah yang digunakan tetapi tidak didefinisikan dalam Modul ini memiliki arti yang sama dengan yang ditentukan dalam DPSA. Jika terdapat perbedaan antara DPSA dan Modul ini, Modul inilah yang akan berlaku apabila terjadi inkonsistensi.

## 2\. **PEMROSESAN**

Kami akan memproses data berikut sehubungan dengan Fitur:

| **Informasi Pribadi**                                     | **Penggunaan**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Data Konfigurasi Captcha:** Captcha APPID, nama Captcha, UIN, APPID, batas domain, kunci enkripsi, jenis Captcha, jenis adegan, verifikasi pintar, mesin pintar, warna skema, bahasa, kelas/tingkat intersepsi jahat, ambang lalu lintas, layar penuh atas, waktu pembuatan, waktu pembaruan | Kami hanya memproses data ini untuk tujuan penyediaan Fitur kepada Anda, sesuai dengan konfigurasi tertentu Anda.<br/>Perlu diperhatikan bahwa data ini dibagikan dengan fitur TencentDB for Redis (Redis) untuk tujuan ini, dan disimpan serta dicadangkan dalam fitur TencentDB for MySQL (MySQL) kami. |
| **Data Statistik** **Captcha (pengguna akhir):** Captcha APPID, waktu, informasi permintaan (tindakan tiket, verifikasi, throughput, dan intersepsi), informasi tiket (jumlah tiket, throughput, dan intersepsi) | Kami hanya memproses data ini untuk memberi Anda statistik penggunaan Fitur oleh Anda.<br/>Harap diperhatikan bahwa data ini disimpan dan dicadangkan dalam fitur MySQL kami. |
| **Data Verifikasi Manusia (pengguna akhir):** bahasa browser, URL halaman, status pekerja web (jika ada), upaya verifikasi, fitur browser, agen pengguna, resolusi layar, dimensi halaman dan layar, perujuk halaman, Sistem Operasi, CPU, nilai kanvas, font, hash properti, pengubah ukuran browser, info WebGL, GPU, zona waktu, plugin, kedalaman warna, driver web, set karakter, posisi perangkat dan kursor, waktu buka, stempel waktu, cookie login, pengaturan javascript, status baterai, alamat IP, penyimpanan dan status DB, status DoNotTrack, status AdBlock, domain | Kami memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/>Harap diperhatikan bahwa data ini disimpan dan dicadangkan dalam fitur MySQL kami. |
| **Data Cookie (pengguna akhir):** TDC_itoken                    | Kami menggunakan cookie ini untuk tujuan menyediakan Fitur kepada Anda (untuk mengidentifikasi apakah permintaan pengguna akhir berasal dari perangkat yang sama). |

## 3\. WILAYAH LAYANAN

Sebagaimana ditentukan dalam DPSA.

## 4\. SUB-PROSESOR

Sebagaimana ditentukan dalam DPSA, termasuk Aceville Pte Ltd. dan Shenzhen Tencent Computer System Co., Ltd..

## 5\. RETENSI DATA

Kami akan menyimpan data pribadi yang diproses sehubungan dengan Fitur sebagai berikut (kecuali diwajibkan lain oleh Undang-Undang Perlindungan Data yang berlaku):

| **Informasi Pribadi**   | **Kebijakan Retensi**                                         |
| -------------------------- | ------------------------------------------------------------ |
| Data Konfigurasi Captcha | Kami menyimpan data tersebut hingga Anda menghapusnya secara manual. Atau, apabila Anda menghapus akun, kami akan menghapus data tersebut setelah 7 hari. |
| Data Statistik Captcha   | Kami menyimpan data tersebut selama 1 tahun, kecuali Anda menghapus data tersebut secara manual (dalam hal ini data tersebut akan dihapus dalam waktu 7 hari).\] |
| Data Verifikasi Manusia    | Disimpan selama 30 hari, kecuali jika Anda meminta penghapusan data tersebut (dalam kasus tersebut, data akan dihapus dalam waktu 7 hari). |
| Data Cookie                | Cookie ini akan kedaluwarsa ketika pengguna akhir menghapus riwayat penjelajahan mereka. |

Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.

## 6\. PERSYARATAN KHUSUS

Anda harus memastikan bahwa Fitur ini hanya digunakan oleh pengguna akhir yang setidaknya berusia minimum yang mana seseorang dapat menyetujui pemrosesan data pribadi mereka, atau bahwa persetujuan orang tua diperoleh untuk individu di bawah usia minimum. Persyaratan ini mungkin berbeda-beda, tergantung pada wilayah hukum tempat pengguna akhir berada.

Anda menyatakan, menjamin, dan berjanji bahwa Anda akan menyediakan semua pemberitahuan yang diperlukan, dan memperoleh serta memelihara semua persetujuan yang diperlukan dari pengguna akhir, dalam hubungan dengan pemrosesan data pribadi mereka dan penggunaan cookie terkait dengan Fitur, sesuai dengan hukum yang berlaku dan agar memungkinkan kami mematuhi hukum yang berlaku. Anda setuju bahwa Anda akan mengganti rugi dan membebaskan Tencent dari dan terhadap semua klaim, kewajiban, biaya, biaya, kerugian atau kerusakan (termasuk kerugian konsekuensial, kehilangan laba, rugi reputasi, dan semua bunga, penalti, dan biaya serta pengeluaran profesional lainnya) yang dikeluarkan oleh Tencent yang timbul secara langsung atau tidak langsung dari pelanggaran persyaratan ini.  