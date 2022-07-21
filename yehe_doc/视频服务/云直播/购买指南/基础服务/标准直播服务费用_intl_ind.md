## Ikhtisar

- Mode penagihan: Bayar sesuai pemakaian harian
- Siklus penagihan: Siklus penagihan harian. Pemotongan akumulasi biaya lalu lintas dalam satu hari tertentu dilakukan pada hari berikutnya. Informasi seputar pemotongan biaya aktual dan waktu pembuatan tagihan dapat dilihat di laporan tagihan Anda.
- **Mode default untuk pengguna baru LVB adalah tagihan berdasarkan lalu lintas.**
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
- **Mulai pukul 00.00 (UTC+08.00), 4 Januari 2022**, CSS telah menyesuaikan harga tagihan harian dan tingkat harga layanan dasar LVB serta penggunaan yang dikenai tagihan di luar Tiongkok Daratan berdasarkan wilayah, bukan berdasarkan harga gabungan. Keterangan terperinci dapat dilihat di [Notice: CSS to Adjust Prices of Basic Services (Pemberitahuan: CSS Menerapkan Penyesuaian Harga Layanan Dasar)](https://intl.cloud.tencent.com/document/product/267/43055).

>!
> - Secara default, biaya ditagihkan berdasarkan penggunaan downstream. Akan tetapi, penggunaan upstream juga akan dikenai tagihan jika rasio penggunaan upstream terhadap penggunaan downstream lebih besar dari 1:10 dan bandwidth upstream tertinggi yang digunakan dalam satu hari melampaui 100 Mbps.
> - **Metode penagihan, aturan harga bertingkat, dan wilayah penagihan yang sama (di dalam/di luar Tiongkok daratan)** digunakan untuk push langsung dan pemutaran ulang LVB. **Penagihan untuk push langsung telah dimulai sejak pukul 00.00 (UTC+08.00), 1 Juli 2021.**
> - Contoh penagihan:
>  **Kita akan menggunakan tagihan berdasarkan lalu lintas harian sebagai contoh.** Misalnya, total lalu lintas upstream dan downstream yang digunakan dalam sehari adalah 10 GB dan 90 GB secara berturut-turut, dan bandwidth upstream tertinggi yang digunakan adalah 101 Mbps. Karena rasio penggunaan upstream terhadap penggunaan downstream adalah 10:90, yang berarti lebih besar dari 1:10, dan penggunaan bandwidth upstream puncak melebihi 100 Mbps, biaya lalu lintas dihitung sebagai berikut:
>  Biaya lalu lintas upstream + Biaya lalu lintas downstream = 0,0417 (USD/GB/Hari) x (10 (GB) + 90 (GB)) = 4,17 USD.


[](id:overseas_speed)

## Akselerasi di Luar Tiongkok Daratan

Penggunaan Lalu Lintas/Bandwidth di luar Tiongkok Daratan didefinisikan sebagai lalu lintas/bandwidth downstream yang terpakai ketika pengguna melakukan koneksi ke server asal akselerasi Tencent Cloud di luar Tiongkok Daratan. Anda dapat memilih penagihan [per lalu lintas](#overseas_flow) atau [per bandwidth](#overseas_bandwidth). Penagihan per lalu lintas secara default digunakan untuk pengguna baru.
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
<td>0,0748</td>
<td>0,1236</td>
<td>0,1138</td>
<td>0,0715</td>
<td>0,0715</td>
<td>0,1951</td>
<td>0,1951</td>
<td>0,1675</td>
</th>
<tr>
<td>2 TB (inklusif)‒50 TB</td>
<td>0,0699</td>
<td>0,1138</td>
<td>0,1041</td>
<td>0,0634</td>
<td>0,0634</td>
<td>0,1789</td>
<td>0,1789</td>
<td>0,1593</td>
</tr>
<tr>
<td>50 TB (inklusif)‒100 TB</td>
<td>0,0585</td>
<td>0,1057</td>
<td>0,0911</td>
<td>0,0504</td>
<td>0,0504</td>
<td>0,1675</td>
<td>0,1675</td>
<td>0,1463</td>
</tr>
<tr>
<td>100 TB (inklusif)‒1 PB</td>
<td>0,0504</td>
<td>0,0911</td>
<td>0,0813</td>
<td>0,0325</td>
<td>0,0325</td>
<td>0,1545</td>
<td>0,1545</td>
<td>0,1382</td>
</tr>
<tr>
<td>≥ 1 PB</td>
<td>0,0455</td>
<td>0,0846</td>
<td>0,0715</td>
<td>0,0260</td>
<td>0,0260</td>
<td>0,1382</td>
<td>0,1382</td>
<td>0,1301</td>
</tr>
</tbody></table>


#### Detail
- Item yang dapat dikenai tagihan: Lalu lintas downstream yang dihasilkan selama pemutaran ulang LVB di luar Tiongkok Daratan
- Aturan penagihan: Biaya dihitung dengan mengalikan total lalu lintas yang digunakan dalam sehari di suatu wilayah penagihan dengan harga unit di tingkat yang sesuai.

#### Contoh penagihan
- Misalnya, Anda menggunakan layanan LVB pada 4 Januari 2022 dan memakai 1 TB lalu lintas downstream di Hong Kong (Tiongkok) serta 6 TB lalu lintas downstream di Rusia. Pada 5 Januari 2022, Anda akan dikenai tagihan sebesar:
0,0748 (USD/GB) x 1000 (GB) + 0,0634 (USD/GB) x 6000 (GB) = 445,2 USD.

- Secara default, biaya ditagihkan berdasarkan penggunaan downstream. Akan tetapi, penggunaan upstream juga akan dikenai tagihan jika rasio penggunaan upstream terhadap penggunaan downstream lebih besar dari 1:10 dan bandwidth upstream puncak yang digunakan dalam sehari melebihi 100 Mbps. Mode penagihan, harga daftar, dan aturan harga bertingkat yang sama berlaku untuk penggunaan downstream dan upstream.

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
<td>0,2049</td>
<td>0,6016</td>
<td>0,6228</td>
<td>0,1984</td>
<td>0,1984</td>
<td>0,9333</td>
<td>0,9333</td>
<td>0,8455</td>
</tr>
<tr>
<td>500 Mbps (inklusif)‒5 Gbps</td>
<td>0,1854</td>
<td>0,5415</td>
<td>0,6049</td>
<td>0,1805</td>
<td>0,1805</td>
<td>0,9203</td>
<td>0,9203</td>
<td>0,8276</td>
</tr>
<tr>
<td>5 Gbps (inklusif)‒20 Gbps</td>
<td>0,1707</td>
<td>0,4829</td>
<td>0,5561</td>
<td>0,1681</td>
<td>0,1681</td>
<td>0,9008</td>
<td>0,9008</td>
<td>0,8065</td>
</tr>
<tr>
<td>≥ 20 Gbps</td>
<td>0,1626</td>
<td>0,4228</td>
<td>0,5041</td>
<td>0,1593</td>
<td>0,1593</td>
<td>0,8911</td>
<td>0,8911</td>
<td>0,7967</td>
</tr>
</tbody></table>


#### Detail
- Item yang dapat dikenai tagihan: Bandwidth downstream yang digunakan selama pemutaran ulang LVB di luar Tiongkok Daratan
- Aturan penagihan: Biaya dihitung dengan mengalikan bandwidth tertinggi yang digunakan dalam sehari di suatu wilayah penagihan dengan harga unit di tingkat yang sesuai.

#### Contoh penagihan

- Misalnya, Anda menggunakan layanan LVB pada 4 Januari 2022 untuk pemutaran ulang di Makau (Tiongkok) dan penggunaan bandwidth tertinggi Anda mencapai 600 Mbps. Pada 5 Januari 2022, Anda akan dikenai tagihan sebesar:
0,1854 (USD/Mbps) x 600 (Mbps) = 111,24 USD.
- Secara default, biaya ditagihkan berdasarkan penggunaan downstream. Akan tetapi, penggunaan upstream juga akan dikenai tagihan jika rasio penggunaan upstream terhadap penggunaan downstream lebih besar dari 1:10 dan bandwidth upstream puncak yang digunakan dalam sehari melebihi 100 Mbps. Mode penagihan, harga daftar, dan aturan harga bertingkat yang sama berlaku untuk penggunaan downstream dan upstream.

[](id:domestic)

## Penggunaan Lalu Lintas/Bandwidth di Tiongkok Daratan

Layanan LVB dikenai tagihan berdasarkan lalu lintas/bandwidth downstream yang digunakan selama streaming langsung. LVB menyediakan dua mode penagihan bayar-sesuai-pemakaian harian: [tagihan berdasarkan lalu lintas](#flow) dan [tagihan berdasarkan bandwidth](#bandwidth). Anda dapat memilih sesuai dengan kebutuhan.

[](id:flow)

### Tagihan berdasarkan lalu lintas

#### Harga

Untuk lalu lintas LVB, kami melakukan penagihan per hari dan menggunakan pendekatan harga bertingkat. Informasi lebih lanjut tentang tingkat harga dapat dilihat di bawah:

| Tingkat Lalu Lintas | Harga (USD/GB/Hari) |
| ----------------- | ---------------- |
| 0‒2 TB           | 0,0423           |
| 2 TB (inklusif)‒10 TB   | 0,0407           |
| 10 TB (inklusif)‒50 TB   | 0,0390                                  |
| 50 TB (inklusif)‒100 TB | 0,0358           |
| 100 TB (inklusif)‒1 PB | 0,0309                                                |
| ≥ 1 PB             | 0,0260           |

#### Detail

- Item yang dapat dikenai tagihan: Lalu lintas downstream yang terpakai selama pemutaran ulang LVB di Tiongkok Daratan
- Aturan penagihan: Biaya dihitung dengan mengalikan total lalu lintas yang dihasilkan dalam sehari dengan harga unit di tingkat yang sesuai.
- Rumus perhitungan:
  - Lalu lintas terpakai = Bitrate/8 x Total durasi pemutaran ulang. 

>?Total durasi pemutaran ulang = Jumlah pemirsa online harian x Rata-rata durasi pemutaran ulang per pemirsa. Artinya, total durasi pemutaran ulang akan sama jika 1 pemirsa menonton selama 60 menit dan 60 pemirsa menonton masing-masing selama 1 menit.

  - Biaya lalu lintas = Lalu lintas terpakai x Harga unit di tingkat yang sesuai

#### Contoh penagihan

- Misalnya, suatu sesi LVB berlangsung selama 2 jam dengan bitrate 1 Mbps (Angka ini merupakan jumlah bitrate audio dan bitrate video. Jika Anda mengaktifkan transcoding dan menetapkan bitrate video, jumlah bitrate audio dan bitrate video yang sudah ditetapkan akan digunakan untuk penagihan). Jika 100 pemirsa menonton streaming langsung masing-masing selama 1 jam dan 50 pemirsa menonton masing-masing selama 2 jam, lalu lintas yang terpakai adalah sebagai berikut:
  1 (Mbps)/8 x 7.200 (d) x 50 (Pemirsa) + 1 (Mbps)/8 x 3.600 (d) x 100 (Pemirsa) = 90.000 (MB) = 90 GB.
- Misalnya, Anda menggunakan layanan LVB pada 4 Januari 2022 dan memakai 90 GB lalu lintas downstream. Pada 5 Januari 2022, Anda akan dikenai tagihan sebesar:
  0,0423 (USD/GB) x 90 (GB) = 3,807 USD.
- Secara default, biaya ditagihkan berdasarkan penggunaan downstream. Akan tetapi, penggunaan upstream juga akan dikenai tagihan jika rasio penggunaan upstream terhadap penggunaan downstream lebih besar dari 1:10 dan bandwidth upstream puncak yang digunakan dalam sehari melebihi 100 Mbps. Mode penagihan, harga daftar, dan aturan harga bertingkat yang sama berlaku untuk penggunaan downstream dan upstream.
  <span id="bandwidth"></span>

### Tagihan berdasarkan bandwidth

#### Harga

Untuk penggunaan bandwidth LVB, kami melakukan penagihan per hari dan menggunakan pendekatan harga bertingkat. Anda akan dikenai tagihan atas penggunaan bandwidth puncak dalam satu hari. Informasi lebih lanjut tentang tingkat harga dapat dilihat di bawah:

| Tingkat Bandwidth | Harga (USD/Mbps/Hari) |
| -------------------- | ------------------ |
| 0‒500 Mbps          | 0,1057             |
| 500 Mbps (inklusif)‒5 Gbps | 0,1024             |
| 5 Gbps (inklusif)‒20 Gbps  | 0,0992             |
| ≥ 20 Gbps             | 0,0943             |

#### Detail

- Item yang dapat dikenai tagihan: Bandwidth downstream yang digunakan selama pemutaran ulang LVB di Tiongkok Daratan
- Aturan penagihan: Biaya dihitung dengan mengalikan bandwidth tertinggi yang digunakan dalam sehari dengan harga unit di tingkat yang sesuai.

#### Contoh penagihan

- Misalnya, suatu sesi LEB memiliki bitrate 500 Kbps (Angka ini adalah jumlah bitrate audio dan bitrate video. Jika Anda mengaktifkan transcoding dan menetapkan bitrate video, jumlah bitrate audio dan bitrate video yang sudah ditetapkan akan digunakan untuk penagihan), dan jumlah maksimum pemirsa yang menonton bersamaan adalah 100 orang, bandwidth tertinggi yang digunakan adalah sebagai berikut:
  500 (Kbps) × 100 = 50.000 (Kbps) = 50 Mbps.
- Misalnya, Anda menggunakan layanan LVB pada 4 Januari 2022 dan penggunaan bandwidth tertinggi Anda mencapai 50 Mbps. Pada 5 Januari 2022, Anda akan dikenai tagihan sebesar:
  0,1057 (USD/Mbps/Hari) x 50 (Mbps) = 5,285 USD.
- Secara default, biaya ditagihkan berdasarkan penggunaan downstream. Akan tetapi, penggunaan upstream juga akan dikenai tagihan jika rasio penggunaan upstream terhadap penggunaan downstream lebih besar dari 1:10 dan bandwidth upstream puncak yang digunakan dalam sehari melebihi 100 Mbps. Mode penagihan, harga daftar, dan aturan harga bertingkat yang sama berlaku untuk penggunaan downstream dan upstream.

>? Jika Anda memiliki bisnis streaming langsung skala besar dan pengeluaran Anda untuk sumber daya Tencent Cloud telah melampaui atau diperkirakan akan melampaui 10.000 USD, mode penagihan harian mungkin tidak memenuhi kebutuhan Anda. Silakan [hubungi](https://intl.cloud.tencent.com/contact-us) tim penjualan Tencent Cloud atau [kirimkan tiket](https://console.cloud.tencent.com/workorder/category) untuk mengetahui opsi penagihan lainnya.

