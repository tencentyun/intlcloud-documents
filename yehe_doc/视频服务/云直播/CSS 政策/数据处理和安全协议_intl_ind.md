## 1\. LATAR BELAKANG

Modul ini berlaku jika Anda menggunakan fitur Cloud Streaming Services (“**Fitur**”). Modul ini tergabung dalam Perjanjian Keamanan dan Pemrosesan Data yang terdapat di [DPSA](https://intl.cloud.tencent.com/document/product/301/17347). Istilah-istilah yang digunakan tetapi tidak didefinisikan dalam Modul ini memiliki arti yang sama dengan yang ditentukan dalam DPSA. Jika terdapat perbedaan antara DPSA dan Modul ini, maka Modul inilah yang akan berlaku apabila terjadi inkonsistensi.

## 2\. PEMROSESAN

Kami akan memproses data berikut sehubungan dengan Fitur:

| **Informasi Pribadi**                                     | **Penggunaan**                                                      |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Data Konfigurasi:**<li>Konfigurasi nama domain (konfigurasi autentikasi, konfigurasi batas bandwidth, konfigurasi https (termasuk sertifikat ssl), konfigurasi wilayah, konfigurasi templat, konfigurasi server asal);<br><li>Templat pencatatan (nama templat, format file pencatatan, durasi file tunggal pencatatan, jangka waktu penyimpanan, batas waktu peringkasan (hanya untuk hls), Pencatatan subaplikasi VOD);<br><li>Templat watermark (nama templat, gambar watermark, lokasi watermark);<br><li>Templat transkode (nama templat, kecepatan bit, tinggi layar langsung, GOP, metode pengkodean);<br><li>Templat tangkapan layar (nama templat, frekuensi tangkapan layar, lokasi cos penyimpnanan tangkapan layar, nama file tangkapan layar, Smart Porn Detection). | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda dan pengguna akhir sesuai konfigurasi spesifik Anda.<br/>Harap perhatikan bahwa data ini disimpan dalam fitur TencentDB for MySQL kami. |
| **Video Rekaman Langsung** (jika Anda memilih untuk merekam video streaming langsung) | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/>Harap diperhatikan bahwa data ini disimpan dalam fitur Video on Demand (VOD) kami. |
| **Tangkapan Layar Langsung** (jika Anda memilih untuk merekam tangkapan layar langsung), termasuk tangkapan layar langsung yang dihasilkan setelah deteksi situs porno (jika Anda memilih untuk mengaktifkan fungsi Konfigurasi Deteksi Pornografi) | Kami hanya memproses data ini untuk tujuan menyediakan Fitur kepada Anda.<br/>Harap diingat bahwa data ini disimpan dalam fitur Cloud Object Storage (COS) kami.<br/>Harap perhatikan bahwa jika Anda mengaktifkan fungsi Konfigurasi Deteksi Pornografi dari Fitur ini, data tersebut disimpan di COS akan dikirimkan ke fitur Image Moderation System (IMS) kami, untuk menyediakan Anda dengan Fitur ini sebagaimana diperlukan (termasuk untuk meninjau dan mengidentifikasi informasi pornografi dan mengembalikan hasil yang terkait). IMS akan menyimpan tangkapan layar langsung hanya selama diperlukan untuk menyelesaikan proses deteksi pornografi dan mengembalikan hasil terkait hal yang sama kepada Anda. |


## 3\. WILAYAH LAYANAN

Sebagaimana ditentukan dalam DPSA.

## 4\. SUB-PROSESOR

Sebagaimana ditentukan dalam DPSA, termasuk Aceville Pte Ltd.

## 5\. RETENSI DATA

Kami akan menyimpan data pribadi yang diproses sehubungan dengan Fitur sebagai berikut:

| **Informasi Pribadi**                                | **Kebijakan Retensi**                                         |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| Configuration DataLive Recording VideosLive Screenshots | Kami menyimpan data tersebut selama batas waktu penyimpanan data yang Anda pilih. Atau, apabila Anda menghapus akun atau menghentikan penggunaan Fitur, kami akan menghapus data tersebut setelah 60 hari. |

Anda dapat meminta penghapusan data pribadi tersebut sesuai dengan DPSA.

## 6\. KETENTUAN KHUSUS

Anda harus memastikan bahwa Fitur ini hanya digunakan oleh pengguna akhir yang setidaknya berusia minimum di mana seseorang dapat menyetujui pemrosesan data pribadi mereka, atau bahwa persetujuan orang tua diperoleh untuk individu di bawah usia minimum. Persyaratan ini mungkin berbeda-beda, tergantung pada wilayah hukum tempat pengguna akhir berada.

Anda menyatakan, menjamin, dan berjanji bahwa Anda harus memperoleh dan mempertahankan semua persetujuan yang diperlukan dari Pengguna Akhir sehubungan dengan pemrosesan data pribadi mereka terkait dengan Fitur sesuai dengan hukum yang berlaku dan untuk memungkinkan kami mematuhi hukum yang berlaku.  