>!If you are a customer of a Tencent Cloud partner, the rules regarding resources when there are overdue payments are subject to the agreement between you and the partner.

## Kebijakan Jatuh Tempo CBS
<dx-tabs>

::: Disk cloud yang dibayar sesuai pemakaian

- Setelah Anda berhenti menggunakan sumber daya yang dibayar sesuai pemakaian, **hentikan sumber daya tersebut sesegera mungkin** untuk menghindari pemotongan biaya.
- Karena konsumsi sumber daya Anda yang sebenarnya berubah terus-menerus, mungkin akan ada beberapa perbedaan kecil untuk saldo yang tertera.

![](https://main.qcloudimg.com/raw/becc841c9f150f7ad781da71278fbed3.png)

### Peringatan
<table>
<tr>
<th>Jenis</th><th>Deskripsi</th>
</tr>
<tr>
<td><b>Peringatan saldo rendah</b></td>
<td>Sistem memperkirakan kapan saldo akun Anda akan habis berdasarkan jumlah saldo saat ini dan penggunaan sumber daya dalam 24 jam terakhir. Ketika saldo diperkirakan habis dalam 5 hari atau kurang, peringatan saldo rendah dikirim ke pembuat akun Tencent Cloud Anda dan kolaborator yang telah berlangganan pesan melalui email, SMS, dan Pusat Pesan.</td>
</tr>
<tr>
<td><b>Peringatan pembayaran yang lewat jatuh tempo</b></td>
<td>Sumber daya yang dibayar sesuai penggunaan ditagih untuk setiap jam. Saat saldo akun Anda menjadi negatif (seperti Poin 1 pada gambar di atas), peringatan akan dikirimkan ke pembuat akun Tencent Cloud dan kolaborator Anda yang telah berlangganan pesan melalui email, SMS, dan Pusat Pesan.</td>
</tr>
</table>

Memproses pembayaran yang lewat jatuh tempo

- Anda dapat terus menggunakan disk cloud yang dibayar sesuai pemakaian selama 2 jam sejak saldo akun Anda menjadi negatif. Anda akan ditagih untuk periode ini. Setelah 2 jam (Poin 2 pada gambar di atas), layanannya akan ditangguhkan (disk cloud tidak tersedia dan hanya dapat menyimpan data). Anda akan tetap ditagih sesuai standar penagihan (walaupun saldo akun negatif) hingga data terhapus seluruhnya.
- Jika akun Tencent Cloud Anda diisi hingga saldo menjadi positif dalam waktu 15 hari setelah layanan disk cloud ditangguhkan, disk dapat dipulihkan.
- Jika saldo negatif selama 15 hari setelah penangguhan disk cloud (Poin 3 pada gambar di atas), disk yang dibayar sesuai pemakaian akan diambil alih. Semua data akan dihapus dan **tidak dapat dipulihkan**. Pembuat akun Tencent Cloud dan semua kolaborator akan diberi tahu melalui email, SMS, dan Pusat Pesan.
:::
</dx-tabs>

## [Kebijakan Jatuh Tempo Snapshot](id:SnapshotArrears)
### Pembekuan
Setelah akun Tencent Cloud Anda melewati jatuh tempo, snapshot akan masuk ke status **Isolated** (Terisolasi). Operasi terkait snapshot tidak diizinkan, termasuk pembuatan snapshot, pengembalian, replikasi lintas wilayah, kebijakan snapshot terjadwal, dll.
- Snapshot yang terisolasi akan disimpan selama 30 hari. Jika saldo akun Anda tetap negatif, semua snapshot (kecuali snapshot gambar) akan dihapus setelah periode ini.


### Catatan
- Bahkan setelah akun Anda jatuh tempo, **ukuran penyimpanan snapshot yang melebihi tingkat gratis akan tetap ditagih** hingga dihapus.
- Setelah snapshot dihentikan, data tidak dapat dipulihkan.
- Setelah pembayaran yang lewat jatuh tempo dibayar, operasi snapshot secara otomatis dilanjutkan.
- Jika Anda tidak lagi membutuhkan snapshot, hapus untuk menghindari pemotongan biaya. Untuk informasi selengkapnya, lihat [Menghapus Snapshot](https://intl.cloud.tencent.com/document/product/362/5758).


