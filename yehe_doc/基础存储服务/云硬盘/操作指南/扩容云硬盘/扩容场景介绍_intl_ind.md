### Memperluas disk sistem cloud
- [Memperluas disk sistem cloud melalui konsol CVM](https://intl.cloud.tencent.com/document/product/362/5747)




### Memperluas disk data cloud

Jika disk cloud adalah disk data, Anda dapat memperluasnya menggunakan tiga metode berikut.
- [Memperluas disk cloud melalui konsol CVM](https://intl.cloud.tencent.com/document/product/362/5747)
- [Memperluas disk cloud melalui konsol CBS](https://intl.cloud.tencent.com/document/product/362/5747)
- [Memperluas disk cloud melalui API](https://intl.cloud.tencent.com/document/product/362/5747)




Berdasarkan status **melampirkan** disk data CBS, Anda dapat memperluas kapasitasnya dengan metode yang berbeda.
- Jika disk data CBS saat ini **dapat dilepas**, Anda dapat meningkatkan kapasitasnya di konsol CBS atau melalui API [`ResizeDisk`](https://intl.cloud.tencent.com/document/product/362/16310).
- Jika disk data CBS saat ini **tidak dapat dilepas**, Anda dapat memperluas kapasitasnya di konsol CVM atau melalui API [`ResizeDisk`](https://intl.cloud.tencent.com/document/product/362/16310).

>! Jika kapasitas maksimum disk cloud tidak dapat memenuhi kebutuhan bisnis Anda, silakan coba [membangun grup RAID](https://intl.cloud.tencent.com/document/product/362/2932) atau [membangun volume logis LVM dengan beberapa disk cloud elastis](https://intl.cloud.tencent.com/document/product/362/2933).
>
Setelah kapasitas disk data diperluas, Anda harus melakukan operasi berikut agar instance dapat mengenali dan menggunakan disk data:
<table>
<tr>
<th nowrap="nowrap">Sebelum Perluasan</th>
<th nowrap="nowrap">Setelah Perluasan</th>
<th>Operasi Berikutnya</th>
</tr>
<tr>
<td   rowspan="2" nowrap="nowrap">Sistem file tidak dibuat</td>
<td>Kapasitas disk < 2 TB</td>
<td><a href="https://intl.cloud.tencent.com/document/product/362/31597">Menginisialisasi disk cloud (< 2 TB)</a></td>
</tr>
<tr>
<td nowrap="nowrap">Kapasitas disk 2 TB</td>
<td><a href="https://intl.cloud.tencent.com/document/product/362/31598">Menginisialisasi disk cloud (≥ 2 TB)</a></td>
</tr>
<tr>
<td   rowspan="2">Sistem file dibuat</td>
<td>Kapasitas disk < 2 TB</td>
<td><ul><li>Disk cloud yang terlampir ke CVM Windows: <a href="https://intl.cloud.tencent.com/document/product/362/31601">memperluas partisi dan sistem file (Windows )</a></li>
<li>Disk cloud yang diperluas yang dilampirkan ke CVM Linux: <a href="https://intl.cloud.tencent.com/document/product/362/39995">memperluas partisi dan sistem file (Linux)</a> </li></ul>
</td>
</tr>
<tr>
<td>Kapasitas disk ≥ 2 TB</td>
<td>
<ul><li>Format partisi GPT: <a href="https://intl.cloud.tencent.com/document/product/362/31601">memperluas partisi dan sistem file (Windows)</a> atau <a href="https://intl.cloud.tencent.com/document/product/362/39995">memperluas partisi dan sistem file (Linux)</a></li>
<li>Format partisi MBR: tidak didukung.</li>Partisi MBR mendukung disk dengan kapasitas maksimum 2 TB.Saat Anda mempartisi disk dengan kapasitas lebih besar dari 2 TB, sebaiknya Anda membuat dan melampirkan disk data baru dan menggunakan format partisi GPT untuk menyalin data.</ul>
</td>
</tr>
</table>


