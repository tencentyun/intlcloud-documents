## Ikhtisar
Membuat snapshot adalah metode penting untuk melakukan berbagi dan migrasi data.Disk cloud yang dibuat menggunakan snapshot memiliki semua data dalam snapshot.Anda dapat menggunakan snapshot untuk membuat disk cloud yang kapasitasnya lebih besar atau sama dengan kapasitas snapshot.
- Saat Anda menggunakan snapshot untuk membuat disk data dengan kapasitas yang sama dengan kapasitas snapshot, disk data tidak perlu diinisialisasi.Untuk membaca dan menulis ke dalamnya, Anda hanya perlu [memasang](https://intl.cloud.tencent.com/document/product/362/32401) dan memilih **Server Management** -> **Storage** -> **Disk Management** (Manajemen Server -> Penyimpanan -> Manajemen Disk) untuk mengaitkannya dengan CVM.
- Saat Anda menggunakan snapshot untuk membuat disk data yang kapasitasnya lebih besar daripada kapasitas snapshot, sistem hanya memperluas blok penyimpanan dan tidak memperluas sistem file atau mengubah format partisi.Setelah Anda [memasang](https://intl.cloud.tencent.com/document/product/362/32401) disk data baru, disk data baru tersebut hanya dapat menggunakan sistem file dan data snapshot sumber, dan tidak dapat menggunakan ruang disk baru.Anda perlu memperluas sistem file secara manual dan mengonversi format partisi.
Misalnya, jika Anda ingin disk data 3 TB dengan menggunakan snapshot disk data yang menggunakan format partisi MBR dan memiliki kapasitas 1 TB, Anda perlu memformat disk data dengan gaya partisi GPT karena ruang disk maksimum yang didukung di gaya partisi MBR adalah 2 TB.Harap dicatat bahwa operasi ini akan **delete original data** (menghapus data asli).

Dokumen ini menjelaskan cara menggunakan snapshot untuk membuat disk cloud di halaman [Daftar Snapshot](https://console.cloud.tencent.com/cvm/snapshot).Saat [membuat disk cloud](https://intl.cloud.tencent.com/document/product/362/5744), Anda dapat mengonfigurasi parameter **Snapshots** (Snapshot) untuk menentukan snapshot untuk membuat disk cloud.


## Petunjuk
### Membuat disk cloud dengan snapshot di konsol
1.Masuk ke halaman [Daftar Snapshot](https://console.cloud.tencent.com/cvm/snapshot).
2.Di baris snapshot target, klik **More** (Selengkapnya) dan pilih **Create Cloud Disk** (Buat Disk Cloud).
3.Di kotak dialog **Purchase Data Disk** (Beli Disk Data), konfigurasikan parameter berikut:
<table>
<tr>
<th width="12%">Parameter</th>
<th>Deskripsi</th>
</tr>
<tr>
<td>Zona Ketersediaan</td>
<td>Wajib Diisi.</br>Zona ketersediaan tempat disk cloud yang dibuat berada.Ini tidak dapat diubah setelah disk cloud dibuat.</td>
</tr>
<tr>
<td>Jenis Disk Cloud</td>
<td>Wajib Diisi.</br>Nilainya meliputi:<ul><li>Premium Cloud Storage</li><li>SSD Cloud Storage</li></ul></td>
</tr>
<tr>
<td>Kapasitas</td>
<td>Wajib Diisi.</br>CBS menyediakan kapasitas dan spesifikasi disk cloud berikut:<ul><li>Premium Cloud Storage: 50 hingga 16.000 GB</li><li>SSD Cloud Storage: 100 hingga 16.000 GB</li></ul>Saat Anda membuat disk cloud menggunakan snapshot, kapasitas disk tidak boleh lebih kecil dari kapasitas snapshot.Jika Anda tidak menentukan parameter ini, kapasitas disk sama dengan kapasitas snapshot secara default.</td>
</tr>
<tr>
<td>Snapshot</td>
<td>Opsional.Untuk menggunakan snapshot untuk membuat disk cloud, pilih **Create a Cloud Disk with a Snapshot** (Buat Disk Cloud dengan Snapshot) dan pilih snapshot yang diperlukan. <ul><li>Kapasitas disk sama dengan kapasitas snapshot secara default.Anda dapat menyesuaikan kapasitas agar lebih besar dari kapasitas snapshot.</li><li>Jenis disk sama dengan jenis snapshot secara default.Anda dapat mengubah jenis disk cloud.</li></ul></td>
</tr>
<tr>
<td>Nama Disk</td>
<td>Opsional.</br>Maksimum 20 karakter yang didukung.Harus dimulai dengan huruf, dan dapat berupa kombinasi huruf, angka, dan karakter khusus (`.`, `_`, `:`, dan `-`).Parameter ini dapat diubah setelah disk cloud dibuat.<ul><li>Jika Anda hanya membuat satu disk cloud, nama disk adalah nama dari disk cloud yang Anda buat.</li><li>Jika Anda membuat beberapa disk cloud pada satu waktu, nama disk yang dimasukkan akan digunakan sebagai awalan nama disk akhir, dalam format **disk name_number** (nama disk_nomor), misalnya, "nama disk_0" menjadi "nama disk_49".</li> </ul></td>
</tr>
<tr>
<td>Proyek</td>
<td>Wajib Diisi.</br>Saat membuat disk cloud, Anda dapat mengonfigurasi proyek tempat disk cloud itu berada.Nilai default-nya adalah **DEFAULT PROJECT**.</td>
</tr>
<tr>
<td>Tag</td>
<td>Opsional.</br>Saat membuat disk cloud, Anda dapat mengikat tag ke dalamnya.Tag digunakan untuk mengidentifikasi sumber daya cloud, membantu Anda dengan mudah mengategorikan dan mencari sumber daya cloud.Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/651">Tag</a>.</td>
</tr>
<tr>
<td>Cara Penagihan</td>
<td>Wajib Diisi.<li>Nilainya adalah **Pay as you go** (Bayar sesuai pemakaian).</li></ul></td>
</tr>
<tr>
<tr>
<td>Snapshot Terjadwal</td>
<td>Opsional.</br>Saat membuat disk cloud, Anda dapat memilih <b>Scheduled Snapshot</b> (Snapshot Terjadwal) untuk membuat snapshot untuk disk cloud secara berkala berdasarkan kebijakan snapshot terjadwal yang dibuat.Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/362/35238">Snapshot Terjadwal</a>.
</tr>
<tr>
<td>Kuantitas</td>
<td>Opsional.</br>Nilai default-nya adalah <b>1</b>, yang menunjukkan bahwa hanya satu disk cloud yang dibuat.Saat ini, hingga 50 disk cloud dapat dibuat sekaligus.</td>
</tr>
<tr>
<td>Periode</td>
<td></li><li>Jika <b>Billing Mode</b> (Cara Penagihan) diatur ke <b>Pay as you go</b> (Bayar sesuai pemakaian), parameter ini tidak terlibat.</li></ul></td>
</tr>
<tr>
<td>Perpanjangan Otomatis</td>
<td> <li>Jika <b>Billing Mode</b> (Cara Penagihan) diatur ke <b>Pay as you go</b> (Bayar sesuai pemakaian), parameter ini tidak terlibat.</li></ul></td>
</tr>
</table>
4.Klik <b>OK</b>.
- Jika <b>Billing Mode</b> (Cara Penagihan) adalah <b>Pay as you go</b> (Bayar sesuai pemakaian), proses pembuatan selesai.
<ol>
1.Setelah Anda mengonfirmasi konfigurasi Anda, pilih apakah akan menggunakan voucher berdasarkan kebutuhan aktualnya, lalu klik <b>OK</b>.
2.Selesaikan pembayaran.
</ol>

5.Anda dapat melihat disk cloud yang Anda buat di halaman daftar [Penyimpanan Blok Cloud](https://console.cloud.tencent.com/cvm/cbs).Disk cloud elastis baru berada dalam status *<b>To be mounted</b>(Akan dipasang).Untuk informasi selengkapnya tentang cara memasang disk cloud elastis ke CVM di zona ketersediaan yang sama, lihat [Memasang Disk Cloud](https://intl.cloud.tencent.com/document/product/362/32401).

### Menggunakan API untuk membuat disk cloud dari snapshot
Anda dapat menggunakan API `CreateDisks` untuk membuat disk cloud.Untuk informasi selengkapnya, lihat [CreateDisks](https://intl.cloud.tencent.com/document/product/362/16312).
