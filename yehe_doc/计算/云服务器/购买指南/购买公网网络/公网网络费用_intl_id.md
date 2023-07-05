Dokumen ini menjelaskan harga jaringan publik dalam berbagai mode penagihan dan membantu Anda memilih paket penagihan yang paling sesuai dengan bisnis Anda.

## Tagihan per lalu lintas
>? Biaya dalam skema bayar sesuai pemakaian pada siklus penagihan per jam berdasarkan lalu lintas jaringan publik yang digunakan. Tagihan per lalu lintas cocok untuk skenario di mana lalu lintas bisnis puncak sangat fluktuatif pada waktu yang bervariasi.

**Pricing** (Harga)
<table>
<thead>
<tr>
<th>Wilayah</th>
<th>Harga (unit: USD/GB)</th>
</tr>
</thead>
<tbody><tr>
<td>Tiongkok daratan (tidak termasuk Hong Kong, Macau, dan Taiwan), Seoul, Hong Kong (Tiongkok), Jakarta</td>
<td>0,12</td>
</tr>
<tr>
<td>Tokyo</td>
<td>0,13</td>
</tr>
<tr>  
<td>Singapura</td>
<td>0,081</td>
</tr>
<tr>
<td>Sao paulo</td>
<td>0,15</td>
</tr>
<tr>  
<td>Toronto, Silicon Valley, Frankfurt</td>
<td>0,077</td>
</tr>
<tr>
<td>Bangkok, Mumbai</td>
<td>0.1</td>
</tr>
<tr> 
<td>Virginia</td>
<td>0,075</td>
</tr>
<tr>
</tbody></table>


**Contoh Penagihan**
Misal, Anda membeli EIP di wilayah Seoul dengan mode penagihan tagihan per lalu lintas dan menggunakan lalu lintas total 10 GB antara pukul 07:00:00-07:59:59, pada pukul 08:00:00, biaya yang harus dibayar: 0,12 USD/GB × 10 GB = 1,2 USD.

> ?
> - Unit lalu lintas berbasis 1024. Misalnya, 1 TB = 1.024 GB, dan 1 GB = 1.024 MB.
> - lalu lintas jaringan publik mengacu pada lalu lintas hilir (dalam byte) yang merupakan data lapisan aplikasi. Selama transfer data aktual, lalu lintas yang dihasilkan melalui jaringan sekitar 5-15% lebih banyak daripada lalu lintas lapisan aplikasi, sehingga lalu lintas yang dihitung Tencent Cloud mungkin sekitar 10% lebih banyak dari yang dihitung oleh pengguna sendiri di server.
> - Penggunaan oleh header TCP/IP: dalam permintaan HTTP berbasis TCP/IP, setiap paket memiliki ukuran maksimum 1.500 byte dan mencakup header TCP dan IP sebesar 40 byte yang menghasilkan lalu lintas selama transfer tetapi tidak dapat dihitung oleh lapisan aplikasi. Overhead bagian ini sekitar 3%.
> - Transmisi ulang TCP: selama transfer data normal melalui jaringan, sekitar 3-10% paket gagal terkirim di Internet dan ditransmisi ulang oleh server. Jenis lalu lintas ini, yang menyumbang 3-7% dari lalu lintas total, tidak dapat dihitung pada lapisan aplikasi.


## Paket Bandwidth
Tencent Cloud Bandwidth Package (BWP) adalah metode penagihan agregat multi-IP. Mode ini sangat menghemat biaya jaringan publik Anda ketika instans jaringan publik mengalami puncak lalu lintas pada waktu yang berbeda.
Untuk detail harga, harap lihat [Mode Penagihan](https://intl.cloud.tencent.com/document/product/684/15255).


## Referensi
- [Penagihan Jaringan Publik](https://intl.cloud.tencent.com/document/product/213/10578)
- [Batas Bandwidth Jaringan Publik](https://intl.cloud.tencent.com/document/product/213/12523)
