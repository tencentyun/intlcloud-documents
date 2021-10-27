### Bisakah CDN ditagih berdasarkan jumlah permintaan?
Tidak. Saat ini, CDN tidak mendukung penagihan berdasarkan jumlah permintaan.

### Apa jadinya jika akun saya terlambat membayar?
Untuk informasi selengkapnya, silakan lihat bagian [Pembayaran Terlambat](https://intl.cloud.tencent.com/document/product/228/2949#.E6.AC.A0.E8.B4.B9.E8.AF.B4.E6.98.8E) pada dokumen uraian penagihan.

### Jika server asal menggunakan COS, apakah saya akan ditagih menurut lalu lintas yang dihasilkan oleh tarik-asal dari CDN ke COS?
Tidak. Lalu lintas yang dihasilkan oleh tarik-asal dari CDN ke COS ditagih berdasarkan COS, bukan CDN.Untuk informasi selengkapnya, silakan lihat [COS sebagai Server Asal CDN](https://intl.cloud.tencent.com/document/product/228/32977).

### Jika dimatikan (atau dinonaktifkan), apakah CDN akan menghasilkan lalu lintas dan memakan biaya?
Setelah layanan akselerasi nama domain CDN dimatikan, jika nama domain masih dikonfigurasi dengan CNAME, kode status 404 akan dikembalikan untuk permintaan yang telah diselesaikan ke simpul dan sejumlah kecil lalu lintas akan digunakan.Konsol akan merekam data lalu lintas ini sebagai pedoman Anda.Log yang sesuai juga akan dihasilkan.Namun, karena layanan akselerasi nama domain Anda telah dimatikan, Anda tidak akan ditagih atas penggunaan lalu lintas dan paket log ini.Kami sarankan Anda mengubah resolusi tarik-asal terlebih dahulu sebelum mematikan layanan akselerasi tersebut.

### Bagaimana saya mengubah cara penagihan CDN?

Jika Anda merasa cara penagihan yang dipilih tidak cocok untuk kondisi bisnis Anda yang sebenarnya (untuk informasi selengkapnya tentang teknik memilih cara penagihan yang tepat, silakan baca [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/228/2949#.E8.AE.A1.E8.B4.B9.E6.96.B9.E5.BC.8F.E9.80.89.E6.8B.A9)), Anda dapat mengubahnya dengan mengikuti prosedur di bawah ini:
1.Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), lihat halaman ikhtisar layanan, lalu klik **Change** (Ubah) di bagian cara penagihan di sebelah kanan.
![](https://main.qcloudimg.com/raw/38b82d3d166970552437b5525b74c44f.png)
2.Ubah cara penagihan awal dari **Bill by Traffic** (Tagih sesuai Lalu Lintas) menjadi **Bill by Bandwidth** (Tagih sesuai Bandwidth).
![](https://main.qcloudimg.com/raw/6fd1575557d0c4b7b06be9f1fc30e1da.png)
3.Setelah Anda mengubah cara penagihan menjadi **Bill by Bandwidth** (Tagih sesuai Bandwidth), biaya untuk total penggunaan yang dihasilkan pada tanggal saat itu akan ditagih dan dipotong pada hari berikutnya:

### Jika server asal menggunakan CVM, apakah saya akan ditagih atas lalu lintas yang dihasilkan oleh tarik-asal dari CDN ke CVM?

Tidak. CDN tidak menagih bayaran atas jenis lalu lintas ini.

### Berapa tingkat konversi dari Gbps ke Mbps dalam tagihan CDN?

Dalam tagihan CDN, 1 Gbps = 1000 Mbps, 1 Mbps = 1000 Kbps, dan 1 Kbps = 1000 bps.

### Apakah hanya lalu lintas downstream yang dapat ditagih di CDN?

YaCDN hanya menagih bayaran untuk lalu lintas downstream, bukan lalu lintas upstream.


### Bagaimana cara penagihan CDN?

CDN menawarkan dua metode penagihan: tagihan-berdasarkan-bandwidth dan tagihan-berdasarkan-lalu-lintas (default).Kedua metode ini bersifat bayar sesuai pemakaian dengan siklus penagihan harian.Pembayaran untuk total konsumsi yang dihasilkan antara 00.00.00–23.59.59 pada tanggal berjalan akan dipotong sebelum 18.00 hari berikutnya.Untuk informasi selengkapnya tentang cara memilih metode penagihan yang tepat, silakan lihat [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/228/2949).

### Kapan biaya CDN akan dipotong?

CDN ditagih secara pascabayar.Tagihan untuk total konsumsi yang dihasilkan pada hari saat itu ditagih dan dipotong pada hari berikutnya.

- Jika Anda beralih dari tagihan-berdasarkan-bandwidth ke tagihan-berdasarkan-lalu-lintas ketika konsumsi belum terjadi untuk hari tersebut, Anda akan ditagih dengan cara tagihan-berdasarkan-lalu-lintas pada hari berikutnya kecuali jika Anda mengubah lagi cara penagihan.
- Jika konsumsi sudah terjadi, Anda akan ditagih dengan tagihan-berdasarkan-bandwidth pada hari berikutnya.Anda akan ditagih dengan penagihan-berdasarkan-lalu-lintas pada hari ketiga ketika menghitung konsumsi pada hari kedua, kecuali jika Anda mengubah lagi cara penagihan.

Jika biaya layanan CDN bulanan Anda melampaui atau diperkirakan melampaui USD 20.000, Anda memenuhi syarat untuk mendapatkan paket penagihan bulanan yang lebih fleksibel dan hemat.Untuk informasi selengkapnya, silakan kirim tiket guna menghubungi tim penjualan.

### Apakah penagihan persentil ke-95 bulanan itu?

Tagihan-berdasarkan-Bandwidth adalah metode penagihan berdasarkan penggunaan bandwidth puncak.
Persentil ke-95 bulanan: ada 288 poin statistik bandwidth CDN per hari.Mulai hari ke-1 bulan berjalan, semua poin statistik dari hari yang valid (ketika konsumsi bandwidth benar-benar terjadi) diurutkan secara tertib.5% poin statistik teratas dihilangkan, dan nilai tertinggi sisanya merupakan bandwidth yang dapat ditagih.Biaya kemudian dihitung berdasarkan harga yang tertera dan pola pelunasan.

> Contoh penagihan:
> Misalkan penagihan seorang pelanggan resmi dimulai pada 1 Januari dan harga kontrak adalah P USD/Mbps/bulan.
> Misalkan ada 14 hari yang valid pada Januari, dan bandwidth yang dapat ditagih untuk seluruh 14 hari yang valid tersebut memiliki 14 * 288 poin statistik.Sebanyak 5% poin statistik tertinggi dibuang sehingga Max95 merupakan poin tertinggi dalam poin statistik sisanya, yang merupakan bandwidth yang dapat ditagih.Biaya untuk Januari adalah:Max95 * P * 14 / 31.

### Bagaimana cara memeriksa tagihan CDN saya?

Anda dapat memeriksa tagihan di [Pusat Tagihan](https://console.cloud.tencent.com/expense/bill/overview) Tencent Cloud.Untuk informasi selengkapnya, silakan lihat [Kueri Tagihan](https://intl.cloud.tencent.com/document/product/228/6071).

### Apakah ada penundaan dalam menggunakan API untuk mengueri data?Berapa lama penundaan tersebut?
Ada penundaan tertentu dalam menggunakan API untuk mengueri data.Kueri data real-time, seperti data akses dan data penagihan, mengalami penundaan sekitar 5–10 menit, sedangkan kueri data analitik, seperti peringkat, akan mengalami penundaan sekitar setengah jam.Data tersebut dikalibrasi di backend sekitar pukul 3 pagi Waktu Beijing.
