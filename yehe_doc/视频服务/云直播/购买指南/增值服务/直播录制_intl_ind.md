CSS dapat merekam streaming langsung dan menyimpannya dalam VOD. Penggunaan perekaman langsung akan dikenai biaya. Perekaman langsung dikenai tagihan berdasarkan **jumlah puncak saluran perekaman bersamaan pada bulan tersebut**.

### Catatan

- Fitur perekaman dinonaktifkan secara default dan dapat diaktifkan di konsol atau melalui API TencentCloud.
- File video rekaman disimpan di [konsol VOD](https://console.cloud.tencent.com/vod/overview) secara default dan akan dikenai [biaya VOD](https://intl.cloud.tencent.com/document/product/266/2838). Setelah Anda mengaktifkan fitur perekaman, pastikan layanan VOD Anda dalam kondisi normal. Jika fitur perekaman tidak diaktifkan atau ditangguhkan karena keterlambatan pembayaran, perekaman langsung tidak akan tersedia, file rekaman tidak dapat dibuat, dan biaya perekaman tidak akan dikenakan.
- Untuk informasi selengkapnya tentang cara menghitung jumlah puncak saluran perekaman, silakan pelajari [CSS Billing (Penagihan CSS)](https://intl.cloud.tencent.com/document/product/267/32479).



### Harga

| Item Tagihan | Harga (USD/Saluran/Bulan) |
| ------------ | ------------------ |
| Jumlah puncak saluran perekaman | 5,2941             |

### Ikhtisar Penagihan

- Item yang dapat dikenai tagihan: jumlah saluran perekaman langsung.
- Mode penagihan: bayar sesuai pemakaian.
- Siklus penagihan: siklus penagihan bulanan. Tagihan bulan berjalan akan dibuat antara tanggal 1 dan 5 bulan berikutnya. Silakan baca laporan penagihan aktual Anda untuk keterangan detail.


### Rumus Perhitungan

- Persentase hari perekaman yang valid = Jumlah hari penggunaan fitur perekaman dalam suatu bulan/Total jumlah hari dalam bulan tersebut.
- Biaya perekaman = Jumlah puncak saluran perekaman bersamaan dalam suatu bulan × Persentase hari perekaman yang valid × Harga unit saluran perekaman.
>? Jumlah puncak bulanan saluran perekaman bersamaan: nilai terbesar di antara semua jumlah saluran perekaman langsung dengan durasi 5 menit dalam bulan tersebut. Satu format perekaman dihitung sebagai satu saluran streaming perekaman. Sebagai contoh, jika file MP4 dan HLS direkam untuk ID streaming yang sama, dua jenis file tersebut akan dihitung sebagai dua saluran streaming perekaman.

### Contoh Penagihan

Sebuah templat perekaman dikonfigurasi oleh pengguna A untuk nama domain A dan B di konsol CSS dengan **1** format file rekaman untuk nama domain A dan **2** format untuk nama domain B. Nama domain A memiliki 11 push langsung pada 2 April 2020 dan memiliki 10 push pada 5 hari lainnya. Nama domain B memiliki 1 push langsung pada 29 April 2020. Tabel berikut memperlihatkan jumlah hari penggunaan fitur perekaman oleh nama domain A dan B: 

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">ID Streaming</th>
<th colspan=7 width="50%" style="text-align:center;">April 2020 (Tanggal 1‒30)</th>
<th rowspan=2 width="10%" style="text-align:center;">Jumlah hari valid <br>penggunaan fitur perekaman</th>
</tr><tr>
<td style="text-align:center;">1</td><td style="text-align:center;">2</td><td style="text-align:center;">3</td>
<td style="text-align:center;">…</td>
<td style="text-align:center;">28</td><td style="text-align:center;">29</td><td style="text-align:center;">30</td>
</tr><tr>
<td style="text-align:center;">A</td>
<td id="ye"></td><td id="ye"></td><td id="ye"></td>
<td rowspan=13 style="text-align:center;">Perekaman tidak digunakan</td>
<td id="ye"></td><td id="ye"></td><td id="ye"></td>
<td style="text-align:center;">6</td>
</tr><tr>
<td style="text-align:center;">B</td>
<td></td><td></td><td></td><td></td><td id="gr"></td><td></td>
<td style="text-align:center;">1</td>
</tr><tr>
<td style="text-align:center;">Pengguna A menggunakan <br>fitur perekaman</td>
<td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td>
<td style="text-align:center;">6</td>
</tr>
</tr>
</table>


- Jumlah saluran perekaman puncak pada 2 April 2020 adalah **11**. Rumus perhitungan: 11 Saluran untuk nama domain A × 1 Format + 0 Saluran untuk nama domain B × 2 Format = 11 Saluran.
- Jumlah saluran perekaman puncak pada 29 April 2020 adalah **12**. Rumus perhitungan: 10 Saluran untuk nama domain A × 1 Format + 1 Saluran untuk nama domain B × 2 Format = 12 Saluran.
- Pada April 2020, jumlah hari perekaman adalah 6 untuk nama domain A dan 1 untuk nama domain B sehingga total jumlah hari penggunaan fitur perekaman oleh pengguna A pada April adalah 6, dan persentase hari perekaman yang valid adalah 6 hari/30 hari = 0,2.

Oleh karena itu, jumlah maksimum saluran push langsung bersamaan untuk April 2020 adalah 12, persentase hari perekaman yang valid adalah 0,2, dan biaya perekaman langsung yang harus Anda bayar untuk bulan ini adalah sebagai berikut:
Biaya perekaman langsung untuk April = 5,2941 (USD/Saluran/Bulan) × 0,2 × 12 Saluran = 12,70584 USD.