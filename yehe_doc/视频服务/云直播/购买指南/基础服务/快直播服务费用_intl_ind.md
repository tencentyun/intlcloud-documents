## Ikhtisar

- Mode penagihan: **Bayar sesuai pemakaian harian**
- Siklus penagihan: Siklus penagihan harian. Pemotongan akumulasi biaya lalu lintas dalam satu hari tertentu dilakukan pada hari berikutnya. Informasi seputar pemotongan biaya aktual dan waktu pembuatan tagihan dapat dilihat di laporan tagihan Anda.
- Wilayah penagihan di luar Tiongkok Daratan:
  - Asia Pasifik 1: Hong Kong (Tiongkok), Singapura, Makau (Tiongkok), Vietnam, Thailand, Nepal, Kamboja
  - Asia Pasifik 2: Taiwan (Tiongkok), Jepang, Malaysia, Indonesia, Korea Selatan
  - Asia Pasifik 3: Filipina, India, Australia
  - Amerika Utara: Amerika Serikat, Kanada, Meksiko
  - Eropa: Belanda, Jerman, Rusia, Britania Raya, Irlandia, Italia, Spanyol, Prancis
  - Timur Tengah: Uni Emirat Arab, Turki, Qatar, Arab Saudi, Bahrain
  - Afrika: Afrika Selatan
  - Amerika Selatan: Brasil, Kolombia
- Faktor konversi untuk unit lalu lintas/bandwidth adalah 1.000. Misalnya, 1 TB = 1.000 GB.
- Hari layanan CSS adalah pukul 00.00‒23.59 (UTC+08.00).
- Karena LEB menggunakan saluran dengan latensi ultra-rendah, biaya lalu lintas//bandwidth LEB sedikit lebih tinggi daripada biaya lalu lintas/bandwidth LVB.
- LEB tidak mendukung streaming langsung dengan B-frame. Jika streaming yang di-push mengandung B-frame, sistem akan menghapus B-frame dalam transcoding sehingga biaya transcoding akan dikenakan.
- Pemutaran ulang menggunakan browser hanya mendukung protokol WebRTC standar dan tidak mendukung AAC. Jika streaming yang di-push mengandung audio dalam format AAC, sistem akan melakukan transcoding audio ke dalam format Opus sehingga biaya transcoding audio akan dikenakan.
- **Mulai pukul 00.00 (UTC+08.00), 4 Januari 2022**, CSS telah menyesuaikan harga tagihan harian dan tingkat harga layanan dasar LEB serta penggunaan yang dikenai tagihan di luar Tiongkok Daratan berdasarkan wilayah, bukan berdasarkan harga gabungan. Keterangan terperinci dapat dilihat di [Notice: CSS to Adjust Prices of Basic Services (Pemberitahuan: CSS Menerapkan Penyesuaian Harga Layanan Dasar)](https://intl.cloud.tencent.com/document/product/267/43055).

>! 
> - Secara default, biaya ditagihkan berdasarkan penggunaan downstream. Akan tetapi, penggunaan upstream juga akan dikenai tagihan jika rasio penggunaan upstream terhadap penggunaan downstream lebih besar dari 1:10 dan bandwidth upstream tertinggi yang digunakan dalam satu hari melampaui 100 Mbps.
>- **Metode penagihan, aturan harga bertingkat, dan wilayah penagihan yang sama (di dalam/di luar Tiongkok Daratan)** digunakan untuk push langsung dan [pemutaran ulang LVB](https://intl.cloud.tencent.com/document/product/267/2818). **Penagihan untuk push langsung telah dimulai sejak pukul 00.00 (UTC+08.00), 1 Juli 2021**.
>- Contoh penagihan:
Contoh tagihan berdasarkan lalu lintas harian. Misalnya, total lalu lintas upstream dan total lalu lintas downstream yang digunakan dalam sehari secara berturut-turut adalah 10 GB dan 90 GB, dan bandwidth upstream tertinggi yang digunakan adalah 101 Mbps. Karena rasio penggunaan upstream terhadap penggunaan downstream adalah 10:90, yang berarti lebih besar dari 1:10, dan penggunaan bandwidth upstream puncak melebihi 100 Mbps, biaya lalu lintas dihitung sebagai berikut:
Biaya lalu lintas upstream + Biaya lalu lintas downstream = 0,0417 (USD/GB/Hari) x (10 (GB) + 90 (GB)) = 4,17 USD.



[](id:overseas)
## Akselerasi di Luar Tiongkok Daratan

Penggunaan Lalu Lintas/Bandwidth di luar Tiongkok Daratan didefinisikan sebagai lalu lintas/bandwidth downstream yang terpakai ketika pengguna melakukan koneksi ke server asal akselerasi Tencent Cloud di luar Tiongkok Daratan. Anda dapat memilih penagihan [per lalu lintas](#overseas_flow) atau [per bandwidth](#overseas_bandwidth). Penagihan per lalu lintas secara default digunakan untuk pengguna baru.

>! Aturan tagihan LEB berdasarkan lalu lintas/bandwidth untuk wilayah di luar Tiongkok Daratan berlaku efektif pada tanggal 20 April 2021. Sejak tanggal 21 April 2021, semua tagihan telah dibuat menurut aturan penagihan yang baru.

[](id:overseas_flow)
### Tagihan berdasarkan lalu lintas

#### Harga
Untuk lalu lintas di luar Tiongkok Daratan, kami melakukan penagihan per wilayah secara harian dan menggunakan pendekatan harga bertingkat. Informasi lebih lanjut tentang tingkat harga dapat dilihat di bawah:

<table>
<thead>
<tr>
<th rowspan=2>Tingkat Lalu Lintas</th>
<th colspan=8 style="text-align:center;">Harga (USD/GB/Hari)</th>
</tr>
<tr>
<th>Asia Pasifik 1</th>
<th>Asia Pasifik 2</th>
<th>Asia Pasifik 3</th>
<th>Amerika Utara</th>
<th>Eropa</th>
<th>Timur Tengah</th>
<th>Afrika</th>
<th>Amerika Selatan</th>
</tr>
</thead>
<tbody>
<tr>
<td>0‒2 TB</td>
<td>0,1496</td>
<td>0,2472</td>
<td>0,2276</td>
<td>0,1431</td>
<td>0,1431</td>
<td>0,3902</td>
<td>0,3902</td>
<td>0,3350</td>
</th>
<tr>
<td>2 TB (inklusif)‒50 TB</td>
<td>0,1398</td>
<td>0,2276</td>
<td>0,2081</td>
<td>0,1268</td>
<td>0,1268</td>
<td>0,3577</td>
<td>0,3577</td>
<td>0,3187</td>
</tr>
<tr>
<td>50 TB (inklusif)‒100 TB</td>
<td>0,1171</td>
<td>0,2114</td>
<td>0,1821</td>
<td>0,1008</td>
<td>0,1008</td>
<td>0,3350</td>
<td>0,3350</td>
<td>0,2927</td>
</tr>
<tr>
<td>100 TB (inklusif)‒1 PB</td>
<td>0,1008</td>
<td>0,1821</td>
<td>0,1626</td>
<td>0,0650</td>
<td>0,0650</td>
<td>0,3089</td>
<td>0,3089</td>
<td>0,2764</td>
</tr>
<tr>
<td>≥ 1 PB</td>
<td>0,0911</td>
<td>0,1691</td>
<td>0,1431</td>
<td>0,0520</td>
<td>0,0520</td>
<td>0,2764</td>
<td>0,2764</td>
<td>0,2602</td>
</tr>
</tbody></table>


#### Detail
- Item yang dapat dikenai tagihan: Lalu lintas downstream yang dipakai selama pemutaran ulang LEB di luar Tiongkok Daratan
- Aturan penagihan: Biaya dihitung dengan mengalikan total lalu lintas yang digunakan dalam sehari di suatu wilayah penagihan dengan harga unit di tingkat yang sesuai.

#### Contoh penagihan
- Misalnya, sesi LEB berlangsung selama 1 jam dengan bitrate 500 Mbps (Angka ini merupakan jumlah bitrate audio dan bitrate video. Jika Anda mengaktifkan transcoding dan menetapkan bitrate video, jumlah bitrate audio dan bitrate video yang sudah ditetapkan akan digunakan untuk penagihan). Jika sesi tersebut ditonton oleh 100 pemirsa, besarnya lalu lintas yang terpakai adalah: 500/8 x 3600 x 100 = 22.500.000 KB = 22,5 GB.
- Misalnya, Anda menggunakan layanan LEB pada tanggal 4 Januari 2022 dan menggunakan lalu lintas downstream sebesar 22,5 GB. Pada 5 Januari 2022, Anda akan dikenai tagihan sebesar:
  0,1496 (USD/GB) x 22,5 (GB) = 3,366 USD.
- Secara default, biaya ditagihkan berdasarkan penggunaan downstream. Akan tetapi, penggunaan upstream juga akan dikenai tagihan jika rasio penggunaan upstream terhadap penggunaan downstream lebih besar dari 1:10 dan bandwidth upstream tertinggi yang digunakan dalam satu hari melampaui 100 Mbps. Mode penagihan, harga daftar, dan aturan harga bertingkat yang sama berlaku untuk penggunaan upstream LEB dan penggunaan downstream LVB.

[](id:overseas_bandwidth)
### Tagihan berdasarkan bandwidth

#### Harga

Untuk penggunaan bandwidth di luar Tiongkok Daratan, kami melakukan penagihan per wilayah secara harian dan menggunakan pendekatan harga bertingkat. Anda akan dikenai tagihan atas penggunaan bandwidth puncak dalam satu hari. Informasi lebih lanjut tentang tingkat harga dapat dilihat di bawah:

<table>
<thead>
<tr>
<th rowspan=2>Tingkat Bandwidth</th>
<th colspan=8 style="text-align:center;">Harga (USD/Mbps/Hari)</th>
</tr>
<tr>
<th>Asia Pasifik 1</th>
<th>Asia Pasifik 2</th>
<th>Asia Pasifik 3</th>
<th>Amerika Utara</th>
<th>Eropa</th>
<th>Timur Tengah</th>
<th>Afrika</th>
<th>Amerika Selatan</th>
</tr>
</thead>
<tbody>
<tr>
<td>0‒500 Mbps</td>
<td>0,4098</td>
<td>1,2033</td>
<td>1,2455</td>
<td>0,3967</td>
<td>0,3967</td>
<td>1,8667</td>
<td>1,8667</td>
<td>1,6911</td>
</tr>
<tr>
<td>500 Mbps (inklusif)‒5 Gbps</td>
<td>0,3707</td>
<td>1,0829</td>
<td>1,2098</td>
<td>0,3610</td>
<td>0,3610</td>
<td>1,8407</td>
<td>1,8407</td>
<td>1,6553</td>
</tr>
<tr>
<td>5 Gbps (inklusif)‒20 Gbps</td>
<td>0,3415</td>
<td>0,9659</td>
<td>1,1122</td>
<td>0,3363</td>
<td>0,3363</td>
<td>1,8016</td>
<td>1,8016</td>
<td>1,6130</td>
</tr>
<tr>
<td>≥ 20 Gbps</td>
<td>0,3252</td>
<td>0,8455</td>
<td>1,0081</td>
<td>0,3187</td>
<td>0,3187</td>
<td>1,7821</td>
<td>1,7821</td>
<td>1,5935</td>
</tr>
</tbody></table>


#### Detail
- Item yang dapat dikenai tagihan: Bandwidth downstream yang digunakan selama pemutaran ulang LEB di luar Tiongkok Daratan
- Aturan penagihan: Biaya dihitung dengan mengalikan bandwidth tertinggi yang digunakan dalam sehari di suatu wilayah penagihan dengan harga unit di tingkat yang sesuai.

#### Contoh penagihan
- Misalnya, suatu sesi LEB memiliki bitrate 500 Kbps (Angka ini adalah jumlah bitrate audio dan bitrate video. Jika Anda mengaktifkan transcoding dan menetapkan bitrate video, jumlah bitrate audio dan bitrate video yang sudah ditetapkan akan digunakan untuk penagihan), dan jumlah maksimum pemirsa yang menonton bersamaan adalah 100 orang, bandwidth tertinggi yang digunakan adalah sebagai berikut:
   500 Kbps × 100 = 50.000 Kbps = 50 Mbps.
- Misalnya, Anda menggunakan layanan LEB pada 4 Januari 2022 untuk pemutaran ulang di Makau (Tiongkok) dan penggunaan bandwidth tertinggi Anda mencapai 50 Mbps. Pada 5 Januari 2022, Anda akan dikenai tagihan sebesar:
   0,4098 (USD/Mbps/Hari) x 50 (Mbps) = 20,49 USD.
- Secara default, biaya ditagihkan berdasarkan penggunaan downstream. Akan tetapi, penggunaan upstream juga akan dikenai tagihan jika rasio penggunaan upstream terhadap penggunaan downstream lebih besar dari 1:10 dan bandwidth upstream tertinggi yang digunakan dalam satu hari melampaui 100 Mbps. Mode penagihan, harga daftar, dan aturan harga bertingkat yang sama berlaku untuk penggunaan upstream LEB dan penggunaan downstream LVB.

[](id:domestic)

## Penggunaan Lalu Lintas/Bandwidth di Tiongkok Daratan

Layanan LEB dikenai tagihan berdasarkan lalu lintas/bandwidth downstream yang digunakan selama streaming langsung.
LEB menyediakan dua mode penagihan bayar-sesuai-pemakaian harian: [tagihan berdasarkan lalu lintas](#flow) dan [tagihan berdasarkan bandwidth](#bandwidth). Anda dapat memilih sesuai dengan kebutuhan. **Mode default untuk pengguna baru LEB adalah tagihan berdasarkan lalu lintas.**

[](id:flow)

### Tagihan berdasarkan lalu lintas

#### Harga

Untuk lalu lintas LEB, kami melakukan penagihan per hari dan menggunakan pendekatan harga bertingkat. Informasi lebih lanjut tentang tingkat harga dapat dilihat di bawah:

| Tingkat Lalu Lintas | Harga (USD/GB/Hari) |
| ----------------- | ---------------- |
| 0‒2 TB           | 0,0846           |
| 2 TB (inklusif)‒10 TB   | 0,0813           |
| 10 TB (inklusif)‒50 TB   | 0,0780                                  |
| 50 TB (inklusif)‒100 TB | 0,0715           |
| 100 TB (inklusif)‒1 PB | 0,0618           |
| ≥ 1 PB             | 0,0520           |

#### Detail

- Item yang dapat dikenai tagihan: Lalu lintas downstream yang terpakai selama pemutaran ulang LEB di Tiongkok Daratan
- Aturan penagihan: Biaya dihitung dengan mengalikan total lalu lintas yang digunakan dalam sehari dengan harga unit di tingkat yang sesuai.

#### Contoh penagihan

- Misalnya, sesi LEB berlangsung selama 1 jam dengan bitrate 500 Mbps (Angka ini merupakan jumlah bitrate audio dan bitrate video. Jika Anda mengaktifkan transcoding dan menetapkan bitrate video, jumlah bitrate audio dan bitrate video yang sudah ditetapkan akan digunakan untuk penagihan). Jika sesi tersebut ditonton oleh 100 pemirsa, besarnya lalu lintas yang terpakai adalah: 500/8 x 3600 x 100 = 22.500.000 KB = 22,5 GB.
- Misalnya, Anda menggunakan layanan LEB pada tanggal 4 Januari 2022 dan menggunakan lalu lintas downstream sebesar 22,5 GB. Pada 5 Januari 2022, Anda akan dikenai tagihan sebesar:
  0,0846 (USD/GB) x 22,5 (GB) = 1,9035 USD.
- Secara default, biaya ditagihkan berdasarkan penggunaan downstream. Akan tetapi, penggunaan upstream juga akan dikenai tagihan jika rasio penggunaan upstream terhadap penggunaan downstream lebih besar dari 1:10 dan bandwidth upstream tertinggi yang digunakan dalam satu hari melampaui 100 Mbps. Mode penagihan, harga daftar, dan aturan harga bertingkat yang sama berlaku untuk penggunaan upstream LEB dan penggunaan downstream LVB.

[](id:bandwidth)

### Tagihan berdasarkan bandwidth

#### Harga

Untuk penggunaan bandwidth LEB, kami melakukan penagihan per hari dan menggunakan pendekatan harga bertingkat. Anda akan dikenai tagihan atas penggunaan bandwidth puncak dalam satu hari. Informasi lebih lanjut tentang tingkat harga dapat dilihat di bawah:

| Tingkat Bandwidth | Harga (USD/Mbps/Hari) |
| -------------------- | ------------------ |
| 0‒500 Mbps          | 0,2114             |
| 500 Mbps (inklusif)‒5 Gbps | 0,2049             |
| 5 Gbps (inklusif)‒20 Gbps  | 0,1984             |
| ≥ 20 Gbps             | 0,1886             |

#### Detail

- Item yang dapat dikenai tagihan: Bandwidth downstream yang digunakan selama pemutaran ulang LEB di Tiongkok Daratan
- Aturan penagihan: Biaya dihitung dengan mengalikan bandwidth tertinggi yang digunakan dalam sehari dengan harga unit di tingkat yang sesuai.

#### Contoh penagihan

- Misalnya, suatu sesi LEB memiliki bitrate 500 Kbps (Angka ini adalah jumlah bitrate audio dan bitrate video. Jika Anda mengaktifkan transcoding dan menetapkan bitrate video, jumlah bitrate audio dan bitrate video yang sudah ditetapkan akan digunakan untuk penagihan), dan jumlah maksimum pemirsa yang menonton bersamaan adalah 100 orang, bandwidth tertinggi yang digunakan adalah sebagai berikut:
   500 Kbps × 100 = 50.000 Kbps = 50 Mbps.
- Misalnya, Anda menggunakan layanan LEB pada tanggal 4 Januari 2022 dan penggunaan bandwidth maksimum Anda mencapai 50 Mbps. Pada 5 Januari 2022, Anda akan dikenai tagihan sebesar:
   0,2114 (USD/Mbps/Hari) x 50 (Mbps) = 10,57 USD.
- Secara default, biaya ditagihkan berdasarkan penggunaan downstream. Akan tetapi, penggunaan upstream juga akan dikenai tagihan jika rasio penggunaan upstream terhadap penggunaan downstream lebih besar dari 1:10 dan bandwidth upstream tertinggi yang digunakan dalam satu hari melampaui 100 Mbps. Mode penagihan, harga daftar, dan aturan harga bertingkat yang sama berlaku untuk penggunaan upstream LEB dan penggunaan downstream LVB.

>? Jika Anda memiliki bisnis streaming langsung skala besar, mode penagihan harian mungkin tidak memenuhi kebutuhan Anda. Silakan [hubungi](https://intl.cloud.tencent.com/contact-us) tim penjualan Tencent Cloud atau [kirimkan tiket](https://console.cloud.tencent.com/workorder/category) untuk mengetahui opsi penagihan lainnya.

