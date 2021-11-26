
## Ikhtisar Penagihan CBS[](id:CBS)
### Cara penagihan
Cloud Block Storage adalah layanan penyimpanan cloud yang dibayar sesuai pemakaian yang disediakan oleh Tencent Cloud.
Lihat tabel di bawah untuk detailnya.

| Paket penagihan | Bayar sesuai pemakaian |
|---------|---------|
| Metode pembayaran | Deposit biaya satu jam diperlukan pada saat pembelian.Layanan ini ditagih per jam. |
| Harga | USD/GB\*jam |
| Durasi penggunaan minimum | Ditagih per detik dan ditagih per jam.Anda dapat membeli atau melepaskan layanan kapan saja. |
| Kasus penggunaan | Layanan ini berlaku untuk skenario ketika permintaan bisnis sangat berfluktuasi, seperti penjualan kilat e-niaga. |

### Harga
Harga bervariasi berdasarkan wilayah dan jenis disk.Untuk informasi selengkapnya, lihat [Ikhtisar Harga](https://intl.cloud.tencent.com/document/product/362/2413).


## Ikhtisar Penagihan Snapshot[](id:Snapshot)
Layanan Snapshot **dikomersialkan** pada 22 Januari 2019 pukul 00:00:00.Semua snapshot ditagih berdasarkan penggunaan penyimpanan.
>! [Image](https://intl.cloud.tencent.com/document/product/213/4940) menggunakan layanan snapshot CBS untuk penyimpanan data.Akibatnya, mempertahankan image khusus menempati porsi tertentu dari kapasitas snapshot Anda dan menimbulkan biaya.

### Cara penagihan
Anda dikenakan biaya sesuai dengan total ukuran penyimpanan snapshot Anda.Setiap wilayah dikenakan biaya secara terpisah.CBS adalah **layanan yang dibayar sesuai pemakaian** pada siklus penagihan per jam.
>?Untuk melihat ukuran snapshot Anda di setiap wilayah, buka [Konsol Snapshot](https://console.cloud.tencent.com/cvm/snapshot/overview).
>





### Harga
Harga untuk snapshot bervariasi berdasarkan wilayah.Untuk informasi selengkapnya, lihat [Ikhtisar Harga](https://intl.cloud.tencent.com/document/product/362/2413).

### Tingkat gratis
Tencent Cloud menawarkan ruang penyimpanan gratis sebesar 50 GB untuk pengguna di Tiongkok Daratan.Perincian kebijakannya adalah sebagai berikut:
- Tingkat gratis tersedia untuk pengguna di wilayah seperti yang terdaftar di [Konsol Snapshot](https://console.cloud.tencent.com/cvm/snapshot/overview).
- Tingkat gratis ini akan dihapus pada Oktober 2021.

Tabel berikut menjelaskan cara penyimpanan snapshot ditagihkan dalam berbagai jenis keadaan:

<table>
<tr>
<th>Wilayah</th>
<th nowrap="nowrap">Total ukuran snapshot</th>
<th nowrap="nowrap">Jumlah disk cloud</th>
<th>Detail</th>
</tr>
<tr>
<td nowrap="nowrap">Tiongkok Utara (Beijing)</td>
<td>100 GB</td>
<td nowrap="nowrap">1 disk cloud</td>
<td>Memenuhi syarat untuk tingkat gratis sebesar 50 GB.Total ukuran penyimpanan snapshot yang dapat ditagih adalah 100 GB - 50 GB = 50 GB.</td>
</tr>
<tr>
<td nowrap="nowrap">Hong Kong, Makau dan Taiwan, Tiongkok (Hong Kong)</td>
<td>60 GB</td>
<td>2 disk cloud</td>
<td>Memenuhi syarat untuk tingkat gratis sebesar 50 GB.Total ukuran penyimpanan snapshot yang dapat ditagih adalah 60 GB - 50 GB = 10 GB.</td>
</tr>
<tr>
<td nowrap="nowrap">Asia Tenggara (Singapura)</td>
<td>40 GB</td>
<td>1 disk cloud</td>
<td>Tidak memenuhi syarat untuk tingkat gratis.Total ukuran penyimpanan snapshot yang dapat ditagih adalah 40 GB.</td>
</tr>
</table>

### Pembayaran yang lewat jatuh tempo
Setelah akun Anda jatuh tempo, snapshot akan masuk ke status **Isolated** (Terisolasi), dan layanan akan ditangguhkan.Untuk informasi selengkapnya, lihat [Kebijakan Jatuh Tempo](https://intl.cloud.tencent.com/document/product/362/31625).

