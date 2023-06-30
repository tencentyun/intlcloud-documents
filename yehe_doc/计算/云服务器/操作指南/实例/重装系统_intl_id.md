## Ikhtisar

Penginstalan ulang sistem adalah metode penting untuk mengembalikan instans ke status awal jika terjadi kegagalan sistem.

CVM mendukung dua jenis penginstalan ulang berikut:
 - **Single-system reinstallation** (Penginstalan ulang sistem tunggal): CVM di semua wilayah dapat diinstal ulang ke sistem operasi yang sama.
 Misalnya, Linux diinstal ulang sebagai Linux dan Windows diinstal ulang sebagai Windows. 
 - **Cross-system reinstallation** (Penginstalan ulang lintas sistem): hanya CVM di daratan China (tidak termasuk Hong Kong, China) yang dapat diinstal ulang ke sistem operasi yang berbeda.
 Misalnya, Linux diinstal ulang sebagai Windows dan Windows diinstal ulang sebagai Linux.
>? 
> - Saat ini, semua instans CBS baru dan disk lokal mendukung penginstalan ulang lintas sistem. Namun, beberapa disk lokal 20 GB yang ada tidak mendukung penginstalan ulang lintas sistem melalui Konsol. Jika Anda perlu menerapkan penginstalan ulang lintas sistem untuk instans pada disk lokal ini, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category/create?level1_id=6&level2_id=7&level1_name=%E8%AE%A1%E7%AE%97%E4%B8%8E%E7%BD%91%E7%BB%9C&level2_name=%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%20CVM) untuk mengajukan fitur penginstalan lintas sistem.
> - Instans spot tidak mendukung penginstalan ulang sistem.

## Catatan
 - **Preparing for reinstallation:** (Mempersiapkan penginstalan ulang:) cadangkan data penting ke disk sistem Anda sebelum penginstalan ulang karena data disk sistem akan hilang setelah penginstalan ulang. Untuk menyimpan data sistem Anda, sebaiknya [buat citra kustom](https://intl.cloud.tencent.com/document/product/213/4942) dan gunakan citra ini untuk menginstal ulang sistem.
 - **Image selection:** (Pemilihan citra:) sebaiknya gunakan citra yang disediakan oleh Tencent Cloud atau citra kustom Anda, bukan citra dari sumber yang tidak dikenal atau sumber lain. Jangan lakukan operasi lain saat disk sistem sedang diinstal ulang.
 - **Instance physical features:** (Fitur fisik instans:) IP publik instans tidak akan berubah.
 - **Billing:** (Penagihan:) saat menyesuaikan ukuran disk sistem (hanya untuk CBS), Anda akan dikenakan biaya sesuai dengan standar harga CBS. Untuk informasi selengkapnya, lihat [Daftar Harga](https://intl.cloud.tencent.com/document/product/213/2255).
 - **Subsequent operations:** (Operasi selanjutnya:) setelah disk sistem diinstal ulang, data dalam disk data tidak akan terpengaruh dan hanya akan tersedia untuk digunakan setelah disk data dipasang kembali.

## Petunjuk

Anda dapat menggunakan salah satu metode berikut untuk menginstal ulang sistem operasi:
- [Instal ulang sistem melalui Konsol](#consoleRestart)
- [Instal ulang sistem melalui API](#apiRestart)

<span id="consoleRestart"></span>
### Menginstal ulang sistem melalui Konsol

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/).
2. Di baris instans yang sistemnya yang ingin Anda instal ulang, klik **More** (Lainnya) > **Reinstall the system** (Instal ulang sistem), seperti yang ditunjukkan pada gambar berikut:
![Instal ulang sistem](https://main.qcloudimg.com/raw/cf9c32f589a0243d84d6db0b92ccad2e.png)
3. Di jendela pop-up yang muncul, klik **OK, reinstall now** (OKE, instal ulang sekarang).
4. Pilih citra yang digunakan oleh instans saat ini atau citra lain, atur ukuran disk, atur kata sandi login untuk instans, lalu klik **Start reinstall** (Mulai instal ulang).
![](https://main.qcloudimg.com/raw/868508ad1ab1e1e2a60ea98d5d936a92.png)

<span id="apiRestart"></span>
### Menginstal ulang sistem melalui API

Untuk informasi selengkapnya, lihat [ResetInstance](https://intl.cloud.tencent.com/document/product/213/33242) API.

## Operasi Selanjutnya
Jika CVM Anda telah memasang disk data sebelum penginstalan ulang lintas sistem, lihat dokumen berikut tentang cara membaca data dari disk data sistem operasi asli:
- [Membaca/Menulis Disk Data EXT setelah Menginstal Ulang CVM Linux ke CVM Windows](https://intl.cloud.tencent.com/document/product/213/3856)
- [Membaca/Menulis Disk Data NTFS setelah Menginstal Ulang CVM Windows ke CVM Linux](https://intl.cloud.tencent.com/document/product/213/3857)
