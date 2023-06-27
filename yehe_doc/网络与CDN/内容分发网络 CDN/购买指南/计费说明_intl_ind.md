Mulai 7 Desember 2020, 21.30 (UTC +8), hanya **bill-by-hourly-traffic** (penagihan-berdasarkan-lalu-lintas-per-jam) tersedia untuk pengguna CDN baru.Cara penagihan tidak dapat diubah setelah aktivasi layanan.
Tingkat harga tagihan-berdasarkan-lalu-lintas-per-jam sama dengan tingkat harga tagihan-berdasarkan-lalu-lintas-harian.Lihat [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/228/2949)


>! Untuk detail tentang penagihan nama domain ECDN, baca [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/570/37505).

## Ikhtisar Tagihan

### Divisi Area

Wilayah **inside the Chinese mainland** (di Tiongkok daratan) dan **outside the Chinese mainland** (di luar Tiongkok daratan) memiliki paket tagihan yang berbeda.

- Di Tiongkok daratan, biayanya sama untuk semua wilayah.

- Wilayah di luar Tiongkok daratan dibagi menjadi delapan area penagihan menurut lokasi server Tencent Cloud CDN, yaitu, Wilayah Asia Pasifik 1, Wilayah Asia Pasifik 2, Wilayah Asia Pasifik, Timur Tengah, Eropa, Amerika Utara, Amerika Selatan, dan Afrika, seperti gambar berikut:

|  Area   |                        Negara dan Wilayah yang Tercakup                        |
  | :-----: | :----------------------------------------------------: |
| Asia Pasifik 1 |        Hong Kong (Tiongkok), Makao (Tiongkok), Vietnam, Singapura, Thailand        |
| Asia Pasifik 2 |      Taiwan (Tiongkok), Jepang, Korea Selatan, Malaysia, Indonesia      |
| Asia Pasifik 3 |      Filipina, India, Australia, negara dan wilayah Asia Pasifik lainnya       |
|  Timur Tengah   |              Saudi Arabia, Uni Emirat Arab, Turki               |
|  Eropa   | Inggris, Jerman, Italia, Irlandia, Prancis, Belanda, Spanyol |
|  Amerika Utara   |                      Amerika Serikat, Kanada                      |
|  Amerika Selatan   |                          Brasil                          |
|  Afrika   |                          Africa Selatan                          |

>!
>
> Biaya layanan CDN untuk Tiongkok daratan dan wilayah di luar Tiongkok daratan ditagih secara terpisah berdasarkan harga satuan dan penggunaan yang sesuai.

### Cara Penagihan

|     Cara Penagihan      |                             Deskripsi                             |                           Pelunasan Tagihan                           |      Aturan Penagihan      |                           Referensi                           |
| :---------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------: | :----------------------------------------------------------: |
|     Tagihan-berdasarkan-bandwidth      | Biaya dikenakan berdasarkan bandwidth puncak harian.Nilai bandwidth dikumpulkan sekali setiap lima menit untuk menghasilkan total 288 poin statistik bandwidth per hari yang bandwidth puncak harian merupakan yang tertinggi.| Prinsipnya adalah bayar sesuai pemakaian setiap hari.Biaya tertagih antara 00.00.00 hingga 23.59.59 pada suatu hari akan ditagih sebelum 18.00 hari berikutnya.|    Tingkat   |  [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/228/2949) |
| Tagihan-berdasarkan-lalu-lintas-harian |          Biaya dikenakan berdasarkan lalu lintas harian aktual yang dihasilkan oleh simpul CDN Anda.| Prinsipnya adalah bayar sesuai pemakaian setiap hari.Biaya tertagih antara 00.00.00 hingga 23.59.59 pada suatu hari akan ditagih sebelum 18.00 hari berikutnya.| Tingkat kumulatif bulanan | [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/228/2949) |修改
| Tagihan-berdasarkan-lalu-lintas-per-jam (default) |        Biaya dikenakan berdasarkan lalu lintas per jam aktual yang dihasilkan oleh simpul CDN Anda.Prinsipnya adalah bayar sesuai pemakaian setiap jam.Biaya yang tertagih dalam satu jam akan ditagihkan dalam 2 hingga 4 jam berikutnya.| Tingkat kumulatif bulanan | [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/228/2949) |

### Paket penagihan pelanggan VIP

Jika konsumsi perkiraan atau aktual dari layanan CDN Anda melebihi USD 20.000, silakan hubungi tim penjualan Tencent Cloud untuk mendapatkan paket penagihan bulanan yang lebih fleksibel dan hemat biaya.

|    Cara Penagihan    |                             Deskripsi                             |                           Kasus Penggunaan                           |                           Referensi                           |
| :------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
| Rata-rata bandwidth puncak harian | Total 288 poin statistik bandwidth CDN dikumpulkan setiap hari, yang bandwidth puncak hariannya merupakan yang tertinggi.Kemudian poin bandwidth puncak harian dari seluruh hari-hari yang valid dalam sebulan dihitung untuk mendapatkan bandwidth puncak rata-rata, yaitu, nilai bandwidth yang dikenai tagihan.Terakhir, nilai hasil digunakan untuk penagihan berdasarkan harga dalam kontrak layanan Anda.| Jika konsumsi perkiraan atau aktual dari layanan CDN Anda melebihi USD 20.000, silakan hubungi tim penjualan Tencent Cloud.| [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/228/2949) |
|    Persentil ke-95 bulanan    | Total 288 poin statistik bandwidth CDN dikumpulkan setiap hari, lalu poin statistik dari seluruh hari-hari yang valid dalam sebulan (mulai dari hari ke-1) diurutkan secara menurun.Selanjutnya, poin 5% teratas dibuang.Terakhir, poin statistik dengan nilai tertinggi sisanya digunakan sebagai bandwidth untuk penagihan berdasarkan harga dalam kontrak layanan Anda.| Jika konsumsi perkiraan atau aktual dari layanan CDN Anda melebihi USD 20.000, silakan hubungi tim penjualan Tencent Cloud.| [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/228/2949) |
|     Lalu lintas bulanan     |       Lalu lintas yang dihasilkan dalam sebulan diakumulasi untuk penagihan berdasarkan harga dalam kontrak layanan Anda.| Jika konsumsi perkiraan atau aktual dari layanan CDN Anda melebihi USD 20.000, silakan hubungi tim penjualan Tencent Cloud. |                              /                               |

>!
>
> 
>
> - Setiap simpul CDN mengumpulkan data lalu lintas secara real time dan melaporkannya ke pusat penagihan yang mengagregasi entri data menjadi total data lalu lintas.Untuk tagihan-berdasarkan-bandwidth, nilai bandwidth dikumpulkan hingga sekecil 5 menit, yaitu, nilai bandwidth = total lalu lintas 5 menit / 300 d.Misalnya, jika total lalu lintas yang dihasilkan dalam 5 menit adalah 30 MB, maka bandwidth-nya adalah (30 * 8) / 300 = 0,8 Mbps (1 MB = 8 Mbps).
> - Konversi dasar:1 GB = 1.000 MB; 1 MB = 1.000 KB; 1 Gbps = 1.000 Mbps; 1 Mbps = 1.000 Kbps.

## Detail Penagihan



### Tagihan-berdasarkan-bandwidth-puncak

Bandwidth CDN mengadopsi **tiered pricing** (harga bertingkat) sebagai berikut:

| Tingkat Bandwidth (USD/Mbps/hari) | Tiongkok daratan (CN) | Amerika Utara (NA) | Eropa (EU) | Wilayah Asia Pasifik 1 (AP1) | Wilayah Asia Pasifik 2 (AP2) | Wilayah Asia Pasifik 3 (AP3) | Timur Tengah (ME) | Afrika (AA) | Amerika Selatan (SA) |
| :----------------------- | ------------- | :-------- | :-------- | :------------ | :------------ | :------------ | :-------- | :-------- | :-------- |
| 0 Mbps - 500 Mbps          | 0,0815         | 0,2069    | 0,2069    | 0,3647        | 0,3928        | 0,5140        | 0,7391    | 0,5612    | 0,5612    |
| 500 Mbps - 5 Gbps          | 0,0800         | 0,1964    | 0,1964    | 0,3216        | 0,3402        | 0,4679       | 0,6754   | 0,5137    | 0,5137    |
| 5 Gbps - 50 Gbps           | 0,0754         | 0,1491    | 0,1491    | 0,2703        | 0,2859        | 0,3828        | 0,6075    | 0,4702    | 0,4702    |
| ≥ 50 Gbps                 | 0,0738       | 0,1055    | 0,1055    | 0,2436        | 0,2545        | 0,3267           | 0,5301    | 0,4281       | 0,4281       |

>!
>
> Jika bandwidth puncak CDN Anda sebesar atau melebihi 50 Gbps, silakan [hubungi kami](https://intl.cloud.tencent.com/contact-sales) untuk informasi tentang diskon.

#### Metode penghitungan

Misalkan bandwidth puncak CDN di Tiongkok daratan adalah X dan tidak terjadi konsumsi di luar Tiongkok daratan, maka metode penghitungan untuk harga bertingkat adalah sebagai berikut:

1.Jika X < 500 Mbps, maka jumlah tagihan adalah X * 0,0815.
2.Jika 500 Mbps ≤ X < 5.000 Mbps, maka jumlah tagihan adalah X * 0,0800.
3.Jika 5.000 Mbps ≤ X < 50.000 Mbps, maka jumlah tagihan adalah X * 0,0754.
4.If X ≥ 50.000 Mbps, silakan hubungi kami untuk kontrak luring.Tersedia beberapa opsi diskon untuk Anda.

Anda dapat menggunakan [Kalkulator Harga](https://buy.cloud.tencent.com/calculator/cdn) untuk mendapatkan perkiraan harga.



### Tagihan-berdasarkan-lalu lintas (per jam dan harian)

Harga lalu lintas CDN didasarkan pada **monthly cumulative tier** (tingkat kumulatif bulanan) sebagai berikut:

| Tingkat Lalu LIntas(USD/GB) | Tiongkok daratan (CN) | Amerika Utara (NA) | Eropa (EU) | Wilayah Asia Pasifik 1 (AP1) | Wilayah Asia Pasifik 2 (AP2) | Wilayah Asia Pasifik 3 (AP3) | Timur Tengah (ME) | Afrika (AA) | Amerika Selatan (SA) |
| :------------------ | ------------- | :-------- | :-------- | :------------ | :------------ | :------------ | :-------- | :-------- | :-------- |
| 0 TB - 2 TB           | 0,0323         | 0,0452    | 0,0452    | 0,0665        | 0,0798        | 0,0897          | 0,1080    | 0,1039      | 0,1039      |
| 2 TB - 10 TB          | 0,0308         | 0,0378    | 0,0378    | 0,0592        | 0,0737        | 0,0780        | 0,1000    | 0,0970    | 0,0970    |
| 10 TB - 50 TB         | 0,0277         | 0,0319    | 0,0319    | 0,0533        | 0,0677        | 0,0723        | 0,0940    | 0,0907    | 0,0907    |
| 50 TB - 100 TB        | 0,0231         | 0,0261    | 0,0261    | 0,0475        | 0,0590        | 0,0654        | 0,0863    | 0,0842    | 0,0842    |
| ≥ 100 TB             | 0,0169          | 0,0200    | 0,0200    | 0,0446        | 0,0503        | 0,0577        | 0,0794    | 0,0781    | 0,0781    |

>!
>
> Jika lalu lintas CDN Anda sebesar atau melebihi 100 TB, silakan [hubungi kami](https://intl.cloud.tencent.com/contact-sales) untuk informasi tentang diskon.

#### Metode penghitungan

Berbeda dengan tagihan-berdasarkan-bandwidth, tagihan-berdasarkan-lalu-lintas didasarkan pada tingkat kumulatif bulanan.Berikut adalah contoh yang menjelaskan cara kerja tagihan-berdasarkan-lalu-lintas-harian:

- Seperti tampilan gambar di bawah, misalkan lalu lintas yang dihasilkan di Tiongkok daratan pada 1 Januari adalah 3 TB, dan tidak ada konsumsi di luar Tiongkok daratan.Zona abu-abu merupakan tingkat tagihan aktual dan zona hijau memperlihatkan lalu lintas yang dihasilkan pada 1 Januari.Karena 2 TB masuk dalam tingkat tagihan 0 TB - 2 TB dan 1 TB sisanya masuk dalam tingkat 2 TB - 10 TB, biaya aktual untuk 1 Januari adalah 2 * 1000 * 0,0323 + 1 * 1000 * 0,0308.
![img](https://mc.qcloudimg.com/static/img/bfdae242f6cca57421a65e46a96b0c67/image.png)
- Seperti ditunjukkan gambar berikut, misalkan lalu lintas yang dihasilkan di Tiongkok daratan pada 2 Januari adalah juga 3 TB, dan tidak ada konsumsi di luar Tiongkok daratan.Karena tagihan-berdasarkan-lalu-lintas didasarkan pada lalu lintas kumulatif bulanan, semua 3 TB masuk dalam tingkat 2 TB - 10 TB, maka biaya aktual untuk 2 Januari adalah 3 * 1000 * 0,0308.
![img](https://mc.qcloudimg.com/static/img/f62d1056c1c2cab249cec62ad6e74ddc/image.png)
- Seperti ditunjukkan gambar berikut, misalkan lalu lintas yang dihasilkan di Tiongkok daratan pada 3 Januari adalah 7 TB, dan tidak ada konsumsi di luar Tiongkok daratan.Dari 7 TB ini, 4 TB masuk dalam tingkat 2 TB - 10 TB dan 3 TB sisanya masuk dalam tingkat 10 TB - 50 TB, maka biaya aktual untuk 3 Januari adalah 4 * 1000 * 0,0308 + 3 * 1000 * 0,0277.
![img](https://mc.qcloudimg.com/static/img/954e2d483e31afd411f9a91ebd7f66c8/image.png)

Dengan cara ini, Anda dapat menghitung biaya untuk setiap hari dalam sebulan.Ketika masuk 1 Februari, konsumsi akan diakumulasi dari 0 untuk penghitungan tingkat.Anda dapat menggunakan [Kalkulator Harga](https://buy.cloud.tencent.com/calculator/cdn) untuk mendapatkan perkiraan harga.



### Tagihan-berdasarkan-rata-rata-bandwidth-puncak-harian

1.Misalkan penagihan CDN resmi dimulai pada 1 Januari dan harga kontrak adalah P USD/Mbps/bulan.
2.Satu hari valid merujuk pada hari ketika terjadi konsumsi lebih dari 0 Kbps bandwidth.
3.Misalkan ada 14 hari yang valid pada Januari, kami mengambil nilai maksimum dari 288 poin statistik untuk masing-masing dari 14 hari tersebut sebagai Maks_1, Maks_2, Maks_3…dan Maks_14, berturut-turut.Bandwidth yang dapat ditagih adalah Rata-rata (Maks_1, Maks_2, Maks_3…dan Maks_14) sehingga biaya untuk Januari adalah:Rata-rata (Maks_1, Maks_2, Maks_3…dan Maks_14) * P * 14 / 31.



### Tagihan-berdasarkan-bandwidth persentil ke-95 bulanan

1.Misalkan penagihan CDN resmi dimulai pada 1 Januari dan harga kontrak adalah P USD/Mbps/bulan.
2.Satu hari valid merujuk pada hari ketika terjadi konsumsi lebih dari 0 Kbps bandwidth.
3.Misalkan ada 14 hari yang valid pada Januari, maka 14 * 288 poin statistik akan dikumpulkan dan diurutkan secara menurun.5% poin statistik tertinggi dibuang sehingga Max95 merupakan poin tertinggi dalam poin statistik sisanya, yang merupakan bandwidth yang dikenai tagihan.Biaya untuk Januari adalah:Max95 * P * 14 / 31.

## Memilih Cara Penagihan

>!
>
> Jika Anda menyadari bahwa cara penagihan yang dipilih tidak cocok untuk kebutuhan bisnis Anda selama penggunaan, Anda dapat mengubahnya.Untuk informasi selengkapnya, silakan lihat [Mengubah Cara Penagihan](https://intl.cloud.tencent.com/document/product/228/32326).

**Opsi:**
CDN menyediakan dua cara penagihan: **bill-by-traffic** (tagihan-berdasarkan-lalu-lintas) dan **bill-by-bandwidth** (tagihan-berdasarkan-bandwidth).Anda dapat memilih cara penagihan sesuai kebutuhan.

**Calculation example** (Contoh perhitungan):
Misalkan konsumsi lalu lintas antara 00.00 hingga 23.59 kemarin adalah 200 GB, dan tidak ada konsumsi di wilayah di luar Tiongkok daratan.Bandwidth puncaknya adalah 40 Mbps seperti kurva berikut:
![img](https://mc.qcloudimg.com/static/img/3ecfe86a031782ebeaf0b1f7595cc69f/image.png)

Jika Anda memilih cara tagihan-berdasarkan-lalu-lintas, Anda akan membayar:200 * 0,037 = 7,4 USD

Jika Anda memilih cara tagihan-berdasarkan-bandwidth, Anda akan membayar:40 * 0,094 = 3,76 USD

Dalam contoh spesifik ini, tagihan-berdasarkan-bandwidth merupakan model penagihan yang lebih hemat.

## Pembayaran Terlambat

Untuk pembayaran terlambat, Tencent Cloud akan memberi tahu Anda melalui beberapa saluran termasuk email dan SMS.Tersedia masa tenggang 24 jam.Jika Anda tidak mengisi akun dalam 24 jam, layanan CDN Anda akan ditangguhkan.Setelah akun Anda diisi, status nama domain akan otomatis dipulihkan ke status sebelum penangguhan layanan (proses ini memakan waktu beberapa saat).

>!
>
> Ketika layanan akselerasi Anda ditangguhkan karena terlambat membayar, semua nama domain Anda akan dinonaktifkan dan semua permintaan akses akan diteruskan ke server asal.Anda dapat mengueri informasi, tetapi tidak dapat mengubah konfigurasi di konsol CDN.Nama dan konfigurasi domain terkait-CDN Anda akan dipertahankan selama 12 bulan.

