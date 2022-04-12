
Dokumen ini menjelaskan fitur dan kasus penggunaan layanan proksi database di TencentDB for MySQL.

Proksi database adalah layanan proksi jaringan antara layanan TencentDB dan layanan aplikasi. Ini digunakan untuk membuat proksi pada semua permintaan ketika layanan aplikasi mengakses database.
Alamat akses proksi database tidak tergantung pada alamat akses database asli. Permintaan yang tiba di alamat proksi semuanya diteruskan melalui kluster proksi untuk mengakses sumber dan node replika database. Permintaan Baca/Tulis dipisahkan, sehingga permintaan baca diteruskan ke instans baca saja, yang menurunkan beban database sumber.
>?Saat ini, layanan proksi database dalam uji beta, dan Anda dapat menggunakannya secara gratis.
>
## Fitur
- **High stability** (Stabilitas tinggi)
Proksi database mengadopsi arsitektur kluster untuk deployment, dengan banyak node memastikan failover yang lancar.
- **Strong isolation** (Isolasi kuat)
Proksi database menggunakan sumber daya independen untuk menyediakan layanan proksi untuk instans saat ini (sumber daya dari berbagai proksi diisolasi dan tidak dibagikan).
- **Ultra-High performance** (Performa Ultra Tinggi)
Setiap proksi dapat memproses hingga 100.000 permintaan per detik.
- **Convenient and fast scaling** (Penskalaan yang mudah dan cepat)
Anda dapat secara dinamis menambahkan 1–60 node proksi (hanya 6 node yang didukung selama pengujian beta).
- **Comprehensive performance monitoring** (Pemantauan performa yang komprehensif)
Metrik performa dipantau di tingkat kedua, seperti jumlah permintaan baca/tulis, CPU, dan memori. Jumlah proksi dapat disesuaikan dengan [data pemantauan](https://intl.cloud.tencent.com/document/product/236/42055) dan perencanaan bisnis.
- **Hot reload** (Muat ulang terbaru)
Saat instans sumber dialihkan, atau konfigurasinya diubah, atau instans baca saja ditambahkan/dihapus, proksi database dapat secara dinamis memuat ulang konfigurasi tanpa menyebabkan pemutusan jaringan atau memulai ulang.   
- **Support for [automatic read/write separation](https://intl.cloud.tencent.com/document/product/236/42054)** (Dukungan untuk [pemisahan baca/tulis otomatis](https://intl.cloud.tencent.com/document/product/236/42054))
Ini dapat secara efektif mengurangi beban baca instans sumber ketika fitur pemisahan baca/tulis dari proksi database diaktifkan. Instans Baca Saja dapat ditambahkan untuk menskalakan kluster database secara horizontal dan secara otomatis menerapkan pemisahan baca/tulis, yang menghilangkan kerumitan memisahkan permintaan baca dan tulis bisnis secara manual. Ini sangat cocok untuk skenario dengan beban baca yang tinggi.
Misalnya, setelah fitur pemisahan baca/tulis dari proksi database diaktifkan, hanya satu alamat koneksi proksi yang perlu dikonfigurasi dalam aplikasi. Alamat ini akan secara otomatis menerapkan pemisahan baca/tulis dan mengirim permintaan baca ke instans baca saja dan permintaan tulis ke instans sumber. Bahkan jika Anda menambahkan atau menghapus instans baca saja, Anda tidak perlu menyesuaikan pengaturan aplikasi.

## Kasus Penggunaan
- Bisnis dengan performa rendah ketika ada banyak koneksi non-persisten.
- Bisnis menggunakan beberapa instans baca saja, dan pemisahan baca/tulis diterapkan secara manual pada aplikasi, yang mengakibatkan biaya dan risiko pemeliharaan yang lebih tinggi.
- Pemuatan instans tinggi yang disebabkan oleh terlalu banyak koneksi.

