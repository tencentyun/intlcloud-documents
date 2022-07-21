Untuk melihat perincian tagihan dan pembayaran CSS, buka **Billing Center** > **Bills** > **[Bill Details](https://console.cloud.tencent.com/expense/bill/summary)** (Pusat Penagihan > Tagihan > Detail Tagihan) di konsol Tencent Cloud.
Halaman Bill Details (Detail Tagihan) berisi tab **Bill by Instance** (Tagihan Berdasarkan Instans) dan tab **Bill Details** (Detail Tagihan):
- Bill by Instance (Tagihan Berdasarkan Instans): menampilkan tagihan agregat per instans.
- Bill Details (Detail Tagihan): menampilkan satu rekaman berdasarkan tagihan tanpa melakukan agregasi.
<span id="resources_id"></span>
## Tagihan Berdasarkan Instans
1. Klik tab **Bill by Instance** (Tagihan Berdasarkan Instans).
2. Klik **All products** (Semua produk), lalu pilih **Cloud Streaming Services** untuk melihat tagihan CSS.

![](https://main.qcloudimg.com/raw/9db167f7285dfaf82d83a9028d589ad8.png)

#### Bidang tagihan

<table>
<thead>
<tr>
<th>Bidang</th>
<th>Deskripsi</th>
</tr>
</thead>
<tbody><tr>
<td>Jenis transaksi</td>
<td><ul style="margin:0;">
    <li>Siklus tagihan harian: biaya dipotong setiap hari</li>
    <li>Siklus tagihan bulanan: biaya dipotong setiap bulan</li>
    </td>
</tr>
<tr>
<td>Deskripsi konfigurasi</td>
<td>Subfitur CSS dan penggunaannya dalam bulan ini. Subfitur CSS meliputi: <ul style="margin:0;">
    <li>Transcoding langsung</li>
    <li>Perekaman langsung</li>
    <li>Pengambilan tangkapan layar langsung</li>
    <li>Deteksi pornografi</li>
    </ul></td>
</tr>
<tr>
<td>Harga awal</td>
<td>Total biaya subfitur yang digunakan pada bulan ini</td>
</tr>
<tr>
<td>Nilai diskon</td>
<td>Nilai diskon pengguna bulan ini: Pengguna dengan siklus penagihan harian tidak mendapatkan diskon. Nilai diskon pengguna tersebut adalah 1.</td>
</tr>
<tr>
<td>Total biaya</td>
<td>Total biaya = Harga awal × (1 - Nilai diskon)</td>
</tr>
</tbody></table>

>? Bidang-bidang lain ditetapkan oleh Tencent Cloud. Informasi selengkapnya dapat dilihat di [Bills (Tagihan)](https://intl.cloud.tencent.com/document/product/555/7432).
<span id="detail"></span>
## Detail Tagihan
1. Klik tab **Bill Details** (Detail Tagihan).
2. Klik **All products** (Semua produk), lalu pilih **Cloud Streaming Services** untuk melihat detail tagihan CSS.

![](https://main.qcloudimg.com/raw/0716954d4d5a955a77acd4149961ca1b.png)

#### Bidang tagihan

| Bidang     | Deskripsi                                                         |
| :--------- | :----------------------------------------------------------- |
| Component type (Jenis komponen)  | Subfitur CSS yang digunakan dalam bulan ini                        |
| Component name (Nama komponen)  | Sub-item dalam jenis komponen ini                                 |
| Component list price (Harga komponen dalam daftar harga) | Harga unit yang dipublikasikan komponen tanpa diskon                    |
| Component usage (Penggunaan komponen)   | Penggunaan komponen                                             |
| Discount rate (Nilai diskon)    | Diskon pengguna bulan ini: pengguna dengan siklus penagihan harian tidak mendapatkan diskon. Nilai diskon pengguna tersebut adalah 0. Pengguna dengan siklus penagihan bulanan dapat menghubungi tim penjualan untuk bertanya seputar cara menerima diskon |
| Durasi penggunaan   | Total durasi penggunaan komponen    |
| Total biaya    | Total biaya = Harga awal komponen x (1 - Nilai diskon). Harga awal komponen = Harga unit yang dipublikasikan komponen x Durasi penggunaan |

>?Bidang-bidang lain ditetapkan oleh Tencent Cloud. Informasi selengkapnya dapat dilihat di [Bills (Tagihan)](https://intl.cloud.tencent.com/document/product/555/7432).
