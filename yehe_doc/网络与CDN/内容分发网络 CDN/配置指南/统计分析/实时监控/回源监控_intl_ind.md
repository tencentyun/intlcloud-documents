

>! Kueri data tarik-asal tidak tersedia untuk nama domain ECDN sekarang.

## Deskripsi Metrik
### Metrik di halaman ikhtisar
Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn) dan pilih **Statistics** (Statistik) > **Realtime Monitoring** (Pemantauan Real-Time) di bilah samping kiri untuk masuk ke halaman pengelolaan.Tab **Access Monitoring** (Pemantauan Akses) ditampilkan secara default.Anda dapat mengeklik **Origin-Pull Monitoring** (Pemantauan Tarik-Asal) di sebelah kanan untuk masuk ke halaman metrik pemantauan tarik-asal.Kurva pemantauan semua nama domain dengan perincian 1 menit dalam 6 jam terakhir akan dikembalikan, termasuk metrik berikut:
+ Origin-pull bandwidth (Bandwidth tarik-asal):Dihitung dengan membagi total lalu lintas tarik-asal dalam satu menit dengan 60 detik.
+ Origin-pull traffic (Lalu lintas tarik-asal):Total lalu lintas tarik-asal di simpul cache pada lapisan terakhir.
+ Origin-pull requests (Permintaan tarik-asal):Jumlah total permintaan tarik-asal di simpul cache pada lapisan terakhir.
+ Origin-pull failure rate (Kecepatan kegagalan tarik-asal):Persentase permintaan tarik-asal yang gagal dari semua permintaan tarik-asal.
+ Percentage of tarik-asal status code (Persentase kode status tarik-asal):Bagan persentase kode status (2XX/3XX/4XX/5XX) ditampilkan untuk permintaan tarik-asal dalam periode waktu yang dipilih.
+ 2XX tarik-asal status codes (Kode status tarik-asal 2XX):Kode status yang dihasilkan oleh pemantauan kode status tarik-asal 2XX akan dihitung.
+ 3XX tarik-asal status codes (Kode status tarik-asal 3XX):Kode status yang dihasilkan oleh pemantauan kode status tarik-asal 3XX akan dihitung.
+ 4XX tarik-asal status codes (Kode status tarik-asal 4XX):Kode status yang dihasilkan oleh pemantauan kode status tarik-asal 4XX akan dihitung.
+ 5XX tarik-asal status codes (Kode status tarik-asal 5XX):Kode status yang dihasilkan oleh pemantauan kode status tarik-asal 5XX akan dihitung.

**Kondisi berikut akan dihitung sebagai permintaan tarik-asal yang gagal:**
+ Waktu habis dalam menerima data tarik-asal.
+ Waktu habis dalam mengirim permintaan tarik-asal.
+ Waktu habis dalam membuat koneksi TCP untuk tarik-asal.
+ Server asal secara aktif menutup koneksi.
+ Kesalahan kompatibilitas protokol HTTP dari server asal.

### Data di halaman detail
Klik **Learn More** (Pelajari Selengkapnya) di bawah setiap metrik untuk masuk ke halaman detail metrik.
![](https://main.qcloudimg.com/raw/f63c60b1e8d89db0302c9e102548fe70.png)
Anda juga dapat beralih ke metrik lain dengan memilihnya dari daftar drop-down di sudut kiri atas halaman detail.
![](https://main.qcloudimg.com/raw/795eeb398f3f73663f5168f3b41612c4.png)

## Deskripsi Perincian
### Perincian di halaman ikhtisar
Halaman pemantauan menyediakan opsi untuk menampilkan kurva data dengan perincian 1 menit, 5 menit, 1 jam, atau 1 hari.Perincian waktu minimum yang dapat ditampilkan bervariasi menurut periode waktu yang dipilih.
+ Periode waktu ≤ 6 jam:Perincian waktu minimum adalah 1 menit.Latensi untuk menampilkan kurva 1 menit adalah sekitar 3 menit.
+ 6 jam < periode waktu ≤ 24 jam:Perincian waktu minimum adalah 5 menit.Latensi untuk menampilkan kurva 5 menit adalah sekitar 5–10 menit.
+ 24 jam < periode waktu ≤ 31 hari:Perincian waktu minimum adalah 1 jam.
+ Periode waktu > 31 hari:Perincian waktu minimum adalah 1 hari.


### Perincian di halaman detail
Opsi perincian waktu di halaman detail metrik adalah sebagai berikut:
+ Periode waktu ≤ 24 jam:Perincian waktu minimum adalah 1 menit.Latensi untuk menampilkan kurva 1 menit adalah sekitar 3 menit.
+ 24 jam < periode waktu ≤ 31 hari:Perincian waktu minimum bisa 5 menit, 1 jam, atau 1 hari.
+ Periode waktu > 31 hari:Perincian waktu minimum adalah 1 hari.

>!
>- Data yang dikumpulkan dengan perincian 1 menit hanya dapat dikueri di konsol versi baru.Untuk data riwayat, perincian minimum untuk kueri adalah 5 menit.
>- Periode waktu maksimum untuk kueri adalah 90 hari.

### Deskripsi Agregasi
Metode untuk mengagregasi data 1 menit menjadi data 5 menit, 1 jam, atau 1 hari berbeda berdasarkan metrik data.
+ Origin-pull bandwidth (Bandwidth tarik-asal):Perincian terkecil yang disediakan oleh CDN untuk memantau data bandwidth adalah 1 menit.Berdasarkan standar industri, biaya umumnya ditagih dengan perincian 5 menit, yang dihitung dengan mengambil rata-rata nilai data 1 menit.Oleh karena itu, data bandwidth pada perincian 1 jam atau 1 hari dapat dihitung berdasarkan nilai bandwidth maksimum 5 menit.
+ Origin-pull traffic (Lalu lintas tarik-asal):Data lalu lintas pada perincian 5 menit, 1 jam, atau 1 hari diperoleh dengan mengagregasi data lalu lintas 1 menit.
+ Origin-pull requests (Permintaan tarik-asal):Jumlah permintaan pada perincian 5 menit, 1 jam, atau 1 hari diperoleh dengan mengagregasi jumlah permintaan 1 menit.
+ Origin-pull failure rate (Kecepatan kegagalan tarik-asal):Dihitung dengan membagi jumlah total kegagalan tarik-asal dengan jumlah total permintaan tarik-asal berdasarkan perincian waktu yang dipilih.
+ Origin-pull status codes (Kode status tarik-asal):Data kode status pada perincian 5 menit, 1 jam, atau 1 hari diperoleh dengan mengagregasi data kode status 1 menit.



