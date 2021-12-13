Anda dapat memilih citra berdasarkan atribut berikut:
- Lokasi (lihat [Wilayah dan Zona Ketersediaan](https://intl.cloud.tencent.com/document/product/213/6091))
- Sistem operasi
- Arsitektur (32-bit atau 64-bit)

Tencent Cloud menyediakan tiga jenis citra, yaitu citra publik, citra kustom, dan citra bersama.

## Citra Publik
**Citra publik** adalah citra yang disediakan oleh Tencent Cloud. Setiap citra berisi sistem operasi dan komponen inisialisasi yang disediakan oleh Tencent Cloud, dan tersedia untuk semua pengguna.

Fitur:
 - **Sistem operasi:** Anda dapat memilih sistem operasi yang diinginkan, seperti Linux atau Windows. Sistem operasi diperbarui secara berkala.
 - **Perangkat Lunak:** citra publik terintegrasi dengan paket perangkat lunak (seperti API) yang disediakan oleh Tencent Cloud, dan mendukung beberapa versi perangkat lunak dengan izin penuh, seperti Java, MySQL, SQL Server, Python, Ruby, dan Tomcat.
 - **Keamanan:** semua sistem operasi yang disediakan dilisensikan. Semua citra dibuat oleh tim keamanan dan OPS Tencent Cloud, dan telah diuji secara ketat. Komponen keamanan Tencent Cloud juga tersedia.
 - **Batas:** tidak ada.
 - **Biaya:** semua citra publik tidak dikenai biaya, kecuali untuk citra Windows di wilayah di luar daratan Tiongkok yang mungkin dikenai biaya lisensi.
 - **Dukungan teknis:**
  - Tencent Linux disediakan dan dikelola oleh Tencent Cloud.
  - Untuk masalah yang melibatkan citra pihak ketiga, hubungi komunitas sumber terbuka atau vendor sistem operasi. Tencent Cloud akan memberikan bantuan teknis selama proses pemecahan masalah jika diperlukan.

## Citra Kustom
**Citra kustom** dibuat oleh pengguna menggunakan fitur pembuatan citra, atau diimpor menggunakan fitur impor citra. Citra kustom hanya tersedia untuk pembuat konten dan orang yang diajak berbagi.

Fitur:
 - **Kasus penggunaan:** citra yang dibuat dari instans CVM dengan aplikasi yang di-deploy dapat digunakan untuk membuat lebih banyak instans yang berisi konfigurasi yang sama dengan cepat.
 - **Fitur:** Anda dapat membuat, menyalin, membagikan, dan menghentikan citra.
 - **Batasan:** setiap wilayah hanya mendukung maksimal 10 citra kustom.
 - **Biaya:** pembuatan citra dapat dikenakan biaya. Untuk biaya aktual, lihat harga yang ditampilkan saat Anda membuat citra. Replikasi lintas wilayah citra kustom tidak dikenai biaya.

Untuk informasi selengkapnya tentang citra kustom, lihat [Membuat Citra Kustom](https://intl.cloud.tencent.com/document/product/213/4942), [Menyalin Citra](https://intl.cloud.tencent.com/document/product/213/4943), [Berbagi Citra Kustom](https://intl.cloud.tencent.com/document/product/213/4944), [Membatalkan Berbagi Citra](https://intl.cloud.tencent.com/document/product/213/7148), dan [Mengimpor Citra](https://intl.cloud.tencent.com/document/product/213/4945).

## Citra yang Dibagikan
**Citra yang dibagikan** adalah citra kustom yang dibagikan kepada Anda oleh pengguna Tencent Cloud lain menggunakan fitur berbagi citra.
Citra-citra ini ditampilkan di wilayah yang sama dengan citra aslinya.

Fitur:
 - **Kasus penggunaan:** membantu pengguna lain membuat instans CVM dengan cepat.
 - **Fitur:** citra bersama hanya dapat digunakan untuk membuat instans CVM. Mengganti nama, menyalin, atau membagikan ulang citra dengan orang lain tidak didukung.
 - **Keamanan**: citra bersama tidak diperiksa oleh Tencent Cloud, yang dapat menimbulkan risiko keamanan. Kami sangat menyarankan untuk tidak menggunakan citra dari sumber yang tidak dikenal.
 - **Batasan**: setiap citra kustom dapat dibagikan kepada maksimal 50 pengguna Tencent Cloud. Citra kustom hanya dapat dibagikan dengan akun di wilayah yang sama dengan akun sumber.

Untuk informasi selengkapnya tentang citra yang dibagikan, lihat [Berbagi Citra Kustom](https://intl.cloud.tencent.com/document/product/213/4944) dan [Membatalkan Berbagi Citra](https://intl.cloud.tencent.com/document/product/213/7148).


