Alamat IP mendukung protokol pengalamatan IPv4 dan IPv6. IPv4 banyak digunakan, tetapi jumlah alamat jaringannya terbatas, menjadikan IPv6 sebagai pelengkap yang baik.

## Alamat IPv4
Tencent Cloud menyediakan alamat IPv4 untuk akses jaringan pribadi dan publik. Alamat IPv4 publik dapat bersifat umum atau elastis. Seperti yang ditunjukkan pada gambar berikut, **EIP** (EIP) menunjukkan alamat IPv4 elastis, **Private** (Pribadi) menunjukkan alamat IPv4 pribadi, dan **Public** (Publik) menunjukkan alamat IPv4 publik. IP ini tidak akan berubah kecuali Anda melepas ikatan atau mengubahnya.
>?Kecuali ditentukan lain, IP pribadi, IP publik, dan EIP semuanya merujuk ke alamat IPv4.
>
![](https://main.qcloudimg.com/raw/6bb952befc42a89392b4d2369f04820d.png)

### Alamat IPv4 Pribadi
Alamat IPv4 pribadi digunakan untuk akses jaringan pribadi Tencent Cloud, yang tidak dapat digunakan untuk mengakses internet. Setelah instans CVM dibuat, instans tersebut akan secara otomatis ditetapkan dengan alamat IPv4 pribadi. Alamat IPv4 pribadi juga dapat dikustomisasi dalam lingkungan VPC.

#### Atribut
- Jaringan pribadi IPv4 spesifik pengguna, dan pengguna yang berbeda saling terisolasi. Secara default, layanan cloud pengguna lain tidak dapat diakses melalui jaringan pribadi IPv4.
- Jaringan pribadi IPv4 spesifik wilayah, dan wilayah yang berbeda saling terisolasi. Secara default, layanan cloud yang menggunakan akun yang sama di wilayah yang berbeda tidak dapat diakses melalui jaringan pribadi IPv4.

#### Kasus penggunaan
Alamat IPv4 pribadi dapat digunakan untuk:
- Interkoneksi antara instans CLB dan CVM berbasis jaringan klasik atau berbasis VPC melalui jaringan pribadi IPv4.
- Interkoneksi antara instans CVM berbasis jaringan klasik atau berbasis VPC melalui jaringan pribadi IPv4.
- Interkoneksi antara instans CVM berbasis jaringan atau klasik berbasis VPC dan layanan Tencent Cloud lainnya (seperti TencentDB) melalui jaringan pribadi IPv4.

#### Operasi yang relevan
- Untuk informasi selengkapnya tentang cara mendapatkan alamat IPv4 pribadi instans dan DNS yang ditetapkan, lihat [Mendapatkan Alamat IP Pribadi dan Mengatur DNS](https://intl.cloud.tencent.com/document/product/213/17941).
- Untuk informasi selengkapnya tentang cara mengubah alamat IPv4 pribadi instans CVM di VPC, lihat [Memodifikasi Alamat IP Pribadi](https://intl.cloud.tencent.com/document/product/213/16561).

### Alamat IPv4 publik
Tencent Cloud menyediakan IP dan EIP publik untuk akses jaringan publik. Instans CVM dengan alamat IPv4 publik dapat mengakses dan diakses melalui jaringan publik IPv4.

#### Perbandingan
Tabel berikut membandingkan IP publik dengan EIP.
<table>
<thead>
<tr>
<th colspan="2" width="16%">Item</th>
<th>IP Publik</th>
<th>EIP</th>
</tr>
</thead>
<tbody>
<tr>
<td colspan="2">Kasus penggunaan</td>
<td>Jika Anda ingin membuat CVM yang mendukung akses jaringan publik, Anda dapat memilih menggunakan alamat IP publik yang ditetapkan secara otomatis oleh sistem saat membuat instans CVM. Alamat IP publik ini memiliki siklus pemakaian yang sama dengan CVM, dan akan dilepas setelah pelepasan CVM yang terikat.</td>
<td>Jika ingin menggunakan IP publik dalam waktu lama, Anda dapat memilih IP elastis (EIP) dan mengikatnya ke CVM yang ditentukan sesuai kebutuhan. EIP dapat diikat atau dilepas ikatannya berkali-kali, dan akan tetap ada setelah CVM dilepas.</td>
</tr>
<tr>
<td colspan="2">Akses jaringan publik</td>
<td colspan="2">Keduanya mendukung akses jaringan publik.</td>
</tr>
<tr>
<td colspan="2">Metode akuisisi</td>
<td>Metode ini hanya dapat diperoleh ketika Anda membeli CVM.</td>
<td><li>1. Terapkan untuk EIP di konsol.</li><li>2. Ubah alamat IP publik menjadi EIP.</li></td>
</tr>
<tr>
<td colspan="2">Fitur</td>
<td>Alamat IP ini memiliki siklus pemakaian yang sama dengan CVM, dan akan dilepas setelah pelepasan CVM yang terikat.</td>
<td><li>Tidak terikat dari sumber daya lain. Anda dapat mengikatnya ke atau melepaskannya dari CVM dan NAT Gateway kapan saja.</li><li>Anda dapat melepaskan EIP saat Anda tidak lagi membutuhkannya.</li></td>
</tr>
<tr>
<td colspan="2" >Biaya</td>
<td>Hanya biaya jaringan publik yang akan dikenakan biaya.</td>
<td>Biaya sumber daya IP adalah bagian dari biaya EIP, yang berbeda-beda, tergantung jenis akunnya. Untuk informasi selengkapnya, silakan lihat <a href="https://intl.cloud.tencent.com/document/product/684/15246">Memeriksa Jenis Akun</a>.</td>.
</tr>
<tr>
<td colspan="2" rowspan="2">Kuota</td>
<td>Tergantung jumlah CVM yang Anda beli.</td>
<td>Setiap akun dapat menerapkan 20 EIP di setiap wilayah.</td>
</tr>
<tr>
<td colspan="2">Untuk kuota IP publik (termasuk EIP) yang terikat pada CVM, lihat batasan pada IP publik yang terikat pada CVM.</td>
</tr>
<tr>
<td rowspan="4" >Operasi</td>
<td>Mengonversi IP</td>
<td>IP publik dapat dikonversi menjadi EIP. Alamat IP tidak akan berubah setelah konversi.</td>
<td>EIP tidak bisa dikonversi kembali ke IP publik.</td>
</tr>
<tr>
<td>Mengubah IP</td>
<td>IP publik dapat langsung diubah.
Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/16642" target="_blank">Mengubah Alamat IP Publik</a></td>
<td>EIP tidak dapat langsung diubah. Anda perlu melepas ikatan dan melepaskan EIP, menerapkan yang baru, dan mengikatnya lagi.</td>
</tr>
<tr>
<td>Melepaskan IP</td>
<td>Jika Anda tidak memerlukan IP publik lagi, Anda dapat masuk ke <a href="https://console.cloud.tencent.com/cvm" target="_blank">konsol CVM</a>, cari IP publik, dan di kolom <b>Operasi</b>, pilih <b>Selengkapnya > IP/ENI > Kembalikan IP Publik</b> untuk mengembalikannya.</td>
<td>Anda dapat melepaskan EIP di konsol EIP.</td>
</tr>
<tr>
<td>Mengambil IP</td>
<td colspan="2">Anda dapat mengambil IP/EIP publik yang telah Anda gunakan jika belum digunakan oleh pengguna lain.</td>
</tr>
</tbody></table>

#### Penagihan
Lalu lintas jaringan publik yang dihasilkan oleh alamat IPv4 publik akan dikenakan biaya jaringan publik. Untuk informasi selengkapnya, lihat [Harga Jaringan Publik](https://buy.cloud.tencent.com/price/idc).


## Informasi yang Relevan
- Untuk informasi selengkapnya tentang cara cepat membangun IPv4 Virtual Private Cloud (VPC), lihat [Membangun VPC IPv4](https://intl.cloud.tencent.com/document/product/215/31891).
Untuk informasi selengkapnya tentang EIP, lihat [IP Elastis](https://intl.cloud.tencent.com/document/product/215/34109).

