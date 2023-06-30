## Deskripsi Kesalahan
CVM Linux mengalami masalah memori, seperti kecepatan respons layanan yang lambat, kegagalan login CVM, atau Kehabisan Memori (OOM).

## Kemungkinan Alasan
Masalah ini mungkin disebabkan oleh penggunaan memori yang tinggi dari instans, yaitu, penggunaan memori umumnya tetap di atas 90%.


## Pendekatan Pemecahan Masalah
1. Lakukan [prosedur pemecahan masalah](#ProcessingSteps) untuk memeriksa apakah penggunaan memori terlalu tinggi.
2. Lihat [analisis masalah memori](#OtherProcessingSteps) untuk menemukan penyebab masalah.

## Prosedur Pemecahan Masalah[](id:ProcessingSteps)
1. Ikuti [petunjuk](#RelatedOperations) untuk memeriksa apakah penggunaan memori terlalu tinggi.
 - Jika ya, lanjutkan ke langkah berikutnya.
 - Jika tidak, lihat [analisis masalah memori](#OtherProcessingSteps) untuk menemukan penyebab masalah.
2. Login ke CVM, jalankan perintah `top`, dan tekan **M** untuk memeriksa apakah ada proses di kolom “RES” dan “SHR” menggunakan banyak memori.
  - Jika tidak, lanjutkan ke langkah berikutnya.
  - Jika ya, lakukan operasi seperti yang diinstruksikan dalam [analisis proses](https://intl.cloud.tencent.com/document/product/213/32387) menurut jenis proses.
3. Jalankan perintah berikut untuk memeriksa penggunaan memori bersama.
```
cat /proc/meminfo | grep -i shmem
```
Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/269ca888f6f0232a63705b6f9fd578a8.png)
4. Jalankan perintah berikut untuk memeriksa penggunaan memori slab yang tidak dapat diklaim kembali.
```
cat /proc/meminfo | grep -i SUnreclaim
```
Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/9e6c84eb5bfb0be315fc39d1b768d168.png)
5. Jalankan perintah berikut untuk memeriksa apakah ada halaman besar.
```
cat /proc/meminfo | grep -iE "HugePages_Total|Hugepagesize"
```
Informasi berikut akan muncul:
![](https://main.qcloudimg.com/raw/aae7ce06f7034c123c26ef92265b82ea.png)
 - Jika output `HugePages_Total` adalah `0`, lihat [analisis masalah memori](#OtherProcessingSteps) untuk menemukan penyebab masalah.
 - Jika hasil `HugePages_Total` bukan `0`, ada halaman besar. Ukuran halaman yang besar sama dengan `HugePages_Total * Hugepagesize`. Periksa apakah halaman besar dikonfigurasi oleh program berbahaya, atau jika tidak diperlukan, Anda dapat mengomentari item konfigurasi `vm.nr_hugepage` di file `/etc/sysctl.conf`, lalu jalankan `sysctl -p` perintah untuk meninggalkan halaman besar.

## Petunjuk[](id:RelatedOperations)
### Melihat penggunaan memori
Hasil perintah `free` mungkin berbeda dengan distribusi Linux, yang tidak dapat diandalkan untuk menghitung penggunaan memori. Lakukan langkah-langkah berikut untuk melihat penggunaan memori pada halaman **Monitoring** (Pemantauan) dari konsol CVM.
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index) dan akses halaman **Instances* (Instans).
2. Klik **ID/Name** (ID/Nama) instans untuk masuk ke halaman detailnya. Pilih tab **Monitoring** (Pemantauan).
3. Lihat penggunaan memori di bagian **Memory Monitor** (Pemantauan Memori), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/4f9f423e6d9d460d1413ff0ead6c7e96.png)

### Menghitung penggunaan memori
Penggunaan memori adalah rasio memori yang digunakan untuk total memori, tidak termasuk buffer dan cache sistem. Rumus perhitungannya adalah sebagai berikut:
= `(Total - tersedia)100% / Total`
= `(Total - (Bebas + Buffer + Cached + SReclaimable - Shmem)) * 100% / Total`
= `(Total - Bebas - Buffer - Cached - SReclaimable + Shmem）* 100% / Total`

Parameter yang diperlukan `Total`, `Free`, `Buffer`, `Cached`, `SReclaimable`, dan `Shmem` dapat diperoleh di `/proc/meminfo`. Di bawah ini adalah contoh dari `/proc/meminfo`.
```plaintext
1. [root@VM_0_113_centos test]# cat /proc/meminfo 
2. MemTotal: 16265592 kB
3. MemFree: 1880084 kB
4. ......
5. Buffer: 194384 kB
6. Di-cache: 13647556 kB
7. ......
8. Shmem: 7727752 kB
9. Slab: 328864 kB
10. SReclaimable: 306500 kB
11. SUnreclaim: 22364 kB
12. ......
13. HugePages_Total: 0:
14. Hugepagesize: 2048 kB
```
Parameter tersebut dijelaskan sebagai berikut:
<table>
<tr>
<th>Parameter</th>
<th>Deskripsi</th>
</tr>
<tr>
<td><code>MemTotal</code></td>
<td>Total memori sistem</td>
</tr>
<tr>
<td><code>MemFree</code></td>
<td>Memori bebas</td>
</tr>
<tr>
<td><code>Buffer</code></td>
<td>Halaman yang di-cache digunakan oleh perangkat blok untuk membaca/menulis dan metadata sistem file (seperti SuperBlock)</td>
</tr>
<tr>
<td><code>Di-cache</code></td>
<td>Cache halaman, termasuk <code>memori bersama POSIX/SysV</code> dan <code>mmap anonim bersama</code> dari tmpfs
</td>
</tr>
<tr>
<td><code>Shmem</code></td>
<td>Termasuk memori bersama, tmpfs, dll.
</td>
</tr>
<tr>
<td><code>Slab</code></td>
<td>Memori yang dialokasikan oleh pengalokasi memori slab kernel, yang dapat dilihat menggunakan perintah <code>slabtop</code>
</td>
</tr>
<tr>
<td><code>SReclaimable</code></td>
<td>Slab yang dapat diklaim ulang</td>
</tr>
<tr>
<td><code>SUnreclaim</code></td>
<td>Slab yang tidak dapat diklaim ulang</td>
</tr>
<tr>
<td><code>HugePages_Total</code></td>
<td>Jumlah total halaman besar</td>
</tr>
<tr>
<td><code>Hugepagesize</code></td>
<td>Ukuran halaman besar</td>
</tr>
</table>

### Analisis masalah memori[](id:OtherProcessingSteps)
Jika masalah berlanjut, atau kesalahan yang ditunjukkan di bawah ini muncul selama Anda menggunakan CVM, lihat solusi yang sesuai:
- [Kesalahan Log “fork: Cannot allocate memory” (fork: Tidak dapat mengalokasikan memori)](https://intl.cloud.tencent.com/document/product/213/40502)
- [Kesalahan Login VNC “Cannot allocate memory” (Tidak dapat mengalokasikan memori)](https://intl.cloud.tencent.com/document/product/213/40503)
- [Memicu Kehabisan Memori Saat Ada Memori yang Tersedia](https://intl.cloud.tencent.com/document/product/213/40504) 
