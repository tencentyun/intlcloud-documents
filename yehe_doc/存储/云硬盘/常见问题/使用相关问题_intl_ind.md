### Skenario apa yang ideal untuk disk cloud?
- Anda dapat [membeli](https://intl.cloud.tencent.com/document/product/362/5744) dan [memasang](https://intl.cloud.tencent.com/document/product/362/32401) disk cloud elastis untuk menggunakannya sebagai disk data saat ruang disk di CVM Anda tidak mencukupi.
- Anda dapat membeli dan memasang disk cloud elastis untuk menggunakannya sebagai disk data saat Anda membeli CVM tanpa disk data tambahan.
- Saat Anda memiliki 10 GB data penting yang disimpan dalam disk cloud elastis di CVM A dan perlu membagikan data tersebut dengan CVM B. Anda dapat langsung [melepas](https://intl.cloud.tencent.com/document/product/362/32400) disk dari CVM A, lalu [memasang](https://intl.cloud.tencent.com/document/product/362/32401) ke CVM B.
- Ketika satu disk cloud berukuran maksimum tidak dapat memenuhi persyaratan penyimpanan Anda, Anda dapat membeli beberapa disk cloud dengan kapasitas yang sama dan mengonfigurasi volume logis LVM untuk menyediakan kapasitas disk yang lebih besar.
- Ketika kinerja I/O dari satu disk tidak dapat memenuhi persyaratan bisnis Anda, Anda dapat membeli beberapa disk cloud dan mengonfigurasi RAID 0, RIAD 10, dll., untuk meningkatkan kinerja I/O.

Untuk informasi selengkapnya, lihat [Kasus Penggunaan](https://intl.cloud.tencent.com/document/product/362/3065).

### Bagaimana cara memilih disk cloud?
Tentukan kasus penggunaan Anda sebelum memilih jenis disk.
- Untuk kasus penggunaan umum termasuk aplikasi Web/APP, pemrosesan logis, dan situs berukuran kecil dan menengah, kami menyarankan Anda memilih Premium Cloud Storage sebagai solusi yang lebih hemat biaya.
- Untuk basis data berukuran sedang dan pengguna pemrosesan image, kami merekomendasikan SSD untuk kinerja yang lebih baik.
- Untuk kasus penggunaan dengan persyaratan tinggi untuk beban kerja dan kinerja, termasuk basis data besar, bisnis video, NoSQL, dan Elasticsearch, kami menyarankan Anda memilih Enhanced SSD untuk kinerja optimal dan latensi penyimpanan minimum.


### Apa saja item yang harus saya perhatikan saat menggunakan disk cloud?
- Untuk disk cloud yang dibeli secara terpisah, gunakan UUID atau label sistem file sebagai ID sistem file saat mengonfigurasi informasi sistem file statis `fstab`.Ini akan memastikan konsistensi nama kernel dari disk pada CVM ketika disk cloud dilepas dan dipasang kembali.
- Jika disk cloud kedaluwarsa sebelum CVM, disk cloud akan dibatasi, dilepas, atau bahkan diambil alih dalam jangka waktu tertentu.Untuk mencegah gangguan bisnis, harap perhatikan tanggal kedaluwarsa disk cloud dan perbarui segera.
- Pertimbangkan untuk menggunakan opsi `nofail` saat mengonfigurasi `fstab` jika melepas disk cloud dari CVM Anda tidak terlalu memengaruhi bisnis inti Anda.Ini mencegah CVM melaporkan kesalahan saat dimulai ulang setelah disk cloud dilepas.
- Kami menyarankan Anda menjalankan `san policy=OnlineAll` di `diskpart` sebelum menggunakan disk cloud di Windows.
- Saat melepas disk cloud dari Windows, kami menyarankan Anda untuk terlebih dahulu menghentikan semua operasi baca/tulis pada disk, dan lakukan operasi `offline`.

### Jika image khusus dan snapshot disk data digunakan, bagaimana cara memasang disk data secara otomatis saat memulai instance baru?
Untuk informasi selengkapnya, lihat bagian “Pemasangan Otomatis” di [Memasang Disk Cloud](https://intl.cloud.tencent.com/document/product/362/32401).

### Bagaimana cara membeli disk cloud?
Anda dapat membeli disk cloud dengan membuatnya melalui konsol atau API.Untuk informasi selengkapnya, lihat [Membuat Disk Cloud](https://intl.cloud.tencent.com/document/product/362/5744).

### Bagaimana cara melihat detail disk cloud?
1.Masuk ke [konsol CBS](https://console.cloud.tencent.com/cvm/cbs/index).
2.Di bagian atas halaman **Cloud Block Storage**, pilih wilayah tempat disk yang ingin Anda lihat berada.
3.Temukan disk dalam daftar, dan lihat informasi disk.
Untuk melihat informasi selengkapnya, klik ID/Nama disk untuk masuk ke halaman detail.


### Bagaimana cara melihat penggunaan disk cloud di konsol?

Cloud Monitor akan otomatis diaktifkan setelah instance CVM dibuat.Anda dapat melihat penggunaan disk cloud yang diinisialisasi yang dipasang ke CVM dengan mengikuti langkah-langkah di bawah ini:
1.Masuk ke [konsol CVM](https://console.cloud.tencent.com/cvm/instance/index) dan akses halaman **Instances** (Instance).
2.Pilih ID/Nama instance target untuk mengakses halaman detail.
3.Klik tab **Monitoring** (Pemantauan) untuk melihat penggunaan disk instance.

### Apa operasi disk cloud yang paling umum?
Untuk informasi selengkapnya, lihat [Ikhtisar Operasi](https://intl.cloud.tencent.com/document/product/362/33140).


### Mengapa saya tidak bisa menemukan CVM tempat saya ingin memasang disk cloud?
Disk cloud tidak dapat dipasang di seluruh zona ketersediaan.Pastikan instance CVM yang ingin Anda gunakan belum dirilis dan berada di wilayah dan zona ketersediaan yang sama dengan disk cloud Anda.

### Mengapa saya tidak dapat melihat kapasitas disk cloud baru yang saya pasang ke instance CVM?
Beberapa CVM Linux mungkin tidak mengenali disk cloud elastis.Anda harus terlebih dahulu mengaktifkan fungsi hot swapping disk di CVM.Untuk informasi selengkapnya, lihat [Mengaktifkan fungsi hot swapping disk](https://intl.cloud.tencent.com/document/product/362/32401#modprobeacpiphp).

Setelah memasang disk cloud secara manual, Anda harus melakukan operasi berikutnya yang ditunjukkan di bawah ini agar disk cloud dapat digunakan.
<table>
<tr>
<th>Mode pembuatan</th>
<th>Kapasitas disk cloud</th>
<th>Operasi berikutnya</th>
</tr>
<tr>
<td rowspan="2">Buat langsung</td>
<td>Kapasitas disk cloud < 2 TB</td>
<td><a href="https://intl.cloud.tencent.com/document/product/362/31597">Menginisialisasi disk cloud (< 2 TB)</a></td>
</tr>
<tr>
<td>Kapasitas disk cloud ≥ 2 TB</td>
<td><a href="https://intl.cloud.tencent.com/document/product/362/31598">Menginisialisasi disk cloud (≥ 2 TB)</a></td>
</tr>
<tr>
<td  rowspan="3">Buat dari snapshot</td>
<td>Kapasitas disk cloud = Kapasitas snapshot</td>
<td><ul class="params"><li>Memasang ke CVM Windows: setelah masuk ke instance, buat disk online melalui **Server Management** (Manajemen Server) > **Storage** (Penyimpanan) > **Disk Management** (Manajemen Disk).</li>
<li>Memasang ke CVM Linux: setelah masuk ke instance, jalankan perintah <code>mount <disk partition> <mount point></code>, misalnya <code>mount /dev/vdb /mnt</code>.</li>
</ul>
</li></td>
</tr>
</tr>
<tr>
<td nowrap="nowrap">Kapasitas snapshot < Kapasitas disk cloud ≤ 2 TB <br/>atau<br/>2 TB < Kapasitas snapshot < Kapasitas disk cloud</td>
<td><ul class="params"><li>Memasang ke CVM Windows: <a href="https://intl.cloud.tencent.com/document/product/362/31601">memperluas partisi dan sistem file (Windows)</a></li><li>Memasang ke CVM Linux: <a href="https://intl.cloud.tencent.com/document/product/362/31602">memperluas partisi dan sistem file (Linux)</a></li></ul></td>
</tr>
<tr>
<td>Kapasitas snapshot ≤ 2 TB < Kapasitas disk cloud</td>
<td nowrap="nowrap"><ul class="params"><li>Jika snapshot menggunakan format partisi MBR:</li>lihat <a href="https://intl.cloud.tencent.com/document/product/362/31598">Menginisialisasi Disk Cloud (Lebih Besar dari 2 TB)</a> untuk menggunakan partisi GPT.<b>Operasi ini akan menghapus data asli.</b><li>Jika snapshot menggunakan format partisi GPT:<ul><li>Memasang ke CVM Windows:<a href="https://intl.cloud.tencent.com/document/product/362/31601">memperluas partisi dan sistem file (Windows)</a></li><li>Memasang ke CVM Linux:<a href="https://intl.cloud.tencent.com/document/product/362/31602">memperluas partisi dan sistem file (Linux)</a></li></ul></td>
</tr>
</table>

<style>
.params{margin-bottom:0px !important;}
</style>


### Bagaimana cara mempartisi dan memformat disk cloud yang terpasang?
Untuk informasi selengkapnya, lihat [Menginisialisasi Disk Cloud (Lebih Kecil dari 2 TB)](https://intl.cloud.tencent.com/document/product/362/31597) atau [Menginisialisasi Disk Cloud (Lebih besar dari 2 TB)](https://intl.cloud.tencent.com/document/product/362/31598).

### Apa hubungan antara penulisan data dan pemformatan partisi?
Disk data baru atau partisi disk data harus diformat sebelum digunakan.Disk juga harus direkam dengan struktur data.Memformat disk menetapkan sistem file pada disk data untuk penulisan data.Ukuran data tulis bervariasi menurut sistem file:
- Untuk Windows:
- Pemformatan cepat: menetapkan sistem file hanya ke partisi dan menulis ulang tabel direktori dengan sedikit penggunaan kapasitas disk Anda.
- Pemformatan standar: selain tugas pemformatan cepat, pemformatan normal memindai sektor partisi per sektor untuk mengidentifikasi dan menandai sektor buruk, dan mengisi blok kosong di disk cloud, yang berarti pada dasarnya menulis data ke seluruh disk.Oleh karena itu, kapasitas snapshot pertama mendekati kapasitas disk cloud.
- Untuk Linux: setelah disk cloud diformat dan sebelum instance ditulis dengan data, kapasitas snapshot pertama bergantung pada format sistem file disk.

### Dapatkah kapasitas disk data dan kapasitas disk sistem digabungkan?
Tidak. Untuk meningkatkan kapasitas penyimpanan, Anda perlu [memperluas disk data atau disk sistem](https://intl.cloud.tencent.com/document/product/362/5747).

### Setelah memperluas disk cloud saya, apakah saya perlu melepas partisi yang ada saat membuat partisi terpisah baru di Linux?
Ya.Untuk melakukannya, ikuti langkah-langkah di bawah ini:
1.Jalankan perintah berikut untuk melepas disk data.
```
umount <Mount point>
```
Jika titik pemasangan adalah `/data`, jalankan perintah berikut:
```
umount /data
```
2.Lepas sistem file dari semua partisi pada disk cloud, dan lakukan operasi selanjutnya.Anda dapat menjalankan perintah lagi untuk mengonfirmasi bahwa operasi pelepasan berhasil.
```
mount | grep '<Disk path>'
```
Jika pengembaliannya nol, semua sistem file telah dilepas dari partisi di disk cloud.


### Dapatkah beberapa CVM mengakses disk cloud?
Tidak. Anda dapat memasang maksimal 20 disk cloud ke CVM yang sama, tetapi Anda tidak dapat memasang disk cloud yang sama ke beberapa CVM.Anda hanya dapat berbagi data dengan [melepas disk data](https://intl.cloud.tencent.com/document/product/362/32400) dari CVM A lalu [memasang](https://intl.cloud.tencent.com/document/product/362/32401) ke CVM B.

### Bagaimana cara mengidentifikasi disk cloud dengan ukuran dan jenis yang sama yang dipasang ke CVM yang sama?
- Di Linux, Anda dapat melihat hubungan antara disk cloud elastis dan nama perangkat dengan menjalankan perintah berikut:
```
ls -l /dev/disk/by-id
```
![](https://main.qcloudimg.com/raw/66b6a19695ef4ba21b74ce0cd96503db.png)
- Di Windows, Anda dapat melihat hubungannya dengan menjalankan perintah berikut:
```
wmic diskdrive get caption,deviceid,serialnumber
```
Atau
```
wmic path win32_physicalmedia get SerialNumber,Tag
```
![](https://main.qcloudimg.com/raw/e91aa2f938ddda304844d7ac28840859.png)

### Dapatkah saya mengubah disk sistem CVM dari disk lokal ke disk cloud?
Ya.Untuk melakukannya, ikuti langkah-langkah di bawah ini:
>!Lihat [Membuat Image Khusus](https://intl.cloud.tencent.com/document/product/213/4942) dan [Membuat Snapshot](https://intl.cloud.tencent.com/document/product/362/5755) untuk membuat cadangan data sebelum melakukan operasi untuk memastikan keamanan data.
>

1.Masuk ke [konsol CVM](https://console.cloud.tencent.com/cvm/instance/index) dan akses halaman **Instances** (Instance).
2.Temukan instance yang ingin Anda ubah disknya, pilih **More** (Selengkapnya) > **Instance Status** (Status Instance) > **Shutdown** (Matikan) di bawah kolom **Operation** (Operasi) untuk mematikan instance yang dipilih.
3.Setelah instance dimatikan, pilih **More** (Selengkapnya) > **Resource Adjustment** > (Penyesuaian Sumber Daya) **Change Disk Media Type** (Ubah Jenis Media Disk).
4.Di jendela pop-up, pilih jenis disk cloud target, beri centang pada **I have read and agreed to Rules for Changing Disk Media Type** (Saya telah membaca dan menyetujui Aturan untuk Mengubah Jenis Media Disk), dan klik **Change Now** (Ubah Sekarang).
5.Periksa kembali informasinya, lakukan pembayaran jika berlaku, dan tunggu hingga prosesnya selesai.
>?
>
>- Untuk informasi selengkapnya, lihat [Mengubah Jenis Media Disk](https://intl.cloud.tencent.com/document/product/213/32365).


### Dapatkah saya melepas disk data yang disertakan dengan CVM?
Sejak November 2017, disk data yang dibeli dengan CVM dapat dilepas dan dipasang kembali.Disk data yang dipasang ulang ke CVM dengan tanggal kedaluwarsa yang berbeda dapat mengakibatkan masalah Manajemen siklus hidup.Kami menyediakan berbagai opsi seperti penyelarasan tanggal kedaluwarsa dan konfigurasi perpanjangan otomatis agar Anda dapat mengelola masalah siklus hidup disk data dengan lebih baik.Kami menyarankan Anda untuk berhati-hati memilih opsi yang sesuai untuk menghindari kehilangan data yang disebabkan oleh kedaluwarsa disk.

### Mengapa disk cloud terpisah yang saya buat dirilis bersama dengan instance saya?
Saat memasang disk cloud, Anda dapat memutuskan apakah disk cloud harus dirilis dengan instance secara otomatis.Ini dapat dikonfigurasi melalui [konsol CBS](https://console.cloud.tencent.com/cvm/cbs/index) atau API [ModifyDiskAttributes](https://intl.cloud.tencent.com/document/product/362/15659).


### Apa yang harus saya lakukan jika saya kehilangan data setelah memulai ulang instance Linux saya?
Ikuti langkah-langkah di bawah ini jika Anda kehilangan semua data dalam direktori (seperti /data) setelah memulai ulang karena pelepasan partisi data disk:
1.Jalankan perintah `fdisk -l` untuk melihat partisi yang dilepas.
2.Jalankan perintah `mount /dev/vdb /data` untuk memasang partisi.
3.Jalankan perintah `df -h` untuk melihat apakah partisi berhasil dipasang.
4.Selesaikan konfigurasi [pemasangan otomatis](https://intl.cloud.tencent.com/document/product/362/32401#.E6.8C.82.E8.BD.BD.E6.95.B0.E6.8D.AE.E7.9B.98.EF.BC.88linux.EF.BC.89).Kemudian disk cloud akan dipasang secara otomatis saat Anda memulai instance Linux.

### Saat saya melepas disk cloud, apakah datanya akan hilang?
Data di disk cloud tidak akan diubah selama pemasangan atau pelepasan.Untuk memastikan konsistensi data, kami sangat menyarankan Anda mengikuti langkah-langkah di bawah ini:
- Di Linux, masuk ke instance CVM dan jalankan perintah `umount` (lepaskan) pada disk cloud.Setelah perintah dijalankan, masuk ke konsol CVM untuk melepas disk cloud.
- Di Windows, hentikan semua operasi baca dan tulis di semua sistem file disk cloud sebelum melakukan pelepasan.Jika tidak, data yang belum selesai dibaca atau ditulis akan hilang.

### Bagaimana cara melepas disk cloud elastis?
Untuk informasi selengkapnya, lihat [Melepas Disk Cloud](https://intl.cloud.tencent.com/document/product/362/32400).

### Apa yang terjadi pada sistem setelah disk cloud saya kedaluwarsa?
Instruksi berikut hanya berlaku untuk disk cloud elastis yang mendukung pelepasan.Disk cloud non-elastis yang tidak mendukung pelepasan memiliki siklus hidup yang sama dengan CVM.Untuk informasi selengkapnya, lihat [Pembayaran Jatuh Tempo](https://intl.cloud.tencent.com/document/product/213/2181).


- Disk cloud yang dibayar sesuai pemakaian:
- Anda dapat terus menggunakan disk cloud yang dibayar sesuai pemakaian selama 2 jam sejak saldo akun Anda menjadi negatif.Anda akan ditagih untuk periode ini.Setelah 2 jam, layanan akan ditangguhkan dan disk cloud hanya akan menyimpan data.Hingga data benar-benar terhapus, Anda tetap akan ditagih sesuai standar penagihan meskipun saldo akun negatif.
- Jika akun Tencent Cloud Anda diisi hingga saldo menjadi positif dalam waktu 15 hari setelah layanan disk cloud ditangguhkan, disk dapat dipulihkan.
- Jika saldo akun tetap negatif selama lebih dari 15 hari setelah layanan disk cloud ditangguhkan, disk yang dibayar sesuai pemakaian akan diambil alih.Semua data akan dihapus dan **tidak dapat dipulihkan**.Saat disk cloud Anda diambil alih, pembuat akun Tencent Cloud dan semua kolaborator akan menerima pemberitahuan melalui email, SMS, dan Pusat Pesan konsol.

Silakan hubungi 4009100100 jika Anda memerlukan informasi lebih lanjut.

### Dapatkah saya mengubah jenis disk cloud setelah pembelian berhasil dilakukan?
Tidak. Namun, Anda dapat membuat snapshot untuk cadangan data dan kemudian menggunakan snapshot tersebut untuk membuat disk cloud dari jenis yang Anda butuhkan.

### Dapatkah saya menyesuaikan kapasitas disk cloud setelah pembelian berhasil dilakukan?
Ya.Disk cloud mendukung penyesuaian kapasitas.Kapasitas disk cloud dapat [diperluas](https://intl.cloud.tencent.com/document/product/362/31600), tetapi tidak dapat dikurangi.

### Apakah saya harus mematikan instance CVM sebelum perluasan disk cloud?
Tidak. Harap dicatat bahwa Anda perlu menetapkan kapasitas yang diperluas ke partisi yang ada, atau memformatnya menjadi partisi baru yang terpisah.Petunjuk pada sistem operasi CVM:[Memperluas Partisi dan Sistem File (Windows)](https://intl.cloud.tencent.com/document/product/362/31601) atau [Memperluas Partisi dan Sistem File (Linux)](https://intl.cloud.tencent.com/document/product/362/31602).

### Apa saja persyaratan untuk memperluas sistem file?
Hanya disk cloud yang mendukung perluasan.Disk lokal tidak dapat diperluas.Untuk informasi selengkapnya, lihat [Skenario Perluasan Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31600).
>!
> - Kami sangat menyarankan Anda membuat snapshot sebelum melakukan perluasan untuk memastikan keamanan data.
> - Jika kapasitas maksimum disk cloud tidak dapat memenuhi kebutuhan bisnis Anda, silakan coba [membangun grup RAID](https://intl.cloud.tencent.com/document/product/362/2932) atau [membangun volume logis LVM dengan beberapa disk cloud elastis](https://intl.cloud.tencent.com/document/product/362/2933).
> - Partisi MBR mendukung disk dengan kapasitas maksimum 2 TB.Saat Anda mempartisi disk dengan kapasitas lebih besar dari 2 TB, kami menyarankan Anda membuat dan memasang disk data baru dan menggunakan format partisi GPT untuk menyalin data.

### Bagaimana cara memperluas disk cloud?
Untuk informasi selengkapnya tentang operasi perluasan, lihat [Skenario Perluasan Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31600).

### Mengapa kapasitas tampak tidak berubah setelah saya memperluas disk data saya?
Perluasan di konsol hanya meningkatkan kapasitas penyimpanan disk data.Anda juga perlu masuk ke instance CVM Anda dan memperluas partisi dan sistem file.Untuk informasi selengkapnya, lihat:
- [Memperluas Partisi dan Sistem File (Windows)](https://intl.cloud.tencent.com/document/product/362/31601)
- [Memperluas Partisi dan Sistem File (Linux)](https://intl.cloud.tencent.com/document/product/362/31602)


### Apakah CVM mendukung perluasan CPU/memori?
Jika disk sistem CVM adalah disk cloud, Anda dapat menyesuaikan CPU dan memorinya.

### Apa yang harus saya lakukan jika disk cloud dipartisi dalam format MBR dan tidak dapat diperluas?
Partisi MBR mendukung disk dengan kapasitas maksimum 2 TB.Saat Anda mempartisi disk dengan kapasitas lebih besar dari 2 TB, kami menyarankan Anda membuat dan memasang disk data baru dan menggunakan format partisi GPT untuk menyalin data.

### Apa yang harus saya lakukan jika disk cloud tidak dapat memenuhi kebutuhan bisnis saya bahkan pada kapasitas maksimumnya?
Kami menyarankan Anda [membangun grup RAID](https://intl.cloud.tencent.com/document/product/362/2932) atau [membangun volume logis LVM dengan beberapa disk cloud elastis](https://intl.cloud.tencent.com/document/product/362/2933).

### Bagaimana cara membangun grup RAID dengan menggunakan beberapa disk cloud elastis?
Untuk informasi selengkapnya, lihat [Membangun Grup RAID](https://intl.cloud.tencent.com/document/product/362/2932).

### Bagaimana cara membangun volume logis LVM dengan menggunakan beberapa disk cloud elastis?
Untuk informasi selengkapnya, lihat [Membangun Volume Logis LVM dengan Beberapa Disk Cloud Elastis](https://intl.cloud.tencent.com/document/product/362/2933).

### Bagaimana cara mengekspor data dari disk cloud?
Anda dapat menggunakan FTP untuk mengunggah dan mengunduh data.Untuk informasi selengkapnya, lihat [Membangun Layanan FTP (Windows)](https://intl.cloud.tencent.com/document/product/213/10414) dan [Membangun Layanan FTP (Linux)](https://intl.cloud.tencent.com/document/product/213/10912).

### Apa yang terjadi pada data saat CVM dihentikan?
- Siklus hidup disk sistem sama dengan CVM.Ketika CVM dihentikan, data yang disimpan dalam disk sistem juga akan dihentikan.
- Siklus hidup disk data (yaitu, disk cloud elastis) tidak bergantung pada CVM.Anda dapat memutuskan apakah disk cloud elastis dan datanya akan disimpan setelah CVM kedaluwarsa.

Oleh karena itu, kami menyarankan Anda menggunakan disk cloud elastis untuk menyimpan data yang perlu disimpan untuk jangka panjang.
### Bagaimana cara memulihkan disk cloud setelah diformat?
Disk cloud tidak dapat dipulihkan setelah diformat.Sebaiknya Anda [membuat snapshot](https://intl.cloud.tencent.com/document/product/362/5755) sebelum memformat disk.

### Bagaimana cara menghapus disk cloud?
- Siklus hidup disk sistem sama dengan CVM.Disk hanya dapat dihapus ketika [instance CVM dihentikan](https://intl.cloud.tencent.com/document/product/213/4930).
- Siklus hidup disk data (yaitu, disk cloud elastis) tidak bergantung pada CVM.Disk dapat dihapus secara terpisah.Untuk informasi selengkapnya, lihat [Menghentikan disk cloud](https://intl.cloud.tencent.com/document/product/362/32399).

### Dapatkah disk sistem saya dipartisi?
Tidak.


### Bagaimana cara memperbarui informasi pemasangan di titik pemasangan?
LinuxOS mendukung perintah `systemd mount` yang akan menghasilkan file konfigurasi pemasangan di atas file .mount yang ada.Pemasangan ke direktori `/run/systemd/generator/` yang sama akan terpengaruh oleh perintah ini.
#### Masalah
Asumsikan Anda telah memasang disk data vdb ke direktori `/opt/apps` (jalankan perintah `mount -a` pada file fstab berdasarkan uuid disk).Sekarang, Anda ingin memasang vdc disk data baru ke direktori yang sama dan mengganti yang lama.Jika Anda langsung memasang vdc ke direktori, Anda tidak akan dapat membaca data.
#### Solusi
1.Hapus konfigurasi titik pemasangan yang sesuai (misalnya, jalankan perintah `rm /run/systemd/generator/opt-apps.mount`).
2.Jalankan perintah `reload` (misalnya, gunakan `systemctl daemon-reload`).
3.Pasang disk data (misalnya, jalankan perintah `mount /dev/vdc /opt/apps`).


