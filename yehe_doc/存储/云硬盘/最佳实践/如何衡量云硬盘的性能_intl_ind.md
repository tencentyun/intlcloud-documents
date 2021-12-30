## Metrik
Perangkat Tencent Cloud CBS memiliki kinerja dan harga yang beragam berdasarkan jenisnya.Untuk informasi selengkapnya, lihat [Jenis Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31636).Jika jumlah permintaan I/O rendah, disk cloud mungkin tidak dapat memberikan kinerja yang maksimal karena setiap aplikasi memiliki beban kerja yang berbeda-beda.
Metrik berikut biasa digunakan untuk mengukur kinerja disk cloud:

- IOPS: jumlah baca/tulis per detik.IOPS bervariasi menurut jenis drive yang mendasari perangkat penyimpanan.
- Throughput: volume data yang dibaca/ditulis per detik, dalam satuan MB/s.
- Latensi: waktu yang dibutuhkan untuk mengirim operasi I/O sampai menerima balasan (dalam detik).

## Alat Pengujian
FIO adalah alat untuk menguji kinerja disk.Alat ini digunakan untuk melakukan uji tekanan dan verifikasi pada perangkat keras.Dokumen ini menggunakan FIO sebagai contoh.
Sebaiknya Anda menggunakan FIO dengan mesin I/O libaio untuk melakukan pengujian.Harap menginstal FIO dan libaio dengan merujuk ke [Penginstalan Alat](#toolInstallation).

>
>- **Untuk menghindari kerusakan file penting dalam sistem, jangan lakukan uji FIO pada disk sistem**.
>- **Untuk menghindari kerusakan data yang disebabkan oleh kerusakan metadata sistem file yang mendasari, jangan lakukan pengujian pada disk data bisnis. **
>- Pastikan file `/etc/fstab` **TIDAK berisi** konfigurasi pemasangan disk yang akan diuji.Jika berisi konfigurasi tersebut, CVM mungkin gagal diluncurkan.

## Objek Pengujian yang Direkomendasikan
- Sebaiknya uji FIO dilakukan pada disk kosong yang tidak berisi data penting dan buat ulang sistem file-nya saat selesai melakukan pengujian.
- Saat menguji kinerja disk, sebaiknya Anda langsung menguji disk data mentah (seperti /dev/vdb).
- Ketika menguji kinerja sistem file, sebaiknya Anda menetapkan uji file yang spesifik (seperti /data/file).
<span id="toolInstallation"></span>
## Penginstalan Alat
1.Masuk ke CVM dengan mengikuti petunjuk dalam [Masuk ke Instance Linux Menggunakan Metode Masuk Standar](https://intl.cloud.tencent.com/document/product/213/5436).Kami menggunakan CVM yang menjalankan OS CentOS 7.6 sebagai contoh.
2.Jalankan perintah berikut untuk memeriksa apakah disk cloud selaras dengan 4KiB.
```
fdisk -lu
```
Seperti yang terlihat di bawah ini, jika nilai Start dalam output perintah dapat habis dibagi 8, artinya disk telah selaras dengan 4KiB.Jika tidak, lakukan penyelarasan 4KiB sebelum pengujian.
![](https://main.qcloudimg.com/raw/d5726510ea6408a36e11fc21da453137.png)
3.Jalankan perintah berikut secara berurutan untuk menginstal alat pengujian, FIO, dan libaio.
```
yum install libaio -y
```
```
yum install libaio-devel -y
```
```
yum install fio -y
```
Setelah selesai, mulailah menguji kinerja disk cloud dengan mengikuti petunjuk dalam contoh pengujian di bawah.

## Test Example (Contoh Pengujian)
Rumus pengujian untuk berbagai macam skenario pada dasarnya sama, kecuali parameter `rw`, `iodepth`, dan `bs` (block size/ukuran blok).Misalnya, setiap beban kerja memiliki `iodepth` optimal yang berbeda karena bergantung pada sensitivitas aplikasi Anda terhadap IOPS dan latensi.

Deskripsi parameter:

<table>
<tr>
<th nowrap="nowrap">Parameter</th>
<th>Remarks</th>
<th nowrap="nowrap">Sample value</th>
</tr>
<tr>
<td>bs</td>
<td>Ukuran blok per permintaan.Nilai yang valid meliputi 4k, 8k, dan 16k.</td>
<td>4k</td>
</tr>
<tr>
<td>ioengine</td>
<td>Mesin I/O.Sebaiknya Anda menggunakan mesin I/O async Linux.</td>
<td>libaio</td>
</tr>
<tr>
<td>iodepth</td>
<td>Kedalaman antrean permintaan I/O.</td>
<td>1</td>
</tr>
<tr>
<td>direct</td>
<td>Menetapkan mode langsung.<ul><li>True (1) menunjukkan bahwa pengidentifikasi O_DIRECT ditetapkan, cache I/O akan diabaikan, dan data akan ditulis secara langsung.</li><li>False (0) menunjukkan bahwa pengidentifikasi O_DIRECT tidak ditetapkan.</li></ul>Defaultnya adalah True (1).</td>
<td>1</td>
</tr>
<tr>
<td>rw</td>
<td>Mode baca dan tulis.Nilai valid meliputi read, write, randread, randwrite, randrw, dan rw, readwrite.</td>
<td>read</td>
</tr>
<tr>
<td>berbasis_waktu</td>
<td>Menentukan bahwa mode waktu digunakan.Parameter ini tidak perlu diatur selama FIO berjalan berdasarkan waktu.</td>
<td>N/A</td>
</tr>
<tr>
<td>runtime</td>
<td>Menetapkan durasi pengujian, yaitu runtime FIO.</td>
<td>600</td>
</tr>
<tr>
<td>refill_buffers</td>
<td>FIO akan mengisi ulang buffer I/O pada setiap pengiriman.Pengaturan defaultnya adalah mengisi buffer I/O hanya pada permulaan dan menggunakan ulang data.</td>
<td>N/A</td>
</tr>
<td>norandommap</td>
<td>Saat melakukan operasi I/O acak, FIO menimpa setiap blok file.Jika parameter ini ditetapkan, offset baru akan dipilih tanpa melihat riwayat I/O.</td>
<td>N/A</td>
</tr>
<tr>
<td>randrepeat</td>
<td>Menentukan apakah urutan acaknya dapat diulang.True (1) menunjukkan bahwa urutan acaknya dapat diulang.False (0) menunjukkan bahwa urutan acaknya tidak dapat diulang.Nilai defaultnya adalah True (1).</td>
<td>0</td>
</tr>
<td>pelaporan_kelompok</td>
<td>Statistik untuk keseluruhan kelompok dicetak ketika terdapat beberapa pekerjaan yang dilakukan bersamaan.</td>
<td>N/A</td>
</tr>
<tr>
<td>nama</td>
<td>Nama pekerjaan.</td>
<td>fio-read</td>
</tr>
<td>ukuran</td>
<td>Ruang alamat pengujian I/O.</td>
<td>100GB</td>
</tr>
<tr>
<td>namafile</td>
<td>Objek pengujian, yaitu nama disk yang akan diuji.</td>
<td>/dev/sdb</td>
</tr>
</table>

Kasus penggunaan umum adalah sebagai berikut:
- **bs=4k iodepth=1**: uji baca/tulis acak, yang dapat mencerminkan kinerja latensi suatu disk.
Jalankan perintah berikut untuk menguji latensi baca acak disk:
```
fio -bs=4k -ioengine=libaio -iodepth=1 -direct=1 -rw=randread -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randread-lat --size=10G -filename=/dev/vdb
```
Jalankan perintah berikut untuk menguji latensi tulis acak disk:
```
fio -bs=4k -ioengine=libaio -iodepth=1 -direct=1 -rw=randwrite -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randwrite-lat --size=10G -filename=/dev/vdb
```
Jalankan perintah berikut untuk menguji kinerja latensi gabungan baca dan tulis dari disk cloud SSD:
```
fio --bs=4k --ioengine=libaio --iodepth=1 --direct=1 --rw=randrw --time_based --runtime=100 --refill_buffers --norandommap --randrepeat=0 --group_reporting --name=fio-read --size=1G --filename=/dev/vdb
```
Gambar berikut menunjukkan output perintah:
![](https://main.qcloudimg.com/raw/39ffdf41ca9bd28808792b35482fafd0.png)

- **bs=128k iodepth = 32**: uji baca/tulis berurutan, dapat mencerminkan kinerja throughput disk.
Jalankan perintah berikut untuk menguji bandwidth throughput baca berurutan:
```
fio -bs=128k -ioengine=libaio -iodepth=32 -direct=1 -rw=read -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-read-throughput --size=10G -filename=/dev/vdb
```
Jalankan perintah berikut untuk menguji bandwidth throughput tulis berurutan:
```
fio -bs=128k -ioengine=libaio -iodepth=32 -direct=1 -rw=write -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-write-throughput --size=10G -filename=/dev/vdb
```
Jalankan perintah berikut untuk menguji kinerja throughput baca berurutan dari disk cloud SSD:
```
fio --bs=128k --ioengine=libaio --iodepth=32 --direct=1 --rw=read --time_based --runtime=100 --refill_buffers --norandommap --randrepeat=0 --group_reporting --name=fio-rw --size=1G --filename=/dev/vdb
```
Gambar berikut menunjukkan output perintah:
![](https://main.qcloudimg.com/raw/f21de73d7c20d32396d43b11dd756c26.png)

- **bs=4k iodepth=32**: uji baca/tulis acak, dapat mencerminkan kinerja IOPS hard disk.
Jalankan perintah berikut untuk menguji IOPS baca acak disk:
```
fio -bs=4k -ioengine=libaio -iodepth=32 -direct=1 -rw=randread -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randread-iops --size=10G -filename=/dev/vdb
```
Jalankan perintah berikut untuk menguji IOPS tulis acak disk:
```
fio -bs=4k -ioengine=libaio -iodepth=32 -direct=1 -rw=randwrite -time_based -runtime=600  -refill_buffers -norandommap -randrepeat=0 -group_reporting -name=fio-randwrite-iops --size=10G -filename=/dev/vdb
```
Uji kinerja IOPS baca acak disk cloud SSD.Ini ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/b6aaf207adffdb85ba7da487b4fd2ce9.png)
