Izin tingkat sumber daya mengacu pada kemampuan untuk menentukan sumber daya mana yang boleh digunakan oleh pengguna untuk melakukan operasi.CBS mendukung izin tingkat sumber daya.Artinya, Anda dapat menentukan kapan pengguna diizinkan untuk melakukan beberapa operasi CBS yang mendukung izin tingkat sumber daya atau sumber daya mana yang boleh digunakan oleh pengguna.
Jenis sumber daya yang dapat diotorisasi di Cloud Access Management (CAM) adalah sebagai berikut:

| Jenis Sumber Daya | Metode Deskripsi Sumber Daya dalam Kebijakan Otorisasi |
| :-------- | -------------- |
| [API CBS](#CBSCorrelation) |  ` qcs::cvm:$region::volume/* `|

[API CBS](#CBSCorrelation) menjelaskan operasi API CBS yang saat ini mendukung izin tingkat sumber daya serta sumber daya dan kunci kondisi yang didukung oleh setiap operasi.**Saat mengonfigurasi jalur sumber daya,** Anda perlu mengganti parameter variabel seperti `$region` dan `$account` dengan parameter aktual Anda.Anda juga dapat menggunakan kartubebas `*` di jalur.Untuk informasi selengkapnya, lihat [Contoh Konsol](https://intl.cloud.tencent.com/document/product/213/10312).

<dx-alert infotype="notice" title="">
Operasi API CBS yang tidak tercantum dalam tabel tidak mendukung izin tingkat sumber daya.Anda masih dapat mengotorisasi pengguna untuk melakukan operasi ini, tetapi elemen sumber daya dari pernyataan kebijakan harus ditetapkan sebagai `*`.
</dx-alert>

[](id:CBSCorrelation)
### API CBS
<table>
<thead>
<tr>
<th align="left">Operasi API</th>
<th align="left">Jalur Sumber Daya</th>
<th align="left">Kunci kondisi</th>
</tr>
</thead>
<tbody><tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16313" target="_blank">Memasang disk cloud<br>AttachDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16312" target="_blank">Membuat disk cloud<br>CreateDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/32170" target="_blank">Mengueri daftar log operasi disk cloud<br>DescribeDiskOperationLogs</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16315" target="_blank">Mengueri daftar disk cloud<br>DescribeDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16316" target="_blank">Melepas disk cloud<br>DetachDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/15659" target="_blank">Memodifikasi atribut disk cloud<br>ModifyDiskAttributes</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left">Memodifikasi cara penagihan disk cloud<br>ModifyDisksChargeType</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left">Memodifikasi bendera pembaruan disk cloud<br>ModifyDisksRenewFlag</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left">Memperbarui disk cloud<br>RenewDisk</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16310" target="_blank">Memperluas kapasitas disk cloud<br>ResizeDisk</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
<tr>
<td align="left"><a href="https://intl.cloud.tencent.com/document/product/362/16321" target="_blank">Mengembalikan disk cloud<br>TerminateDisks</a></td>
<td align="left"><code>qcs::cvm:$region:$account:volume/*</code><br><code>qcs::cvm:$region:$account:volume/$diskId</code></td>
<td align="left">cvm:region<br>cvm:zone<br>cvm:disk_type</td>
</tr>
</tbody></table>






