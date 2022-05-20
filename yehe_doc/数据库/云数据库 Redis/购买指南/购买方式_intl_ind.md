## Ikhtisar

Dokumen ini menjelaskan cara membeli dan mengonfigurasi instans TencentDB for Redis dengan dua cara berikut:

- Konsol: Anda dapat mengonfigurasi parameter instans dan langsung melakukan pembelian di konsol web.
- API: Anda dapat memanggil `CreateInstances` API untuk melakukan pembelian.

## Persiapan Pembelian

- Anda telah mendaftarkan akun Tencent Cloud dan menyelesaikan verifikasi identitas.
  - Untuk mendaftarkan akun Tencent Cloud:
    
    <div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://intl.cloud.tencent.com/register" target="_blank"  style="color: white; font-size:16px;" hotrep="document.guide.3128.btn1">Klik di sini untuk mendaftar akun Tencent Cloud</a></div>
  - Untuk memverifikasi identitas Anda:
    
    <div style="background-color:#00A4FF; width: 170px; height: 35px; line-height:35px; text-align:center;"><a href="https://console.cloud.tencent.com/developer" target="_blank"  style="color: white; font-size:16px;"  hotrep="document.guide.3128.btn2">Klik di sini untuk memverifikasi identitas Anda</a></div>
- Anda sudah menentukan wilayah dan AZ untuk instans. Untuk informasi selengkapnya, lihat [Wilayah dan AZ](https://intl.cloud.tencent.com/document/product/239/4106).
- Anda sudah menentukan spesifikasi dan persyaratan performa instans. Untuk informasi selengkapnya, lihat [Seri Produk](https://intl.cloud.tencent.com/document/product/239/31959) dan [Performa](https://intl.cloud.tencent.com/document/product/239/17952).
- Anda sudah menentukan VPC dan grup keamanan untuk instans. Untuk informasi selengkapnya, lihat [Virtual Private Cloud](https://intl.cloud.tencent.com/document/product/215) dan [Mengonfigurasi Grup Keamanan untuk TencentDB](https://intl.cloud.tencent.com/document/product/239/31945).
- Untuk men-deploy instans di beberapa AZ di wilayah yang sama, pelajari selengkapnya tentang arsitektur [deployment multi-AZ](https://intl.cloud.tencent.com/document/product/239/39812) terlebih dahulu.
- Untuk mendukung pemisahan baca/tulis, pelajari selengkapnya tentang cara [pemisahan baca/tulis](https://intl.cloud.tencent.com/document/product/239/33132) dilaksanakan terlebih dahulu.
- Anda telah memeriksa detail penagihan instans. Untuk informasi selengkapnya, lihat [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/239/31954). Biaya database selama satu jam akan dibekukan saat Anda membuat database bayar sesuai pemakaian. Pastikan saldo akun Anda mencukupi sebelum melakukan pembelian.

## Membeli di Konsol

1. Login ke [halaman pembelian TencentDB for Redis](https://buy.intl.cloud.tencent.com/redis) dengan akun Tencent Cloud Anda.
2. Konfigurasikan instans sesuai kebutuhan berdasarkan deskripsi parameter di bawah ini:
   <table class="table-striped">
   <tbody>
   <tr><th>Parameter</th><th>Deskripsi</th></tr>
   <tr>
   <td>Cara Penagihan</td>
   <td><b>Bayar sesuai pemakaian</b>. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/239/31954">Ikhtisar Penagihan</a>.</td></tr>	
   <tr>
   <td>Wilayah</td>
   <td>Pilih wilayah tempat instans Anda berada. Harap pilih wilayah yang paling dekat dengan Anda untuk mengurangi latensi akses.<ul><li>Perhatikan bahwa wilayah tidak dapat diubah setelah instans berhasil dibuat.</li><li>Sebaiknya pilih wilayah yang sama dengan instans CVM untuk komunikasi jaringan pribadi.</li></ul></td></tr>
   <tr>
   <td>Edisi Instans</td>
   <td>Pilih <b>Edisi Memori</b>. Edisi CKV saat ini tidak tersedia.</td></tr>
   <tr>
   <td>Versi yang Kompatibel</td>
   <td>Pilih versi performa tinggi berdasarkan mesin Redis sumber terbuka, yang kompatibel dengan Redis 6.0, 5.0, 4.0, dan 2.8. v2.8 tidak tersedia saat ini, dan disarankan v4.0 atau yang lebih baru. Untuk membeli instans Redis v2.8, <a href="https://intl.cloud.tencent.com/document/product/239/31959">kirim tiket</a> untuk mengajukan permohonan.</td></tr>	 
   <tr> 
       <td>Arsitektur</td>
   <td>v4.0 atau yang lebih baru mendukung arsitektur standar dan arsitektur kluster, sedangkan v2.8 hanya mendukung arsitektur standar. Untuk informasi selengkapnya tentang arsitektur produk, lihat <a href="https://intl.cloud.tencent.com/document/product/239/31959">Edisi Memori (Arsitektur Standar)</a> dan <a href="https://intl.cloud.tencent.com/document/product/239/18336">Edisi Memori (Arsitektur Kluster)</a>.</td></tr>
   <tr>
   <td>Memori</td>
   <td>Konfigurasikan ukuran memori yang diperlukan (0,25–64 GB) jika Anda memilih <b>Arsitektur Standar</b> untuk <b>Arsitektur</b>.</td></tr>
   <tr>
   <td>Jumlah Replika</td>
   <td>Pilih jumlah replika database. Beberapa replika dapat menyediakan master/replika ketersediaan tinggi, sehingga meningkatkan keamanan data. Replika juga dapat digunakan untuk meningkatkan performa baca saja. Jumlah replika dapat berbeda-beda, tergantung wilayah atau edisi seperti yang dikonfigurasi di konsol secara default.</td></tr>
   <tr>
   <td>Kuantitas Pecahan</td>
   <td>Atur jumlah pecahan sesuai kebutuhan jika Anda memilih <b>Arsitektur Kluster</b> untuk <b>Arsitektur</b>. Makin banyak pecahan, makin besar kapasitas penyimpanan klusternya.</td></tr> 
   <tr>    
   <td>Kapasitas Pecahan</td>
   <td>Atur kapasitas setiap pecahan jika Anda memilih <b>Arsitektur Kluster</b> untuk <b>Arsitektur</b>.</td></tr>
   <tr>    
   <td>Pratinjau Spesifikasi</td>
   <td>Pratinjau spesifikasi yang dipilih dan jumlah koneksi maksimum yang didukung dan throughput jaringan maksimum untuk memverifikasi apakah sudah memenuhi harapan Anda.</td></tr>
   <tr>    
   <td>Replika Baca Saja</td>
   <td>Tentukan apakah Anda akan mengaktifkan pemisahan baca/tulis. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/239/33132">Pemisahan  Baca/Tulis</a>.</td></tr>
   <tr>
   <td>Jaringan</td>
   <td>Baik <b>VPC</b> dan <b>jaringan klasik</b> sama-sama tidak didukung. Jika Anda memilih VPC, hanya perangkat di subnet yang dipilih yang dapat mengakses instans database. Jika Anda memilih jaringan klasik, hanya perangkat di jaringan klasik yang dipilih yang dapat mengakses instans database, dan deployment multi-AZ tidak didukung.</td></tr>
   <tr>
   <td>AZ</td>
   <td>Tentukan apakah akan mengaktifkan deployment multi-AZ. Deployment AZ tunggal dan deployment multi-AZ didukung. Instans yang di-deploy multi-AZ memiliki ketersediaan dan kemampuan pemulihan bencana yang lebih tinggi daripada instans yang di-deploy dengan AZ tunggal. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/239/39812">Deployment Multi-AZ</a>. <ul><li>Untuk deployment AZ tunggal, pilih AZ untuk node master dari <b>Grup Node Master (Master AZ)</b>. </li><li>Untuk deployment multi-AZ, pilih AZ master dari daftar drop-down <b>Grup Node Master (Master AZ)</b> dan tentukan AZ untuk replika dari daftar drop-down replika x, x adalah nomor replika, seperti replika 1 dan replika 2.</li></ul></tr>
   <tr>
   <td>Jaringan IPv4</td>
       <td>Pilih VPC dan subnet. Sebaiknya pilih <a href="https://cloud.tencent.com/document/product/215">VPC</a> yang sama di wilayah yang sama dengan instans CVM yang akan dihubungkan. Setelah membeli instans TencentDB, Anda dapat mengalihkan jaringannya dari klasik ke VPC, tetapi tidak bisa sebaliknya. Anda juga dapat mengeklik <b>Buat VPC</b> dan <b>Buat Subnet</b> untuk membuat lingkungan jaringan yang diperlukan seperti yang diinstruksikan dalam <a href="https://intl.cloud.tencent.com/document/product/215/31805">Membuat VPC</a>.</td></tr>
   <tr>
   <td>Port</td>
   <td>Port kustom. Rentang nilai: 1024–65535.</td></tr>
   <tr>
   <td>Templat Parameter</td>
   <td>Terapkan templat parameter untuk mengonfigurasi parameter dalam batch untuk instans. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/239/41810">Menerapkan Templat Parameter</a>.</td></tr>
   <tr>
   <td>Proyek</td>
   <td>Tetapkan instans Anda ke sebuah proyek untuk pengelolaan yang mudah.</td></tr>
   <tr>
   <td>Tag</td>
   <td>Tambahkan tag ke instans Anda untuk klasifikasi dan pengelolaan yang mudah. Klik <b>Tambahkan</b> untuk memilih kunci dan nilai tag.</td></tr> 
   <tr>
   <td>Grup Keamanan</td>
   <td>Tetapkan aturan grup keamanan untuk mengontrol lalu lintas masuk/keluar ke/dari instans Anda. Anda dapat memilih grup keamanan dari daftar drop-down <b>Grup Keamanan yang Ada</b> atau klik <b>Grup Keamanan Kustom</b> untuk membuatnya dan menetapkan aturan <b>masuk</b>/<b>keluar</b>. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/239/31945">Grup Keamanan</a>.</td></tr> 
   <tr>
   <td>Nama Instans</td>
   <td>Masukkan hingga 60 huruf, angka, tanda hubung, dan garis bawah.</td></tr>  
   <tr>
   <td>Atur Kata Sandi</td>
   <td><b>Autentikasi Kata Sandi</b> dipilih secara default.</tr>   
   <tr>
   <td>Kata sandi</td>
   <td>Tetapkan kata sandi akses untuk instans, yang harus memenuhi persyaratan berikut:<ul><li>Harus berisi 8–30 karakter. </li><li>Harus berisi karakter setidaknya dua dari jenis karakter berikut: huruf kecil, huruf besar, angka, dan simbol khusus (()`~!@#$%^&*-+=_|{}[]:;< >,.?/). </li><li>Tidak boleh diawali dengan garis miring (/).</li></ul></td></tr> 
   <tr>
   <td>Konfirmasikan Kata Sandi</td>
   <td>Masukkan kata sandi akses untuk instans lagi.</td></tr>  
   <tr>
   <td>Kuantitas</td>
   <td>Anda dapat membeli hingga 100 instans di setiap wilayah dan hingga 30 instans setiap sekali waktu.</td></tr> 
   </tbody></table>
3. Setelah memverifikasi bahwa parameter telah dikonfigurasi dengan benar, klik **Beli Sekarang**. Setelah pesan pembelian berhasil ditampilkan, klik **Buka Konsol** untuk masuk ke halaman daftar instans. Setelah status instans menjadi **Berjalan**, Anda dapat menggunakannya.

>?
>- Setelah mengaktifkan TencentDB for Redis, pastikan saldo akun Anda mencukupi. Saldo yang tidak mencukupi dapat menyebabkan pembayaran yang terlambat atau bahkan penarikan kembali. Untuk informasi selengkapnya, lihat [Bayar Jatuh Tempo](https://intl.cloud.tencent.com/document/product/239/31956).
>- Untuk operasi selanjutnya, lihat [Membuat Instans TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/37712).


## Pembelian melalui API

| API                                                     | Deskripsi      |
| :----------------------------------------------------------- | :------------ |
| [Buat Instans](https://intl.cloud.tencent.com/document/product/239/32069) | Membuat instans TencentDB for Redis |

