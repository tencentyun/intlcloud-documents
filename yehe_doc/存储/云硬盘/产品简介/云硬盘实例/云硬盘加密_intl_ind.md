Saat Anda perlu mengenkripsi data yang disimpan di disk cloud karena alasan keamanan atau kepatuhan bisnis, Anda dapat mengaktifkan enkripsi disk cloud dan menggunakan infrastruktur yang disediakan oleh [Layanan Manajemen Kunci/Key Management Service (KMS) Tencent Cloud](https://intl.cloud.tencent.com/product/kms) untuk melindungi privasi data secara efektif.
>Fitur ini sedang dalam pengujian beta.Untuk menggunakannya, Anda perlu [mengirimkan tiket](https://console.cloud.tencent.com/workorder/category) untuk mendaftar.
>

## Manajemen Kunci
Tencent Cloud mengenkripsi data di disk cloud Anda menggunakan kunci enkripsi data berdasarkan algoritme AES-256 standar.Saat Anda menggunakan enkripsi disk cloud untuk pertama kalinya, sistem secara otomatis membuat kunci master pelanggan/customer master key (CMK) yang memungkinkan Anda untuk menggunakan fitur enkripsi disk cloud di wilayah yang sesuai di KMS.Hanya satu CMK yang secara otomatis dibuat dan disimpan di KMS, yang dilindungi oleh kontrol keamanan fisik dan logis yang ketat.
Di setiap wilayah, kunci data/data key (DK) 256-bit unik digunakan untuk mengenkripsi disk cloud.Snapshot yang dibuat melalui disk cloud terenkripsi dan disk cloud terenkripsi yang dibuat melalui snapshot terenkripsi semuanya terkait dengan DK ini.DK dilindungi oleh infrastruktur Manajemen kunci yang disediakan oleh KMS, yang secara efektif memblokir akses yang tidak sah.DK disk cloud hanya digunakan dalam memori host tempat instance berada, dan tidak disimpan dalam media persisten apa pun (termasuk disk cloud itu sendiri) dalam bentuk teks biasa.

## Prinsip Operasi
Saat Anda mengonfigurasi disk cloud Anda sebagai terenkripsi, KMS mengenkripsi data dan secara otomatis mendekripsinya selama operasi baca.Proses enkripsi dan dekripsi dilakukan pada host tempat instance CVM berada, dengan dampak minimal pada kinerja baca dan tulis disk cloud.Untuk menguji kinerja disk cloud, lihat [Mengukur kinerja disk cloud](https://intl.cloud.tencent.com/document/product/362/6741).

Setelah disk cloud terenkripsi dibuat dan dipasang ke instance, sistem mengenkripsi data berikut:
- Data statis di disk cloud;
- Data yang ditransmisikan antara disk cloud dan instance (data dalam sistem operasi instance tidak dienkripsi);
- Semua snapshot yang dibuat melalui disk cloud terenkripsi;

## Batas Penggunaan
Fitur enkripsi disk cloud tunduk pada batasan berikut:

<table>
<tr>
<th width="20%">Batasan</th>
<th>Deskripsi</th>
</tr>
<tr>
<td>Batasan disk cloud</td>
<td><ul class="params">
<li>Enkripsi disk cloud mendukung semua jenis disk cloud dan jenis instance.</li>
<li>Hanya disk cloud yang dapat dienkripsi, bukan disk lokal.</li>
<li>Hanya disk data yang dapat dienkripsi, bukan disk sistem.</li>
<li>Disk tidak terenkripsi yang ada tidak dapat langsung dikonversi ke disk terenkripsi.</li>
<li>Disk cloud terenkripsi tidak dapat dikonversi ke disk cloud yang tidak terenkripsi.</li>
</ul></td>
</tr>
<tr>
<td>Batasan snapshot dan image</td>
<td><ul class="params">
<li>Snapshot yang dihasilkan oleh disk tidak terenkripsi yang ada tidak dapat langsung dikonversi ke snapshot terenkripsi.</li>
<li>Snapshot terenkripsi tidak dapat dikonversi ke snapshot yang tidak dienkripsi.</li>
<li>Image dengan snapshot terenkripsi tidak dapat dibagikan.</li>
<li>Snapshot terenkripsi dan image yang dibuat olehnya tidak dapat direplikasi di seluruh wilayah.</li>
</ul></td>
</tr>
<tr>
<td>Batasan Lainnya</td>
<td><ul class="params">
<li>Fitur enkripsi disk cloud bergantung pada KMS di wilayah yang sama.Jika Anda tidak memiliki permintaan operasi lain, Anda tidak perlu melakukan operasi tambahan di konsol KMS.</li>
<li>Saat Anda menggunakan fitur enkripsi disk cloud untuk pertama kalinya, Anda harus mengaktifkan KMS seperti yang diinstruksikan di halaman tersebut.Jika tidak, Anda tidak dapat membeli disk cloud terenkripsi.</li>
<li>Anda dapat mengueri CMK yang dibuat khusus oleh sistem untuk enkripsi disk cloud di konsol KMS, tetapi Anda tidak dapat menentukan, menghapus, atau mengubah CMK.</li>
</ul></td>
</tr>
</table>







## Penagihan
Enkripsi disk cloud, CMK, dan baca/tulis data disk cloud tidak dikenakan biaya tambahan.Namun, saat Anda mengelola disk cloud terenkripsi baik di konsol atau melalui API, KMS digunakan sebagai API dan operasi Manajemen Anda akan dihitung sebagai panggilan KMS di wilayah ini.Anda akan ditagih berdasarkan jumlah panggilan KMS.Untuk detailnya, lihat [Ikhtisar Penagihan KMS](https://cloud.tencent.com/document/product/573/34388).

Operasi Manajemen pada disk cloud terenkripsi meliputi:
- Membuat disk cloud terenkripsi
- Memasang disk cloud
- Melepas disk cloud
- Membuat snapshot
- Mengembalikan snapshot
>Pastikan Anda memiliki saldo akun yang cukup, jika tidak, operasi akan gagal.
>


## Membuat disk cloud terenkripsi
Anda dapat membuat disk cloud terenkripsi melalui tiga metode berikut:

### Membuat disk cloud terenkripsi di konsol
1.Masuk ke [Konsol CBS](https://console.cloud.tencent.com/cvm/cbs), pilih wilayah, dan klik **Create** (Buat).
2.Di kotak dialog **Purchase Data Disk** (Beli Disk Data), pilih **Enable disk encryption** (Aktifkan enkripsi disk).
>Jika Anda menggunakan enkripsi disk cloud di wilayah ini untuk pertama kalinya, lakukan otorisasi layanan Manajemen kunci terlebih dahulu.
>
3.Pilih konfigurasi disk cloud berdasarkan kebutuhan aktual Anda dan klik **Submit** (Kirim).
4.Setelah membeli disk cloud, Anda dapat melihat disk cloud terenkripsi yang telah dibuat di halaman [Daftar Disk Cloud](https://console.cloud.tencent.com/cvm/cbs).
Disk cloud terenkripsi baru berada dalam status **to be mounted** (akan dipasang), Anda dapat melihat [Memasang disk cloud](https://intl.cloud.tencent.com/document/product/362/5745) untuk memasang disk cloud ke instance CVM di zona ketersediaan yang sama.

### Membuat disk cloud terenkripsi dari snapshot
Lihat [Membuat disk cloud menggunakan snapshot](https://cloud.tencent.com/document/product/362/5757).Dengan memilih snapshot terenkripsi untuk membuat disk cloud, Anda dapat membuat disk cloud yang berisi data yang relevan dan terenkripsi.

### Membuat disk cloud terenkripsi melalui API
Anda dapat membuat disk cloud terenkripsi menggunakan [API CreateDisks](https://cloud.tencent.com/document/product/362/16312) dengan dua metode berikut:
- Konfigurasikan `Encrypt` sebagai `true`.
- Tentukan `SnapshotId` untuk snapshot terenkripsi.

## Mengubah status enkripsi data
Untuk mengubah status data yang ada di disk cloud dari tidak terenkripsi menjadi terenkripsi, kami sarankan Anda menjalankan perintah `rsync` di sistem Linux atau perintah `robocopy` di sistem Windows untuk menyalin data dari disk yang tidak terenkripsi ke disk terenkripsi yang baru.
Jika Anda perlu mengubah status data yang ada di disk cloud dari terenkripsi menjadi tidak terenkripsi, kami sarankan Anda menjalankan perintah yang sama untuk menyalin data dari disk terenkripsi ke disk tidak terenkripsi yang baru.


<style>
.params{margin-bottom:0px !important;}
</style>





