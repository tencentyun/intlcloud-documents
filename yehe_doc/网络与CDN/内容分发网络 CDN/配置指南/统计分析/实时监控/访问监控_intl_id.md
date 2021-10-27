>Dokumen ini menjelaskan versi baru konsol. Dokumen ini memberikan statistik yang lebih komprehensif dan mendetail dan digunakan sebagai dasar untuk penagihan. Kami menyarankan Anda menggunakan versi baru.
## Deskripsi Metrik
### Metrik di halaman ikhtisar
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn) dan pilih **Statistics** (Statistik) > **Realtime Monitoring** (Pemantauan Real-Time) di bilah samping kiri untuk masuk ke halaman pengelolaan. Tab **Access Monitoring** (Pemantauan Akses) ditampilkan secara default. Kurva pemantauan semua nama domain dengan perincian 1 menit dalam 6 jam terakhir akan dikembalikan, termasuk metrik berikut:
+ Bandwidth: Dihitung dengan membagi total lalu lintas dalam satu menit dengan 60 detik.
+ Traffic hit rate (Hit rate lalu lintas): (Total lalu lintas downstream - lalu lintas tarik-asal) / total lalu lintas downstream dalam satu menit.
+ Percentage of request status code (Persentase kode status permintaan): Bagan persentase kode status (2XX/3XX/4XX/5XX) yang dikembalikan dalam periode waktu yang dipilih.
+ 2XX request status codes (Kode status permintaan 2XX): Kode status yang dihasilkan oleh pemantauan kode status 2XX akan dihitung.
+ 3XX request status codes (Kode status permintaan 3XX): Kode status yang dihasilkan oleh pemantauan kode status 3XX akan dihitung.
+ 4XX request status codes (Kode status permintaan 4XX): Kode status yang dihasilkan oleh pemantauan kode status 4XX akan dihitung.
+ 5XX request status codes (Kode status permintaan 5XX): Kode status yang dihasilkan oleh pemantauan kode status 5XX akan dihitung.

### Data di halaman detail
Klik **View Details** (Lihat Detail) di bawah setiap metrik untuk masuk ke halaman detail metrik.
![](https://main.qcloudimg.com/raw/3aae6ee3d47dadae74ca59667b6d7310.png)
Anda juga dapat beralih ke metrik lain dengan memilihnya dari daftar drop-down di sudut kiri atas halaman detail.
![](https://main.qcloudimg.com/raw/5262321ca413e2a24274a0d0fe086263.png)
Di halaman detail, Anda dapat melihat data metrik berikut:
+ Bandwidth: Total bandwidth puncak, kurva bandwidth real-time, dan peringkat bandwidth nama domain (dari besar ke kecil).
+ Traffic (Lalu Lintas): Total lalu lintas, kurva lalu lintas real-time, peringkat lalu lintas nama domain (dari tinggi ke rendah), dan peringkat lalu lintas URL (dari tinggi ke rendah).
+ Traffic hit rate (Hit rate lalu lintas): Hit rate lalu lintas, kurva hit rate lalu lintas real-time, dan peringkat hit rate lalu lintas nama domain (dari tinggi ke rendah).
+ Requests (Permintaan): Jumlah total permintaan, kurva jumlah permintaan real-time, peringkat jumlah permintaan nama domain (dari tinggi ke rendah), dan peringkat jumlah permintaan URL (dari tinggi ke rendah)
+ Status code percentage (Persentase kode status): Diagram lingkaran kode status 2XX, 3XX, 4XX, dan 5XX serta jumlah dan persentasenya.
+ 2XX status codes (Kode status 2XX): Kurva pemantauan real-time dari kode status 2XX dan kode substatusnya serta peringkat kode status 2XX nama domain (dari tinggi ke rendah).
+ 3XX status codes (Kode status 3XX): Kurva pemantauan real-time dari kode status 3XX dan kode substatusnya serta peringkat kode status 3XX nama domain (dari tinggi ke rendah).
+ 4XX status codes (Kode status 4XX): Kurva pemantauan real-time dari kode status 4XX dan kode substatusnya serta peringkat kode status 4XX nama domain (dari tinggi ke rendah).
+ 5XX status codes (Kode status 5XX): Kurva pemantauan real-time dari kode status 5XX dan kode substatusnya serta peringkat kode status 5XX nama domain (dari tinggi ke rendah).


## Deskripsi Perincian
### Perincian di halaman ikhtisar
Halaman pemantauan menyediakan opsi untuk menampilkan kurva data dengan perincian 1 menit, 5 menit, 1 jam, atau 1 hari. Perincian waktu minimum yang dapat ditampilkan bervariasi menurut periode waktu yang dipilih.
+ Periode waktu ≤ 6 jam: Perincian waktu minimum adalah 1 menit. Latensi untuk menampilkan kurva 1 menit adalah sekitar 5–10 menit.
+ 6 jam < periode waktu ≤ 24 jam: Perincian waktu minimum adalah 5 menit. Latensi untuk menampilkan kurva 5 menit adalah sekitar 5–10 menit.
+ 24 jam < periode waktu ≤ 31 hari: Perincian waktu minimum adalah 1 jam.
+ Periode waktu > 31 hari: Perincian waktu minimum adalah 1 hari.


### Perincian di halaman detail
Opsi perincian waktu di halaman detail metrik adalah sebagai berikut:
+ Periode waktu ≤ 1 hari: Perincian waktu minimum adalah 1 menit. Latensi untuk menampilkan kurva 1 menit adalah sekitar 5–10 menit.
+ 1 hari < periode waktu ≤ 31 hari: Perincian waktu minimum bisa 5 menit, 1 jam, atau 1 hari.
+ Periode waktu > 31 hari: Perincian waktu minimum adalah 1 hari.

>!
>- Saat ini, kueri data pada perincian statistik 1 menit hanya didukung di Tiongkok Daratan. Perincian minimum untuk kueri data riwayat adalah 5 menit.
>- Periode waktu maksimum untuk kueri adalah 90 hari.


### Deskripsi Agregasi
Metode untuk mengagregasi data 1 menit menjadi data 5 menit, 1 jam, atau 1 hari berbeda berdasarkan metrik data.
+ Bandwidth: Perincian terkecil yang disediakan oleh CDN untuk memantau data bandwidth adalah 1 menit. Berdasarkan standar industri, biaya umumnya ditagih dengan perincian 5 menit, yang dihitung dengan mengambil rata-rata nilai data 1 menit. Oleh karena itu, data bandwidth pada perincian 1 jam atau 1 hari dapat dihitung berdasarkan nilai bandwidth maksimum 5 menit.
+ Traffic (Lalu Lintas): Data lalu lintas pada perincian 5 menit, 1 jam, atau 1 hari diperoleh dengan mengagregasi data lalu lintas 1 menit.
+ Traffic hit rate (Hit rate lalu lintas): Berdasarkan perincian yang dipilih, hit rate lalu lintas dihitung dengan menggunakan rumus “(total lalu lintas downstream - lalu lintas tarik-asal) / total lalu lintas downstream" daripada mengambil rata-rata nilai data 1 menit.
+ Number of requests and status codes (+ Jumlah permintaan dan kode status:): Data pada perincian 5 menit, 1 jam, atau 1 hari diperoleh dengan mengagregasi data lalu lintas 1 menit.


## Deskripsi sumber data
### Data yang dapat ditagih dan data log
- Data yang dikumpulkan berdasarkan byte downstream dalam log nama domain akselerasi adalah data pada lapisan aplikasi, sementara lalu lintas yang dihasilkan selama transfer data aktual melalui jaringan adalah 5–15% lebih banyak daripada data lapisan aplikasi.
 + Consumption by TCP/IP headers (Konsumsi oleh header TCP/IP): Dalam permintaan HTTP berbasis TCP/IP, setiap paket memiliki ukuran maksimum 1.500 byte, termasuk header TCP dan IP sebesar 40 byte, yang menghasilkan lalu lintas selama transfer tetapi tidak dapat dihitung oleh lapisan aplikasi. Overhead bagian ini adalah sekitar 3%.
 + TCP retransmission (Transmisi ulang TCP): Selama transfer data normal melalui jaringan, sekitar 3-10% paket hilang di internet, dan server akan mentransmisikan kembali bagian yang hilang. Lalu lintas ini tidak dapat dihitung oleh lapisan aplikasi, yang berjumlah 3-7% dari total lalu lintas.
- Sesuai standar industri, data yang dapat ditagih adalah jumlah data lapisan aplikasi dan biaya overhead yang disebutkan di atas. CDN Tencent Cloud mengambil 10% sebagai proporsi overhead sehingga lalu lintas/bandwidth yang dapat ditagih yang dipantau adalah sekitar 110% dari data yang dicatat.
- Kecuali untuk lalu lintas dan bandwidth, semua metrik lainnya dikumpulkan di lapisan aplikasi. Karena fluktuasi jaringan, statistik yang ditampilkan di halaman pemantauan sedikit berbeda dari yang ada di log karena kehilangan data dapat terjadi selama penarikan log dari simpul atau pelaporan data oleh server.

### Deskripsi sumber data
+ Jika opsi **statistical district** (distrik statistik) atau **ISP** tidak dipilih sebagai filter, semua data yang dikueri akan menjadi data yang dapat ditagih.
+ Jika opsi **statistical district** (distrik statistik) atau **ISP** dipilih sebagai filter, data harus dicocokkan untuk penghitungan oleh IP klien di log akses, dan semua data yang dikueri akan menjadi data log.

## Deskripsi Filter
+ Saat ini, kueri oleh **statistical district** (distrik statistik) dan **ISP** tidak didukung. Anda hanya dapat mengkueri semua ISP berdasarkan distrik atau mengueri semua distrik berdasarkan ISP.
+ Saat ini, pemantauan tarik-asal tidak mendukung pemfilteran berdasarkan area statistik atau ISP.
+ Saat ini, pemantauan tarik-asal tidak mendukung pemfilteran berdasarkan permintaan HTTPS/HTTP.



