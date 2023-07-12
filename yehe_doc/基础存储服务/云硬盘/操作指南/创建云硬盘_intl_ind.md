## Ikhtisar

CBS memungkinkan Anda membuat disk cloud dan melampirkannya ke CVM mana pun di zona ketersediaan yang sama.Disk cloud diidentifikasi dan digunakan oleh CVM melalui pemetaan perangkat penyimpanan blok.Setelah dibuat, disk cloud dapat mencapai kinerja maksimumnya tanpa prefetch.
Anda dapat membuat berbagai jenis disk cloud CBS berdasarkan kebutuhan bisnis.Untuk informasi selengkapnya tentang jenis disk CBS, lihat [Jenis Disk Cloud](/doc/product/362/2353).

## Prasyarat

- Sebelum membuat disk cloud, Anda perlu [mendaftar ke Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985) dan menyelesaikan [verifikasi identitas](https://intl.cloud.tencent.com/document/product/378/3629).

## Petunjuk

<dx-tabs>
::: Membuat\sdisk\scloud\smelalui\skonsol
1.Masuk ke [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).
2.Pilih wilayah dan klik **Create** (Buat).
3.Di kotak dialog **Purchase Data Disk** (Beli Disk Data), konfigurasikan parameter berikut:

<table>
     <tr>
        <th width="15%">Parameter</th>
        <th>Deskripsi</th>
      </tr>
      <tr>
         <td>Zona Ketersediaan</td>
         <td>Wajib Diisi.</br>Zona ketersediaan tempat disk cloud yang dibuat berada.Ini tidak dapat diubah setelah disk cloud dibuat.</td>
       </tr>
       <tr>
          <td>Jenis Disk Cloud</td>
          <td>Wajib Diisi.</br>Tersedia empat jenis disk cloud CBS:<ul><li>Premium Cloud Storage</li><li>SSD</li><li>Enhanced SSD</li><li>Tremendous SSD.Jenis ini hanya dapat dibeli dengan instance CVM Standard Storage Optimized S5se.</li></ul></td>
       </tr>
       <tr>
          <td>Quick Disk Creation (Pembuatan Disk Cepat)</td>
          <td>Opsional.Untuk membuat disk cloud menggunakan snapshot, Anda perlu mencentang <b>Create a cloud disk with a snapshot (Buat disk cloud dengan snapshot)</b> dan pilih snapshot yang ingin Anda gunakan.<ul><li>Kapasitas disk cloud yang dibuat menggunakan snapshot sama dengan kapasitas snapshot secara default.Anda dapat menyesuaikan kapasitas disk.</li><li>Saat Anda membuat disk cloud menggunakan snapshot, jenis disk-nya sama dengan jenis disk sumber snapshot.Anda dapat mengubah jenis disk.</li></ul></td>
       </tr>
       <tr>
         <td>Kapasitas</td>
         <td>Wajib diisi.</br>CBS menyediakan kapasitas dan spesifikasi disk cloud berikut:<ul><li>Premium Cloud Storage: 10 hingga 32.000 GB</li><li>SSD: 20 hingga 32.000 GB</li><li>Enhanced SSD: 20 hingga 32.000 GB</li></ul>Saat Anda membuat disk cloud menggunakan snapshot, kapasitas disk tidak boleh lebih kecil dari kapasitas snapshot.Jika Anda tidak menentukan parameter ini, kapasitas disk sama dengan kapasitas snapshot secara default.</td>
       </tr>
       <tr>
          <td>Snapshot Terjadwal</td>
          <td>Opsional.<br>Anda dapat mengaitkan kebijakan snapshot terjadwal saat membuat disk cloud untuk mengelola snapshot disk cloud Anda secara teratur.Saat ini, Tencent Cloud menyediakan tingkat gratis 50 GB untuk setiap wilayah di Tiongkok Daratan.Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/362/32415">Ikhtisar Penagihan</a>.
       </tr>
       <tr>
          <td>Nama Disk</td>
          <td>Opsional.</br>Maksimum 128 karakter yang didukung.Harus diawali dengan huruf, dan dapat berupa kombinasi huruf, angka, dan karakter khusus (<code>.</code>, <code>_</code>, <code>:</code>, <code>-</code>).Parameter ini dapat dimodifikasi setelah disk cloud dibuat.<ul><li>Membuat disk cloud tunggal: nama disk yang dimasukkan adalah nama disk cloud yang Anda buat.</li><li>Pembuatan disk cloud dalam batch: nama disk yang dimasukkan adalah awalan nama disk cloud Anda, dalam format <b>nama disk_nomor</b>.</li></ul></td>
       </tr>
       <tr>
          <td>Proyek</td>
          <td>Wajib Diisi.</br>Saat membuat disk cloud, Anda dapat mengonfigurasi proyek tempat disk cloud itu berada.Nilai default-nya adalah <b>DEFAULT PROJECT</b>.</td>
       </tr>
           <tr>
           <td>Tag</td>
           <td>Opsional.</br>Saat membuat disk cloud, Anda dapat mengikat tag ke dalamnya.Tag digunakan untuk identifikasi, membantu Anda dengan mudah mengategorikan dan mencari sumber daya cloud.Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/651">Tag</a>.</td>
       </tr>
       <tr>
          <td>Cara Penagihan</td>
          <td>Wajib Diisi</br>Pembayaran CBS dilakukan sesuai pemakaian.</td>
       </tr>
       <tr>
          <td>Kuantitas</td>
          <td>Opsional.</br>Nilai default-nya adalah <b>1</b>, artinya hanya satu disk cloud yang dibuat.Saat ini, hingga 50 disk cloud dapat dibuat sekaligus.</td>
       </tr>
       <tr>
          <td>Periode</td>
          <td>Cara penagihan <b>bayar sesuai pemakaian</b> tidak melibatkan parameter ini.</td>
       </tr>
</table>


4.Klik **OK**.

- Jika **Billing Mode** (Cara Penagihan) adalah **Pay as you go** (Bayar sesuai pemakaian), proses pembuatan selesai.

<ol>
1.Setelah Anda mengonfirmasi konfigurasi Anda, pilih apakah akan menggunakan voucher berdasarkan kebutuhan aktual, lalu klik **Confirm** (Konfirmasi).
2.Selesaikan pembayaran.
</ol>

5.Anda dapat melihat disk cloud yang Anda buat di halaman daftar [Penyimpanan Blok Cloud](https://console.cloud.tencent.com/cvm/cbs).Disk cloud elastis yang baru berada dalam status **To be attached** (Akan dilampirkan).Untuk melampirkannya ke instance CVM di zona ketersediaan yang sama, lihat [Melampirkan Disk Cloud](https://intl.cloud.tencent.com/document/product/362/32401).

:::
::: Membuat\sdisk\scloud\smenggunakan\ssnapshot
Jika ingin membuat disk cloud yang berisi semua data saat dibuat, Anda dapat [membuat disk cloud menggunakan snapshot](https://intl.cloud.tencent.com/document/product/362/5757).
:::
::: Membuat\sdisk\scloud\smenggunakan\sAPI
Anda dapat menggunakan API `CreateDisks` untuk membuat disk cloud.Untuk informasi selengkapnya, lihat [CreateDisks](https://intl.cloud.tencent.com/document/product/362/16312).
:::
</dx-tabs>
