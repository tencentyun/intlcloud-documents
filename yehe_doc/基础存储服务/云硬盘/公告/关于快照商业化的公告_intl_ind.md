CBS snapshot menjalani pengujian beta sejak 2016, dan meluncurkan **formal commercialization** (komersialisasi formal) di Tencent Cloud China sejak pukul 00.00 pada tanggal 22 Januari 2019 dan Tencent Cloud International sejak 1 Maret 2019.Setelah komersialisasi, semua snapshot lama dan baru akan dikenakan biaya berdasarkan kapasitas yang digunakan.
> [Image](https://intl.cloud.tencent.com/document/product/213/4940) menggunakan layanan snapshot CBS untuk penyimpanan data.Akibatnya, image khusus yang disimpan akan memakan kapasitas snapshot Anda dan menimbulkan biaya.

## Detail Komersialisasi
### Tanggal dan lingkup komersialisasi snapshot
Komersialisasi snapshot berlaku untuk semua pengguna di Tencent Cloud China dan Tencent Cloud International.
Snapshot dikomersialkan di Tencent Cloud China pada titik waktu tertentu berikut:
- 00.00, 22 Januari 2019, Asia Pasifik Timur Laut (Tokyo) resmi dikomersialkan.
- 00.00, 23 Januari 2019, Hong Kong, Makao dan Taiwan, Tiongkok (Hong Kong), dan wilayah lain di luar Tiongkok Daratan resmi dikomersialkan.
- 00.00, 24 Januari 2019, Tiongkok Selatan (Shenzhen Finance), Tiongkok Selatan (Guangzhou Open), dan Tiongkok Timur (Shanghai Finance) resmi dikomersialkan.
- 00.00, 25 Januari 2019, Tiongkok Utara (Beijing), Tiongkok Timur (Shanghai), Tiongkok Selatan (Guangzhou), dan Tiongkok Barat Daya (Chengdu dan Chongqing) resmi dikomersialkan.

Snapshot dikomersialkan di Tencent Cloud International sejak 1 Maret 2019.

### Peningkatan layanan setelah komersialisasi
Setelah komersialisasi snapshot, Tencent Cloud akan memberikan layanan yang lebih baik kepada para pengguna.
>Berikut adalah nilai maksimum yang didukung di wilayah yang sama dengan menggunakan satu akun Tencent Cloud.

| Jenis Peningkatan | Sebelum Komersialisasi | Setelah Komersialisasi|
|---------|---------|---------|
| Jumlah snapshot | 7 kali jumlah disk CBS di wilayah | Setiap disk CBS dapat menyimpan hingga 64 snapshot.Harap perhatikan jumlah snapshot dan hapus yang tidak diperlukan untuk melegakan ruang penyimpanan |
| Total kapasitas snapshot | 20 TB | Tidak terbatas |
| Jumlah kebijakan snapshot terjadwal | 20 | 30 |
| Jumlah disk cloud yang dapat diikat ke kebijakan snapshot terjadwal | 100 | 200 |
| Kapasitas disk cloud maksimal yang didukung oleh snapshot terjadwal | 1000 GB | 16 TB |

### Snapshot dan image
- Image menggunakan layanan CBS snapshot untuk penyimpanan data.Ketika suatu image dibuat, sebuah snapshot secara otomatis dibuat dan diikat ke image yang sesuai.Untuk menghapus snapshot, Anda harus terlebih dahulu [menghapus imagenya](https://intl.cloud.tencent.com/document/product/213/6036).Anda dapat memeriksa detail image untuk mendapatkan informasi tentang snapshot yang berkaitan dengan image khusus tersebut.
- Ketika menggunakan image bersama, hanya akun Tencent Cloud yang membuat image bersama itulah yang harus membayar biaya snapshot terkait.Pengguna lainnya tidak perlu membayar.
- Snapshot terkait yang dibuat oleh image khusus ditagihkan berdasarkan kapasitas sebenarnya, yang dapat ditemukan di ikhtisar snapshot.
- Jika akun Tencent Cloud Anda terlambat membayar, Anda tidak bisa membuat image khusus. Jadi, pastikan Anda memiliki saldo yang cukup di akun Anda sebelum membuat image khusus.

### Penagihan snapshot
#### Aturan penagihan
- Cara penagihan: Anda dikenakan biaya sesuai dengan total kapasitas penyimpanan snapshot Anda.Setiap wilayah dikenakan biaya secara terpisah.Saat ini, CBS menggunakan cara **pay-as-you-go** (pembayaran sesuai pemakaian) dengan siklus tagihan per jam.
- Standar penagihan: penagihan snapshot berbeda-beda untuk setiap wilayah.Untuk informasi selengkapnya, lihat [Daftar Harga](https://intl.cloud.tencent.com/document/product/362/2413).
- Kebijakan pembekuan: jika akun Tencent Cloud Anda terlambat membayar, layanan snapshot akan segera ditangguhkan, termasuk pembuatan, pengembalian, replikasi lintas wilayah, dan kebijakan snapshot terjadwal.Semua snapshot akan dihapus jika akun terlambat membayar lebih dari 30 hari.

#### Tingkat gratis
Tencent Cloud menawarkan ruang penyimpanan gratis sebesar 50 GB untuk pengguna di Tiongkok.Perincian kebijakannya adalah sebagai berikut:
- Tingkat gratis berlaku untuk Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, dan Hong Kong (Tiongkok).Saat ini, wilayah luar negeri tidak didukung.
- Disk cloud di wilayah-wilayah yang disebutkan di atas yang berstatus selain `akan diambil alih` atau `dihentikan` mendapatkan ruang penyimpanan snapshot gratis sebesar 50 GB.
- Tingkat gratis ini akan dihapus secara bertahap pada bulan Juli 2020.

#### Contoh penagihan
Tabel berikut menjelaskan cara penyimpanan snapshot ditagihkan dalam berbagai jenis keadaan:

<table>
<tr>
<th>Wilayah</th>
<th nowrap="nowrap">Total kapasitas snapshot</th>
<th nowrap="nowrap">Kuantitas dan status disk cloud</th>
<th>Detail</th>
</tr>
<tr>
<td nowrap="nowrap">Tiongkok Utara (Beijing)</td>
<td>100GB</td>
<td nowrap="nowrap">1 disk cloud<br/><b>To be repossessed</b> (Akan diambil alih)</td>
<td><li>Saat ini tidak memenuhi syarat untuk tingkat gratis.Total kapasitas snapshot adalah 100 GB yang ditagihkan sesuai pemakaian setiap jam.</li><li>Tingkat gratis akan berlaku setelah disk cloud diperpanjang atau setelah disk cloud yang baru dibeli.Total kapasitas snapshot adalah 100GB - 50GB = 50GB yang ditagihkan sesuai pemakaian setiap jam.</li></td>
</tr>
<tr>
<td nowrap="nowrap">Hong Kong, Makau dan Taiwan, Tiongkok (Hong Kong)</td>
<td>60GB</td>
<td>1 disk cloud<br/><b>Mounted</b> (Terpasang)</td>
<td>Memenuhi syarat untuk tingkat gratis.Total kapasitas snapshot adalah 60GB - 50GB = 10GB yang ditagihkan sesuai pemakaian setiap jam.</td>
</tr>
<tr>
<td nowrap="nowrap">Pasifik Asia Tenggara (Singapura)</td>
<td>40GB</td>
<td>1 disk cloud<br/><b>Mounted</b> (Terpasang)</td>
<td>Tidak memenuhi syarat untuk tingkat gratis.Total kapasitas snapshot adalah 40GB yang ditagihkan sesuai pemakaian setiap jam.</td>
</tr>
</table>

## Snapshot manual dan snapshot terjadwal
Berikut adalah dua cara yang disediakan Tencent Cloud untuk membuat snapshot:
- Snapshot manual: Anda dapat membuat snapshot untuk data disk cloud secara manual pada titik waktu tertentu.Snapshot ini dapat digunakan untuk membuat lebih banyak disk cloud dengan data yang identik, atau untuk memulihkan disk cloud ke status saat ini nanti.Untuk informasi selengkapnya, lihat [Membuat Snapshot](https://intl.cloud.tencent.com/document/product/362/5755).
- Snapshot terjadwal: untuk bisnis yang terus diperbarui, Anda dapat menggunakan snapshot terjadwal untuk membuat pencadangan data berkelanjutan.Untuk mencapai pencadangan berkelanjutan data disk cloud selama periode tertentu, Anda hanya perlu mengonfigurasi kebijakan pencadangan dan mengaitkannya dengan disk cloud, yang secara signifikan meningkatkan keamanan data.Untuk informasi selengkapnya, lihat [Snapshot Terjadwal](https://intl.cloud.tencent.com/document/product/362/35238).

<a id="reduceoverhead"></a>
## Cara efektif mengurangi biaya snapshot setelah komersialisasi
### Jika Anda berencana untuk terus menggunakan snapshot
- Hapus snapshot yang tidak lagi digunakan.
- Hapus image khusus yang tidak lagi digunakan beserta snapshot terkaitnya.
- Kurangi frekuensi pembuatan snapshot untuk bisnis non-inti.
- Kurangi waktu penyimpanan snapshot untuk bisnis non-inti.

| Skenario Bisnis | Snapshot yang Direkomendasikan | Periode Penyimpanan |
|---------|---------|---------|
| Bisnis inti | Snapshot terjadwal, dengan kebijakan ditetapkan setiap sehari sekali. | 7-30 hari |
| Bisnis non-inti dan non-data | Snapshot terjadwal, dengan kebijakan ditetapkan setiap seminggu sekali. | 7 hari |
| Bisnis arsip | Snapshot manual dibuat dari waktu ke waktu sesuai kebutuhan bisnis | Satu bulan atau lebih |
| Bisnis pengujian | Snapshot manual dibuat dari waktu ke waktu sesuai kebutuhan bisnis | Segera dihapus setelah digunakan |

### Jika Anda berencana untuk berhenti menggunakan snapshot
- Periksa dan hapus snapshot yang sudah ada: periksa dan hapus snapshot yang disimpan di setiap wilayah.
- Periksa dan hapus image khusus yang sudah ada beserta snapshot terkaitnya: periksa dan hapus image khusus yang disimpan di setiap wilayah, kemudian hapus juga snapshot terkaitnya.
- Periksa dan modifikasi kebijakan snapshot terjadwal: periksa kebijakan penjadwalan untuk setiap wilayah, hapus atau hentikan kebijakan guna mencegah pembuatan snapshot terjadwal baru yang berkelanjutan.
