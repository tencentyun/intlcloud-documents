- Tabel rute default VPC tidak dapat dihapus. 
- Setelah VPC dibuat, tabel rutenya akan otomatis disediakan dengan rute default yang menunjukkan bahwa semua sumber daya di VPC ini saling terhubung melalui jaringan pribadi. Kebijakan perutean ini tidak dapat diubah atau dihapus.
<table>
<tbody>
<tr>
<th>Tujuan</th>
<th>Jenis hop selanjutnya</th>
<th>Hop selanjutnya</th>
</tr>
<tr>
<td>Lokal</td>
<td>Lokal</td>
<td>Lokal</td>
</tr>
</tbody>
</table>

- Protokol perutean dinamis seperti BGP dan OSPF tidak didukung.
- Rute dapat dipublikasikan ke CCN. Rute berikut dapat dipublikasikan ke CCN.
<table>
<tr>
<th>Jenis hop selanjutnya</th>
<th>Menerbitkan ke CCN secara default</th>
<th>Penerbitan atau penarikan secara manual</th>
<th>Deskripsi</th>
</tr>
<tr>
<td>Lokal</td>
<td>Didukung</td>
<td>Tidak Didukung</td>
<td>Ditetapkan oleh sistem. Rentang IP VPC yang terhubung ke CCN akan otomatis dipublikasikan ke CCN, termasuk blok CIDR utama dan sekunder (kecuali untuk rentang IP TKE).</td>
</tr>
<tr>

<td>CVM</td>
<td>Tidak Didukung</td>
<td>Didukung</td>
<td>Rute kustom ke CVM. Jika rentang IP semuanya 0 atau kebijakan perutean dinonaktifkan, rute tidak dapat dipublikasikan ke CCN.</td>
</tr>
<tr>
<td>HAVIP</td>
<td>Tidak Didukung</td>
<td>Didukung</td>
<td>Rute kustom ke HAVIP. Jika rentang IP semuanya 0 atau kebijakan perutean dinonaktifkan, rute tidak dapat dipublikasikan ke CCN.</td>
</tr>
</table>

>?
> - Rute kustom yang dinonaktifkan tidak dapat dipublikasikan ke CCN.
> - Rute kustom harus ditarik terlebih dahulu sebelum dapat dinonaktifkan jika telah dipublikasikan ke CCN.

### Batasan Kuota
<table>
<tr>
<th>Sumber daya</th>
<th>Batas</th>
</tr>
<tr>
<td>Jumlah tabel rute per VPC</td>
<td>10</td>
</tr>
<tr>
<td>Jumlah tabel rute yang terhubung ke setiap subnet</td>
<td>1</td>
</tr>
<tr>
<td>Jumlah kebijakan perutean per tabel rute</td>
<td>50</td>
</tr>
</table>
