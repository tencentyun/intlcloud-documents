>?Produk ini sekarang mendukung permintaan harga dinamis dan estimasi biaya. Anda dapat menggunakan [Kalkulator Harga](https://intl.cloud.tencent.com/pricing/cdb) untuk memperkirakan biaya.

## Mode Penagihan

TencentDB for MySQL sekarang menawarkan mode penagihan berlangganan bulanan. Harga bayar sesuai pemakaian tetap tidak berubah.



TencentDB for MySQL mendukung penagihan terpisah untuk memori dan disk untuk memberi pengguna opsi yang lebih fleksibel.

Rumus harga instans: Harga Instans = Biaya memori + Biaya penyimpanan






## Fitur Lanjutan

### Kapasitas cadangan

Kapasitas cadangan tidak mendukung langganan bulanan. Harap lihat harga bayar sesuai pemakaian.

**Instance renewal management** (Manajemen perpanjangan instans)

Perpanjangan batch, perpanjangan otomatis, tanggal kedaluwarsa kolektif, bendera jangan-perbarui dapat ditemukan di halaman **Renewal Management** (Manajemen Perpanjangan).



**Instance upgrade cost formula** (Formula biaya peningkatan instans)

Misalkan sebuah instans kedaluwarsa dalam T hari, dan perbedaan biaya prabayar bulanan antara konfigurasi target dan konfigurasi saat ini adalah C, maka total biaya peningkatan adalah: T/30xC.

Misalnya Anda memiliki instans dengan 1 core, memori 1000 MB, dan disk 100 GB (biaya prabayar: 24,511 USD/bulan) dan akan kedaluwarsa dalam 15 hari. Jika Anda meningkatkannya ke 1 core, memori 1000 MB, dan disk 200 GB (biaya prabayar: 34,653 USD/bulan), maka total biaya peningkatan adalah: 15/30 x (34,653 - 24,511)=5.071 USD.



**Exceeding instance disk capacity limit** (Melebihi batas kapasitas disk instans)

Untuk memastikan kelangsungan bisnis, Anda perlu memutakhirkan spesifikasi instans Anda atau membeli kapasitas disk tambahan tepat waktu sebelum kapasitas disk habis.

Ketika ukuran data yang disimpan pada instans melebihi batas kapasitasnya, instans akan dikunci dan menjadi baca saja. Anda tidak akan dapat menulis data ke sana. Anda perlu memperluas kapasitasnya atau menghapus beberapa tabel database di konsol untuk membukanya.

Untuk menghindari database memicu status kunci berulang kali, instans terkunci akan dibuka kuncinya dan diizinkan untuk membaca dan menulis hanya jika kapasitas yang tersedia tersisa lebih dari 20% dari total kapasitasnya atau lebih dari 50 GB.



**Traffic synchronization fee for disaster recovery instances** (Biaya sinkronisasi lalu lintas untuk instans pemulihan bencana)

Sinkronisasi data untuk instans pemulihan bencana di TencentDB for MySQL saat ini gratis.

Kami akan memberi tahu pengguna ketika fitur ini dikomersialkan.

## Bayar sesuai Pemakaian

Model penetapan harga bertingkat bayar sesuai pemakaian didasarkan pada durasi penggunaan.

| Durasi Penggunaan | Harga Bertingkat |
|---------|---------|
| 0 jam < durasi 96 jam | Tarif Tingkat 1 berlaku |
| 96 jam < durasi 360 jam | Tarif Tingkat 2 berlaku |
| Durasi > 360 jam | Tarif Tingkat 3 berlaku |

### Harga instans

#### Rumus penagihan
**Total fees = memory fees + storage capacity fees + backup capacity fees + traffic fees (currently free)** (Total biaya = biaya memori + biaya kapasitas penyimpanan + biaya kapasitas cadangan + biaya lalu lintas (saat ini gratis))

#### Item yang dapat ditagih
<table>
<thead>
<tr>
<th width="15%">Item yang Dapat Ditagih</th>
<th>Catatan</th>
</tr>
</thead>
<tbody><tr>
<td>Biaya memori<br></td>
<td>Spesifikasi instans yang dipilih pada laman pembelian adalah bayar sesuai pemakaian dan mendukung penetapan harga bertingkat. Untuk detail harga, harap lihat <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">Harga Produk</a>.</td>
</tr>
<tr>
<td>Biaya kapasitas penyimpanan</td>
<td>Kapasitas disk yang dipilih pada halaman pembelian adalah bayar sesuai pemakaian. Untuk tetail harga, harap lihat <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">Harga Produk</a>.<br>Kapasitas akan penyimpanan menyimpan file data, tablespace bersama, log kesalahan, log ulang, log undo, kamus data, dan binlog yang diperlukan untuk TencentDB for MySQL.</tr>
<tr>
<td>Biaya kapasitas cadangan</td>
<td>TencentDB for MySQL menawarkan sejumlah kapasitas cadangan gratis berdasarkan wilayah, yang setara dengan jumlah kapasitas penyimpanan semua instans dua-node dan tiga-node (termasuk instans sumber) di wilayah Anda. <br>Untuk informasi selengkapnya tentang biaya untuk kapasitas cadangan yang berlebihan, lihat <a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">Penagihan Ruang Cadangan</a>.</td>
</tr>
<tr>
<td>Biaya lalu lintas</td>
<td>Biaya lalu lintas jaringan publik (saat ini gratis).</td>
</tr>
</tbody></table>


#### Harga bayar sesuai pemakaian

##### Edisi ketersediaan tinggi
<table>
  <td rowspan=2>Wilayah</td>
  <td colspan=3 >Memori (USD/GB/Jam)</td>
  <td rowspan=2 >Disk (USD/GB/Jam)</td>
 </tr>
 <tr  >
  <td >Tingkat 1</td>
  <td>Tingkat 2</td>
  <td>Tingkat 3</td>
 </tr>
 <tr  >
  <td>Guangzhou</td>
  <td class=xl65 align=right>0,0500</td>
  <td class=xl65 align=right>0,0400</td>
  <td class=xl65 align=right>0,0300</td>
  <td class=xl65 align=right>0,0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Qingyuan</td>
  <td class=xl65 align=right>0,0500</td>
  <td class=xl65 align=right>0,0400</td>
  <td class=xl65 align=right>0,0300</td>
  <td class=xl65 align=right>0,0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Shanghai</td>
  <td class=xl65 align=right>0,0500</td>
  <td class=xl65 align=right>0,0400</td>
  <td class=xl65 align=right>0,0300</td>
  <td class=xl65 align=right>0,0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Beijing</td>
  <td class=xl65 align=right>0,0500</td>
  <td class=xl65 align=right>0,0400</td>
  <td class=xl65 align=right>0,0300</td>
  <td class=xl65 align=right>0,0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Chengdu</td>
  <td class=xl65 align=right>0,0500</td>
  <td class=xl65 align=right>0,0400</td>
  <td class=xl65 align=right>0,0300</td>
  <td class=xl65 align=right>0,0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Chongqing</td>
  <td class=xl65 align=right>0,0500</td>
  <td class=xl65 align=right>0,0400</td>
  <td class=xl65 align=right>0,0300</td>
  <td class=xl65 align=right>0,0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Hong Kong (Tiongkok)</td>
  <td class=xl66 align=right>0,0688</td>
  <td class=xl65 align=right>0.0516</td>
  <td class=xl65 align=right>0.0344</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Taipei (Tiongkok)</td>
  <td class=xl65 align=right>0,0688</td>
  <td class=xl65 align=right>0,0516</td>
  <td class=xl65 align=right>0,0344</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Singapura</td>
  <td class=xl65 align=right>0,0705</td>
  <td class=xl65 align=right>0,0528</td>
  <td class=xl65 align=right>0,0352</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Bangkok</td>
  <td class=xl65 align=right>0,0556</td>
  <td class=xl65 align=right>0,0417</td>
  <td class=xl65 align=right>0,0278</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Mumbai</td>
  <td class=xl65 align=right>0,0556</td>
  <td class=xl65 align=right>0,0417</td>
  <td class=xl65 align=right>0,0278</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Seoul</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0,0417</td>
  <td class=xl65 align=right>0,0278</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Tokyo</td>
  <td class=xl65 align=right>0,0556</td>
  <td class=xl65 align=right>0,0417</td>
  <td class=xl65 align=right>0,0278</td>
  <td class=xl65 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Silicon Valley</td>
  <td class=xl65 align=right>0,0550</td>
  <td class=xl65 align=right>0,0413</td>
  <td class=xl65 align=right>0,0275</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Virginia</td>
  <td class=xl65 align=right>0,0444</td>
  <td class=xl65 align=right>0,0333</td>
  <td class=xl65 align=right>0,0222</td>
  <td class=xl65 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Toronto</td>
  <td class=xl65 align=right>0,0265</td>
  <td class=xl65 align=right>0,0199</td>
  <td class=xl65 align=right>0,0133</td>
  <td class=xl65 align=right>0,0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Frankfurt</td>
  <td class=xl65 align=right>0,0550</td>
  <td class=xl65 align=right>0,0413</td>
  <td class=xl65 align=right>0,0275</td>
  <td class=xl65 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>Moskow</td>
  <td class=xl65 align=right>0,0556</td>
  <td class=xl65 align=right>0,0417</td>
  <td class=xl65 align=right>0,0278</td>
  <td class=xl65 align=right>0,0003</td>
 </tr>
 </tr>
</table>

##### Instans baca saja

<table>
  <td rowspan=2>Wilayah</td>
  <td colspan=3 >Memori (USD/GB/Jam)</td>
  <td rowspan=2 >Disk (USD/GB/Jam)</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Tingkat 1</td>
  <td class=xl1529815>Tingkat 2</td>
  <td class=xl1529815>Tingkat 3</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Guangzhou</td>
  <td class=xl6529815 align=right>0,0250</td>
  <td class=xl6529815 align=right>0,0200</td>
  <td class=xl6529815 align=right>0,0150</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Qingyuan</td>
  <td class=xl6529815 align=right>0,0250</td>
  <td class=xl6529815 align=right>0,0200</td>
  <td class=xl6529815 align=right>0,0150</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Shanghai</td>
  <td class=xl6529815 align=right>0,0250</td>
  <td class=xl6529815 align=right>0,0200</td>
  <td class=xl6529815 align=right>0,0150</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Beijing</td>
  <td class=xl6529815 align=right>0,0250</td>
  <td class=xl6529815 align=right>0,0200</td>
  <td class=xl6529815 align=right>0,0150</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Chengdu</td>
  <td class=xl6529815 align=right>0,0250</td>
  <td class=xl6529815 align=right>0,0200</td>
  <td class=xl6529815 align=right>0,0150</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Chongqing</td>
  <td class=xl6529815 align=right>0,0250</td>
  <td class=xl6529815 align=right>0,0200</td>
  <td class=xl6529815 align=right>0,0150</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Hong Kong (Tiongkok)</td>
  <td class=xl6529815 align=right>0,0344</td>
  <td class=xl6529815 align=right>0,0258</td>
  <td class=xl6529815 align=right>0,0172</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Taipei (Tiongkok)</td>
  <td class=xl6529815 align=right>0,0344</td>
  <td class=xl6529815 align=right>0,0258</td>
  <td class=xl6529815 align=right>0,0172</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Singapura</td>
  <td class=xl6529815 align=right>0,0352</td>
  <td class=xl6529815 align=right>0,0264</td>
  <td class=xl6529815 align=right>0,0176</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Bangkok</td>
  <td class=xl6529815 align=right>0,0278</td>
  <td class=xl6529815 align=right>0,0208</td>
  <td class=xl6529815 align=right>0,0139</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Mumbai</td>
  <td class=xl6529815 align=right>0,0278</td>
  <td class=xl6529815 align=right>0,0208</td>
  <td class=xl6529815 align=right>0,0139</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Seoul</td>
  <td class=xl6529815 align=right>0,0278</td>
  <td class=xl6529815 align=right>0,0208</td>
  <td class=xl6529815 align=right>0,0139</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Tokyo</td>
  <td class=xl6529815 align=right>0,0278</td>
  <td class=xl6529815 align=right>0,0208</td>
  <td class=xl6529815 align=right>0,0139</td>
  <td class=xl6529815 align=right>0,0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Silicon Valley</td>
  <td class=xl6529815 align=right>0,0275</td>
  <td class=xl6529815 align=right>0,0206</td>
  <td class=xl6529815 align=right>0,0138</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Virginia</td>
  <td class=xl6529815 align=right>0,0222</td>
  <td class=xl6529815 align=right>0,0167</td>
  <td class=xl6529815 align=right>0,0111</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Toronto</td>
  <td class=xl6529815 align=right>0,0133</td>
  <td class=xl6529815 align=right>0,0099</td>
  <td class=xl6529815 align=right>0,0066</td>
  <td class=xl6529815 align=right>0,0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Frankfurt</td>
  <td class=xl6529815 align=right>0,0275</td>
  <td class=xl6529815 align=right>0,0206</td>
  <td class=xl6529815 align=right>0,0138</td>
  <td class=xl6529815 align=right>0,0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>Moskow</td>
  <td class=xl6529815 align=right>0,0278</td>
  <td class=xl6529815 align=right>0,0208</td>
  <td class=xl6529815 align=right>0,0139</td>
  <td class=xl6529815 align=right>0,0002</td>
 </tr>
</table>


## Contoh Penagihan
>?Harga yang digunakan dalam contoh berikut hanya untuk tujuan demonstrasi, yang dapat bervariasi tergantung pada wilayah, kampanye, atau kebijakan. Harap lihat halaman harga untuk harga aktual.
>

### Langganan bulanan
Misalnya:
- Anda membeli instans TencentDB for MySQL dengan ketersediaan tinggi yang berlangganan bulanan dengan 4 core, memori 8.000 MB, dan ruang disk 500 GB di Guangzhou Zone 3 selama 1 bulan.
- Anda membeli instans TencentDB for MySQL dengan ketersediaan tinggi yang berlangganan bulanan dengan 4 core, memori 8.000 MB, dan ruang disk 200 GB di Guangzhou Zone 4 selama 1 bulan.

Total biaya = biaya memori + biaya kapasitas penyimpanan + biaya kapasitas cadangan

##### Biaya memori dan biaya kapasitas penyimpanan
Rumus perhitungan:
Biaya memori + biaya kapasitas penyimpanan = 2 x 114,93 USD/bulan + (500 GB + 200 GB) x 0,1014 USD/GB/bulan x 1 bulan = 300,84 USD

##### Biaya kapasitas cadangan
Instans TencentDB for MySQL dengan ketersediaan tinggi di Zona Guangzhou 3 memiliki kapasitas penyimpanan 500 GB per bulan, dan instans di Zona Guangzhou 4 memiliki kapasitas penyimpanan 200 GB per bulan, sehingga Anda dapat memiliki kapasitas cadangan 700 GB secara gratis di wilayah Guangzhou setiap bulan.

Penggunaan kapasitas cadangan yang melebihi tingkat gratis dihitung per jam sesuai dengan aturan berikut. Misalnya, jika cadangan data Anda mencapai 800 GB dan cadangan log mencapai 100 GB, total penggunaan kapasitas cadangan Anda di Guangzhou akan melebihi 700 GB, dan kapasitas cadangan yang dapat ditagih per jam Anda akan menjadi 200 GB (800 + 100 - 700 = 200).

Biaya kapasitas cadangan (setiap jam) = 200 GB (penggunaan kapasitas cadangan yang melebihi tingkat gratis dapat berubah seiring waktu) x 0,000127 USD/GB/jam

### Bayar sesuai pemakaian
Misalnya Anda membeli instans TencentDB for MySQL bayar sesuai penggunaan dengan 4 core, memori 8.000 MB, dan ruang disk 500 GB di wilayah Guangzhou selama 400 jam.
Biaya tingkat 1: (0,0250 USD/GB/jam * 8 GB + 500 GB * 0,0003) * 96 jam = 33,6 USD
Biaya tingkat 2: (0,0200 USD/GB/jam * 8 GB + 500 GB * 0,0003) * 264 jam = 81,84 USD
Biaya tingkat 3: (0,0150 USD/GB/jam * 8 GB + 500 GB * 0,0003) * 40 jam = 10,8 USD
Biaya instans = Biaya tingkat 1 + Biaya tingkat 2 + Biaya tingkat 3 = 126,24 USD

## Pertanyaan Umum
#### Mengapa dikenakan biaya tambahan untuk instans langganan bulanan saya?
Penggunaan kapasitas cadangan yang melebihi tingkat gratis akan dikenakan biaya. Harap periksa apakah penggunaan kapasitas cadangan Anda melebihi tingkat gratis.
Anda dapat memeriksa penggunaan kapasitas cadangan di halaman **Database Backup** (Cadangan Database) di [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb/backup). Untuk informasi selengkapnya tentang harga kapasitas cadangan, harap lihat [Penagihan Ruang Cadangan](https://intl.cloud.tencent.com/document/product/236/32344).

#### Apakah Tencent Cloud akan mengenakan biaya untuk instans bayar sesuai pemakaian jika tidak digunakan?
Ya. Jika Anda berhenti menggunakan sumber daya bayar sesuai penggunaan, harap hentikan sumber daya tersebut sesegera mungkin untuk menghindari biaya lebih lanjut.

#### File apa yang disimpan dalam kapasitas penyimpanan?

- File data: ruang yang digunakan data Anda, termasuk tabel dan indeks yang dibuat
- File sistem (diperlukan untuk database): ruang tabel bersama, log kesalahan, log ulang, log undo, dan kamus data
- Binlog: binlog merekam semua pernyataan DDL dan DML (kecuali pernyataan SELECT dan SHOW) dan digunakan untuk mereplikasi dan memulihkan data database. Semakin banyak data berubah, semakin banyak binlog. Untuk mengurangi ruang binlog, mereka dapat diunggah ke COS.

## Dokumentasi
- Anda dapat membeli instans TencentDB for MySQL melalui konsol atau API. Untuk informasi selengkapnya, harap lihat [Metode Pembelian](https://intl.cloud.tencent.com/document/product/236/5160).
- TencentDB for MySQL mengirimkan pesan peringatan kepada Anda sebelum kedaluwarsa dan sumber dayanya diambil alih. Untuk informasi selengkapnya, harap lihat [Pembayaran Jatuh Tempo](https://intl.cloud.tencent.com/document/product/236/5159).
- Anda dapat mengembalikan instans TencentDB for MySQL dan meminta pengembalian dana. Untuk informasi selengkapnya, harap lihat [Pengembalian Dana](https://intl.cloud.tencent.com/document/product/236/14618).
- Anda dapat menyesuaikan instans TencentDB for MySQL ke spesifikasi yang lebih tinggi atau lebih rendah. Untuk informasi selengkapnya, harap lihat [Biaya Penyesuaian Instans](https://intl.cloud.tencent.com/document/product/236/32345).
