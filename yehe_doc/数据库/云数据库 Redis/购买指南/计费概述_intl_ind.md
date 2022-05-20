## Mode Penagihan
>? Langganan bulanan saat ini dalam versi beta. Dokumen harga ini hanya untuk referensi, lihat tagihan Anda untuk harga yang sebenarnya. Jika Anda ingin menggunakan opsi penagihan ini, silakan [hubungi penjualan](https://intl.cloud.tencent.com/contact-sales).
>
- TencentDB for Redis mengadopsi strategi penetapan harga linier, dan biaya untuk instans dihitung dengan mengalikan spesifikasi instans dengan harga satuan.
- TencentDB for Redis menyediakan dua opsi penagihan, bayar sesuai pemakaian dan langganan bulanan.
- Untuk bayar sesuai pemakaian, waktu penggunaan yang dapat ditagih akurat hingga detik, dengan harga satuan = harga bulanan / 30 hari / 24 jam / 3600 detik.



### Bayar sesuai pemakaian

TencentDB for Redis mendukung penetapan harga bertingkat. Makin lama Anda menggunakannya, makin banyak Anda menghemat.
Model penetapan harga bertingkat bayar sesuai pemakaian didasarkan pada durasi penggunaan.

- 0 hari < durasi 4 hari: Berlaku harga bayar sesuai pemakaian Tier 1, dengan harga per jam = harga bulanan / 30/24 * 2
- 4 hari < durasi ≤ 15 hari: Berlaku harga bayar sesuai pemakaian Tier 2, dengan harga per jam = harga bulanan / 30/24 * 1,5
- Durasi > 15 hari: Berlaku harga bayar sesuai pemakaian Tier 3, dengan harga per jam = harga bulanan / 30 / 24

| Konfigurasi | USD/GB/Jam | USD/GB/Bulan | Wilayah |
| :------ | :----------- | :--------- | :-------------------------------- |
| 1 GB MEM | 0.034704 | 24.98688 | Beijing, Shanghai, Guangzhou, Chengdu, dan Chongqing |
| 1 GB MEM | 0.029196 | 21.02112 | Pantai Timur AS (Virginia), dan Pantai Barat (Silicon Valley) |
| 1 GB MEM | 0.036108 | 25.99776 | Hong Kong (Tiongkok) dan Singapura |
| 1 GB MEM | 0.045792 | 32.97024 | Mumbai |
| 1 GB MEM | 0.037512 | 27.00864 | Seoul |
| 1 GB MEM | 0.041688 | 30.01536 | Frankfurt |
| 1 GB MEM | 0.024984 | 17.98848 | Moskow |
| 1 GB MEM | 0.045792 | 32.97024 | Bangkok |
| 1 GB MEM | 0.026388 | 18.99936 | Tokyo |
| 1 GB MEM | 0.050004 | 36.00288 | Amerika Utara |

> Catatan:
>
> Harga kembali ke tier 1 untuk instans yang diskalakan atau terisolasi.

### Langganan bulanan

Pembayaran di muka diperlukan untuk instans langganan bulanan.

Untuk detail harga spesifik, silakan lihat [Harga Produk](http://intl.cloud.tencent.com/document/product/583/12281)
