>!Dokumen ini menjelaskan fitur manajemen akses **SMS**. Informasi selengkapnya tentang manajemen akses untuk layanan Tencent Cloud lainnya dapat dilihat di [CAM-Enabled Products (Produk yang Didukung CAM)](https://intl.cloud.tencent.com/document/product/598/10588).

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/zh/document/product/598) adalah layanan Tencent Cloud berbasis web yang membantu Anda mengelola dan mengontrol izin akses ke sumber daya Tencent Cloud dengan aman. Menggunakan CAM, Anda dapat membuat, mengelola, dan menghentikan pengguna (grup), dan mengontrol sumber daya Tencent Cloud yang dapat digunakan oleh pengguna tertentu melalui manajemen identitas dan kebijakan.

SMS telah terhubung ke **CAM**. Anda dapat memberikan izin akses SMS yang sesuai ke sub-akun sesuai kebutuhan.

## Memulai
Sebelum menggunakan CAM untuk SMS, Anda harus memiliki pengetahuan tentang konsep dasar CAM dan SMS, antara lain:
- CAM: [pengguna](https://intl.cloud.tencent.com/document/product/598/32633) and [kebijakan](https://intl.cloud.tencent.com/document/product/598/10601)
- SMS: [aplikasi](https://intl.cloud.tencent.com/document/product/382/35468)

## Kasus Penggunaan
### Isolasi izin di tingkat layanan Tencent Cloud
Di antara berbagai departemen yang menggunakan Tencent Cloud dalam suatu organisasi, departemen A bertanggung jawab atas layanan SMS. Personel departemen A memerlukan izin untuk mengakses SMS, tetapi tidak untuk mengakses layanan Tencent Cloud lainnya. Oleh karena itu, organisasi dapat membuat sub-akun untuk departemen A melalui akun root dan hanya memberikan izin terkait SMS, lalu menyediakannya bagi departemen A.
### Isolasi izin di tingkat aplikasi SMS
Isolasi diperlukan saat terdapat beberapa bisnis dalam suatu organisasi yang menggunakan SMS. Isolasi melibatkan isolasi sumber daya dan isolasi izin. Isolasi sumber daya diaktifkan oleh sistem [aplikasi SMS](), sementara isolasi izin diterapkan oleh manajemen akses SMS. Dalam hal ini, sub-akun dapat dibuat untuk setiap bisnis dan diberi izin ke aplikasi SMS yang relevan sehingga setiap bisnis hanya dapat mengakses aplikasi tertentu.
### Isolasi izin di tingkat tindakan SMS
Personel operasi produk dari bisnis yang menggunakan SMS dalam suatu organisasi perlu mengakses konsol SMS untuk mendapatkan statistik pengiriman, tetapi personel tersebut sebaiknya dilarang melakukan operasi yang bersifat sensitif (seperti memodifikasi pemberitahuan pengiriman yang melebihi batas atau batas tingkat pengiriman) untuk melindungi bisnis dari kesalahan operasi. Untuk melakukan ini, Anda dapat membuat kebijakan khusus yang memiliki izin untuk masuk ke konsol SMS tetapi tidak memiliki izin untuk memanggil API untuk pemberitahuan pengiriman yang melebihi batas dan batas tingkat pengiriman, membuat sub-akun dan mengikatnya ke kebijakan itu, lalu memberikan informasi sub-akun tersebut kepada personel operasi produk.

## Perincian Otorisasi
Fitur inti CAM adalah untuk **mengizinkan atau melarang akun melakukan beberapa operasi atau memanipulasi beberapa sumber daya**. Manajemen akses SMS mendukung [otorisasi tingkat sumber daya](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B). Perincian sumber daya adalah aplikasi SMS dan perincian operasi adalah [TencentCloud API (API TencentCloud)](https://intl.cloud.tencent.com/product/api), termasuk API server dan API yang dapat digunakan saat konsol SMS diakses. Untuk informasi selengkapnya, lihat [Authorizable Resources and Actions (Sumber Daya dan Tindakan yang Dapat Diotorisasi)](https://intl.cloud.tencent.com/document/product/382/38454).

## Batasan
- Manajemen akses SMS mendukung otorisasi pada tingkat aplikasi tetapi tidak pada tingkat sumber daya dengan perincian yang lebih halus (seperti informasi aplikasi dan informasi konfigurasi).
- Manajemen akses SMS tidak mendukung proyek dan tag.

