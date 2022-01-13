CLB klasik mengarahkan permintaan ke instance server asli yang berjalan dengan normal.Dokumen ini menjelaskan cara menambah atau menghapus server asli sesuai kebutuhan atau saat Anda menggunakan CLB Klasik untuk pertama kalinya.
## Prasyarat
Anda telah membuat instance CLB Klasik dan mengonfigurasikan pendengar.Untuk informasi selengkapnya, silakan lihat [Memulai CLB Klasik](https://intl.cloud.tencent.com/document/product/214/6574).
## Petunjuk
### Menambahkan server asli ke instance CLB Klasik
>?
>- Jika instance CLB Klasik diasosiasikan dengan grup penskalaan otomatis, instance CVM di grup itu akan ditambahkan secara otomatis ke server asli instance CLB Klasik tersebut.Jika instance CVM dihapus dari grup penskalaan otomatis, dia akan dihapus secara otomatis dari server-server asli instance CLB Klasik.
>- Jika Anda perlu menggunakan API untuk menambah server asli, silakan lihat [RegisterTargetsWithClassicalLB](https://intl.cloud.tencent.com/document/product/214/33802) API.
>
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance).
2.Di halaman "Manajemen Instance", pilih tab **Classic Cloud Load Balancer** (Penyeimbang Beban Cloud Klasik).
3.Klik **Configure Listener** (Konfigurasikan Pendengar) di kolom "Operasi" di sebelah kanan instance CLB Klasik target.
4.Pada modul konfigurasi pendengar, klik **Create** (Buat).
5.Pada jendela pop-up "Buat Pendengar", masukkan "port backend" (untuk informasi selengkapnya mengenai pemilihan port, silakan lihat [Port Server Biasa](https://intl.cloud.tencent.com/document/product/213/12451)) dan bidang terkait lainnya dan klik **Next** (Berikutnya) untuk menyelesaikan konfigurasi.Untuk informasi selengkapnya, silakan lihat [Mengonfigurasi CLB Klasik](https://intl.cloud.tencent.com/document/product/214/32462).
>?Anda perlu menentukan port server asli untuk CLB Klasik selama **listener creation** (pembuatan pendengar).
>
![](https://main.qcloudimg.com/raw/b2d43b48851d5c021a95872613e359c3.png)
6.Setelah pendengar dibuat, klik **Bind** (Ikat) pada modul pengikatan server asli.
7.Pada jendela pop-up **Bind CVM** (Ikat CVM), pilih instance CVM yang akan diikat, masukkan bobotnya, dan klik **OK**.
>?
>- Jendela pop-up hanya menampilkan instance CVM yang tersedia di satu wilayah dan satu lingkungan jaringan yang tidak terisolasi dan belum kedaluwarsa dengan bandwidth puncak lebih dari 0.
>- Jika beberapa server asli terikat, CLB akan meneruskan lalu lintas sesuai dengan algoritme hash untuk menyeimbangkan beban.
>- Makin besar bobot server, makin banyak permintaan yang diteruskan ke sana.Nilai defaultnya 10, dan rentang nilai yang bisa dikonfigurasi adalah 0-100.Jika bobot diatur ke 0, server tidak akan menerima permintaan baru.Jika persistensi sesi diaktifkan, distribusi permintaan yang tidak merata di antara server asli bisa terjadi.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Algoritme dan Bobot](https://intl.cloud.tencent.com/document/product/214/5371).
>
![](https://main.qcloudimg.com/raw/d9d9becb83da5d34e913591b86132aa5.png)

### Memodifikasi bobot server asli untuk instance CLB Klasik
>?Saat ini, bobot server asli tidak bisa dimodifikasi melalui API untuk CLB Klasik.
>
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance).
2.Di halaman "Manajemen Instance", pilih tab **Classic Cloud Load Balancer** (Penyeimbang Beban Cloud Klasik).
3.Klik **Configure Listener** (Konfigurasikan Pendengar) di kolom "Operasi" di sebelah kanan instance CLB Klasik target.
4.Pada modul pengikatan server asli, modifikasi bobot server yang relevan.
>?Makin besar bobot server, makin banyak permintaan yang diteruskan ke sana.Nilai defaultnya 10, dan rentang nilai yang bisa dikonfigurasi adalah 0-100.Jika bobot diatur ke 0, server tidak akan menerima permintaan baru.Jika persistensi sesi diaktifkan, distribusi permintaan yang tidak merata di antara server asli bisa terjadi.Untuk informasi selengkapnya, silakan lihat [Konfigurasi Algoritme dan Bobot](https://intl.cloud.tencent.com/document/product/214/5371).
>
- **Method 1** (Metode 1).Modifikasi bobot satu server tunggal.
1.Temukan server yang bobotnya perlu dimodifikasi, arahkan kursor di bobot yang sesuai, dan klik <img src="https://main.qcloudimg.com/raw/4aae0dbec227f8fc18b4a35acf560f62.png" style="margin:0;">.
![](https://main.qcloudimg.com/raw/9230ac972fdd0f1b8c55c5188c0424fd.png)
2.Di jendela pop-up "Modifikasi Bobot", masukkan nilai bobot yang baru dan klik **Submit** (Kirim).
- **Method 2** (Metode 2).Modifikasi bobot beberapa server dalam beberapa batch.
>?Setelah modifikasi batch, server akan memiliki bobot yang sama.
		>
1.Klik kotak di depan server, pilih beberapa server, dan klik **Modify Weight** (Modifikasi Bobot) di bagian atas daftar.
![](https://main.qcloudimg.com/raw/6e58995f13d57fe0cd9ea0c92e32d931.png)
2.Di jendela pop-up "Modifikasi Bobot", masukkan nilai bobot yang baru dan klik **Submit** (Kirim).

### Melepas ikatan server asli dari instance CLB Klasik
>?
>- Melepas ikatan server asli akan melepas ikatan instance CLB Klasik dari instance CVM, dan CLB Klasik akan segera berhenti meneruskan permintaan ke sana.
>- Melepas ikatan server asli tidak akan memengaruhi siklus pemakaian instance CVM Anda, yang bisa ditambahkan lagi ke kluster server asli saat dibutuhkan.
>- Jika Anda perlu menggunakan API untuk melepas ikatan server asli, silakan lihat [DeregisterTargetsFromClassicalLB](https://intl.cloud.tencent.com/document/product/214/33807) API.
>
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance).
2.Di halaman "Manajemen Instance", pilih tab **Classic Cloud Load Balancer** (Penyeimbang Beban Cloud Klasik).
3.Klik **Configure Listener** (Konfigurasikan Pendengar) di kolom "Operasi" di sebelah kanan instance CLB Klasik target.
4.Pada modul pengikatan server asli, lepas ikatan server yang terikat.
- **Method 1** (Metode 1).Lepas ikatan satu server tunggal.
1.Temukan server yang perlu dilepas ikatannya dan klik **Unbind** (Lepas Ikatan) di kolom **Operation** (Operasi) di sebelah kanan.
![](https://main.qcloudimg.com/raw/f398806fd564c8b0ff9ed1610b76ce4e.png)
2.Pada jendela pop-up "Lepas Ikatan Server Asli", konfirmasi server yang akan dilepas dan klik **Submit** (Kirim).
- **Method 2** (Metode 2).Lepas ikatan beberapa server dalam beberapa batch.
1.Klik kotak di depan server, pilih beberapa server, dan klik **Unbind** (Lepas Ikatan) di bagian atas daftar.
![](https://main.qcloudimg.com/raw/088d33fd06d677741f58b91ea05ab1a2.png)
2.Pada jendela pop-up "Lepas Ikatan Server Asli", konfirmasi server-server yang akan dilepas dan klik **Submit** (Kirim).


