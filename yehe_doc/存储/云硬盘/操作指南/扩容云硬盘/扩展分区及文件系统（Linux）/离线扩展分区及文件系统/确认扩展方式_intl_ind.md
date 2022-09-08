## Ikhtisar
Disk cloud adalah perangkat penyimpanan yang dapat diperluas di cloud.Setelah disk cloud dibuat, Anda dapat memperluas kapasitasnya kapan saja untuk meningkatkan kapasitas penyimpanannya tanpa kehilangan data apa pun di dalamnya.
Setelah [memperluas kapasitas disk cloud](https://intl.cloud.tencent.com/document/product/362/5747) di konsol, Anda harus masuk ke instance CVM untuk menetapkan kapasitas yang diperluas ke partisi yang ada menggunakan metode yang tepat sesuai kebutuhan.Dokumen ini menjelaskan cara menentukan metode perluasan pada CVM Linux.
<dx-alert infotype="notice" title="">
Memperluas sistem file dapat memengaruhi data yang ada.Kami sangat menyarankan Anda untuk secara manual [membuat snapshot](https://intl.cloud.tencent.com/document/product/362/5755) untuk mencadangkan data Anda sebelum melakukan operasi tersebut.
</dx-alert>


## Prasyarat
- Anda telah [memperluas disk cloud melalui konsol](https://intl.cloud.tencent.com/document/product/362/5747).
- Anda telah [memasang disk cloud](https://intl.cloud.tencent.com/document/product/362/32401) ke CVM Linux dan membuat sistem file.
- Anda telah [masuk ke instance Linux](https://intl.cloud.tencent.com/document/product/213/5436) yang memerlukan perluasan partisi dan sistem file.

## Petunjuk
1.Jalankan perintah berikut sebagai pengguna root untuk melihat format partisi disk cloud.[](id:fdisk)
```shellsession
fdisk -l
```
- Jika hasilnya hanya menampilkan `/dev/vdb` tanpa partisi, Anda perlu memperluas sistem file.
![](https://main.qcloudimg.com/raw/661ad0745c10a44035697cf4d03759f5.png)
- Jika hasilnya seperti yang ditunjukkan pada dua gambar berikut (yang dapat berbeda sesuai dengan sistem operasi), format partisi GPT harus digunakan.
![](https://main.qcloudimg.com/raw/5ff70adb58a223d32d334470c5b29e0e.png)
![](https://main.qcloudimg.com/raw/ce19715fc8494a9735b714d86f0cccfa.png)
- Jika hasilnya seperti yang ditunjukkan pada gambar berikut (yang dapat berbeda sesuai dengan sistem operasi), format partisi MBR harus digunakan.
![](https://main.qcloudimg.com/raw/0e336cd3354c098cf5e70d0672e6f625.png)
2.Pilih metode perluasan yang sesuai dengan format partisi yang diperoleh di [langkah 1](#fdisk).
<dx-alert infotype="notice" title="">
- Partisi MBR mendukung disk dengan kapasitas maksimum 2 TB.
- Saat Anda mempartisi disk dengan kapasitas lebih besar dari 2 TB, kami menyarankan Anda membuat dan memasang disk data baru dan menggunakan format partisi GPT untuk menyalin data.
</dx-alert>
<table>
<tr>
<th nowrap="nowrap">Format partisi</th>
<th>Metode perluasan</th>
<th>Deskripsi</th>
</tr>
<tr>
<td>-</td>
<td nowrap="nowrap">Memperluas sistem file</a></td>
<td>Berlaku untuk skenario ketika sistem file dibuat langsung pada perangkat kosong dan <b>tidak ada partisi yang dibuat</b>.</td>
</tr>
<tr>
<td rowspan="2">GPT</td>
<td nowrap="nowrap"><a href="https://cloud.tencent.com/document/product/362/53366#Add">Menetapkan kapasitas yang diperluas ke partisi GPT yang ada</a></td>
<td>Berlaku untuk skenario pemformatan langsung saat tidak ada partisi yang dibuat.</td>
</tr>
<tr>
<td><a href="https://cloud.tencent.com/document/product/362/53366#New">Memformat kapasitas yang diperluas menjadi partisi GPT baru yang terpisah</a></td>
<td>Berlaku untuk skenario ketika partisi asli tetap tidak berubah dan partisi GPT baru dibuat untuk perluasan.</td>
</tr>
<tr>
<td rowspan="2">MBR</td>
<td><a href="https://cloud.tencent.com/document/product/362/53365#Add">Menetapkan kapasitas yang diperluas ke partisi MBR yang ada</a></td>
<td>Berlaku untuk skenario pemformatan langsung saat tidak ada partisi yang dibuat.</td>
</tr>
<tr>
<td><a href="https://cloud.tencent.com/document/product/362/53365#New">Memformat kapasitas yang diperluas menjadi partisi MBR baru yang terpisah</a></td>
<td>Berlaku untuk skenario ketika partisi asli tetap tidak berubah dan partisi MBR baru dibuat untuk perluasan.</td>
</tr>
</table>






