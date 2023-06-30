Biaya EIP dibebankan menurut dua jenis akun, tagihan per IP dan tagihan per CVM. Dokumen ini mengenalkan bagaimanan biaya EIP ditagih untuk dua jenis akun. 

## Latar belakang

Saat ini, ada dua jenis akun Tencent Cloud: tagihan per IP dan tagihan per CVM. Semua akun Tencent Cloud yang terdaftar setelah 17 Juni 2020 adalah akun tagihan per IP. Perbedaan kedua jenis akun tersebut adalah sebagai berikut:
 - Tagihan per CVM: mengelola bandwidth/lalu lintas di CVM. IP dan CLB akun tagihan CVM tidak memiliki bandwidth jaringan atau atribut lalu lintas sehingga harus dibeli dan dikelola di CVM.
 - Tagihan per IP: mengelola bandwidth/lalu lintas pada IP dan CLB. CVM yang dibeli oleh akun ini tidak lagi mempertahankan bandwidth jaringan eksternal atau sumber daya lalu lintas, CLB/IP publik mengelola bandwidth jaringan eksternal atau sumber daya lalu lintas.

>? Untuk informasi selengkapnya tentang memeriksa jenis akun Anda, lihat [Memeriksa Jenis Akun Anda](https://intl.cloud.tencent.com/document/product/684/15246).

## Item yang Dapat Ditagih

Biaya EIP terdiri dari **biaya sumber daya IP** dan **biaya jaringan publik**. Berikut adalah pembayaran akun tagihan per CVM dan tagihan per IP:

### Akun tagihan per CVM

Akun tagihan per CVM hanya dikenakan biaya sumber daya IP. Biaya jaringan publik dibebankan pada instans CVM.

- Bila EIP belum tersambung dengan sumber daya cloud: EIP hanya membebankan <a href="#ip"> biaya sumber daya IP</a> per jam.
- Ketika EIP telah tersambung dengan sumber daya cloud: EIP tidak memungut biaya apa pun. <a href="https://intl.cloud.tencent.com/document/product/213/10578">Biaya jaringan publik</a> dibebankan pada instans CVM.


### Akun tagihan per IP

Ada tiga paket penagihan untuk akun tagihan per IP:

<ul>
<li>Tagihan per lalu lintas: membebankan biaya jaringan publik dan biaya sumber daya IP.</li>
<ul>
<li>Bila EIP belum tersambung dengan sumber daya cloud: EIP hanya membebankan <a href="#ip">biaya sumber daya IP</a> per jam dan tidak membebankan biaya jaringan publik.</li>
<li>Saat EIP telah tersambung dengan sumber daya cloud: EIP hanya membebankan <a href="#net">biaya jaringan publik</a>.</li>
</ul>
<li>Langganan bandwidth bulanan: hanya membebankan <a href="#net">biaya jaringan publik</a>, terlepas dari apakah EIP telah tersambung dengan sumber daya cloud atau tidak.</li>
<li>Paket bandwidth: membebankan biaya jaringan publik dan biaya sumber daya IP.
<ul>
<li>Bila EIP belum tersambung dengan sumber daya cloud: EIP hanya membebankan <a href="#ip">biaya sumber daya IP</a> per jam dan tidak membebankan biaya jaringan publik.</li>
<li>Saat EIP telah tersambung dengan sumber daya cloud: EIP hanya membebankan <a href="#net">biaya jaringan publik</a>.</li>
</ul></li>
</ul>

<span id ="ip"></span>
## Biaya Sumber Daya IP

### Periode penagihan

Biaya sumber daya IP berjenis bayar sesuai pemakaian pada siklus penagihan per jam.
Biaya sumber daya IP ditagih mulai dari saat Anda mengajukan EIP. Penagihan ditangguhkan saat sumber daya cloud tersambung, dilanjutkan saat sumber daya cloud tidak tersambung, dan berhenti saat EIP dilepaskan. Penagihan akurat hingga detik, dan biaya yang dihasilkan untuk jam tersebut telah diputuskan dan dipotong pada jam berikutnya. Jika sumber daya cloud tidak tersambung dan tersambung beberapa kali dalam siklus penagihan yang sama, periode penagihan adalah waktu kumulatif yang dihabiskan sumber daya cloud saat tidak tersambung.


### Rumus penagihan

Biaya sumber daya IP = harga waktu jeda wilayah tempat EIP × periode penagihan

#### Harga

<table>
   <tr><th>Wilayah</th><th>Harga (USD/Jam)</th></tr>
   <tr><td>Tiongkok Daratan</td><td>0,031</td></tr>
   <tr><td>Hong Kong, Tiongkok</br>Singapura</br>Frankfurt</br>Seoul</br>Toronto</br>Virginia</br>Silicon Valley</br>Bangkok</br>Tokyo</br>Mumbai</td><td>0,04</td></tr>
</table>


#### Contoh penagihan

Misal, pengguna dengan akun tagihan per CVM mengajukan EIP di wilayah Guangzhou antara pukul 09:00:00 - 09:59:59 dan tersambung dengan CVM setelah waktu jeda selama 15 menit (900 detik), biaya sumber daya IP yang dihasilkan: 0,031 USD/jam \* (900/3600) jam = 0,00775 USD. 

> ! Untuk menghindari menghasilkan biaya sumber daya IP yang tidak perlu, harap segera sambungkan EIP dengan sumber daya cloud setelah mengajukan EIP dan segera lepaskan EIP setelah memutus sambungan dari sumber daya cloud.

<sapn id="net"></span>

## Biaya Jaringan Publik

Lalu lintas jaringan publik yang dihasilkan oleh EIP akan dikenakan biaya jaringan publik. Ada dua paket penagihan berbeda: tagihan per lalu lintas dan tagihan per bandwidth. Untuk detail selengkapnya, lihat [Penagihan Jaringan Publik](https://intl.cloud.tencent.com/document/product/213/39743). 

## Melewati Jatuh Tempo
### Akun Melewati Jatuh Tempo
<table>
    <tr><th>Periode melewati jatuh tempo</th><th>Deskripsi</th></tr>
    <tr><td>Kurang dari 2 jam</td><td>Anda dapat terus menggunakan sumber daya dan akun Anda akan terus dibebankan biaya.</td></tr>
    <tr><td>≥ 2 jam atau 2 jam + 24 jam</td><td>EIP akan dipertahankan, tetapi layanan akan ditangguhkan. Biaya tidak akan dikenakan lagi dan EIP tidak dapat digunakan.</td></tr>
    <tr><td>≥ 2 jam + 24 jam</td><td><li>EIP yang belum tersambung dengan sumber daya cloud akan dilepaskan.</li><li>EIP yang telah tersambung dengan sumber daya cloud akan dipertahankan, tetapi layanan akan ditangguhkan. Biaya tidak akan dikenakan lagi dan EIP tidak dapat digunakan.</li></td></tr>
</table>

### Sumber daya tersambung yang melewati jatuh tempo 
Jika sumber daya yang tersambung ke EIP melewati jatuh tempo, EIP akan dilepaskan dari sumber daya, menjadi tidak aktif, dan dikenakan biaya waktu jeda. Jika tidak perlu menggunakan EIP lagi, harap lepaskan di Konsol.



