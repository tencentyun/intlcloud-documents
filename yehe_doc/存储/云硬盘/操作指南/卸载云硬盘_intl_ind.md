## Skenario

Saat Anda perlu memasang disk cloud elastis yang merupakan **disk data** pada CVM lain, Anda dapat melepas disk cloud elastis ini dari CVM, lalu memasangnya ke CVM lain.**Melepas disk cloud elastis tidak menghapus data pada disk ini.**
Saat ini, pelepasan disk cloud elastis yang merupakan **disk data** didukung.Anda tidak dapat melepas disk sistem atau disk cloud non-elastis.**Untuk melepas disk cloud, Anda harus menjalankan operasi `umount` (Linux) atau offline (Windows).Jika tidak, disk cloud elastis mungkin tidak dikenali oleh CVM saat dipasang lagi**

## Prasyarat

Sebelum melepas disk data, pastikan Anda memahami prasyarat berikut:
- Dalam sistem operasi Windows:
- Untuk mencegah kehilangan data, kami menyarankan Anda untuk menangguhkan operasi baca dan tulis pada semua sistem file disk.Jika tidak, data yang belum dibaca atau ditulis akan hilang.
- Saat melepas disk cloud elastis, Anda harus mengatur disk ke status offline terlebih dahulu.Jika tidak, Anda mungkin tidak dapat memasang kembali disk cloud elastis kecuali Anda memulai ulang CVM.Ini ditunjukkan pada gambar berikut:
- Dalam sistem operasi Linux:
- Anda harus terlebih dahulu [masuk](https://intl.cloud.tencent.com/document/product/213/5436) ke instance, dan melakukan operasi `umount` pada disk cloud elastis yang ingin Anda lepas.Jika Anda secara langsung memaksa melepas tanpa menjalankan operasi `umount`, masalah yang ditunjukkan pada gambar berikut dapat terjadi selama pematian dan bootup:
![](https://mccdn.qcloud.com/static/img/9939fccce6e6d9ead64b5703455d4403/image.png)
![](https://mccdn.qcloud.com/static/img/9939fccce6e6d9ead64b5703455d4403/image.png)
- Jika Anda membuat volume logis LVM pada CVM, melepas disk langsung dari konsol akan menyebabkan sebagian data perangkat tetap berada di memori CVM.Jika aplikasi CVM mencoba melintasi atau mengakses perangkat ini, kesalahan sistem akan terjadi.Akibatnya, Anda harus terlebih dahulu menjalankan operasi berikut (contoh ini mengasumsikan bahwa volume logis /dev/test/lv1 dibuat berdasarkan /dev/vdb1, dan dipasang di bawah direktori /data):
a.Jalankan perintah `umount /data` untuk melepas disk dari titik pemasangan yang sesuai di CVM.
b.Jalankan perintah `lvremove /dev/test/lv1` untuk menghapus LV.Jika ada beberapa LV, hapus semua LV satu per satu.
c.Jalankan perintah `vgremove test` untuk menghapus VG.
d.Jalankan perintah `pvremove /dev/vdb1` untuk menghapus PV.
e.Modifikasi file `/etc/fstab` untuk menghindari pemasangan terus menerus dari LV yang sesuai pada bootup berikutnya.

## Petunjuk

### Menggunakan konsol untuk melepas disk cloud

1.Masuk ke [Konsol CBS](https://console.cloud.tencent.com/cvm/cbs).
2.Anda dapat menggunakan metode berikut untuk melepas disk cloud:
a.Pelepasan tunggal:Di baris disk cloud target dengan status **Mounted** (Dipasang), klik **More**>**Unmount** (Selengkapnya > Lepas).
b.Pelepasan dalam batch:Pilih beberapa disk cloud target dengan status **Mounted** (Dipasang) dan klik **Unmount** (Lepas) di bagian atas daftar.
3.Di kotak pengingat **Unmount Cloud Disk** (Lepas Disk Cloud) yang muncul, konfirmasi peringatan dan klik **Confirm** (Konfirmasi) untuk melepas disk.

### Menggunakan API untuk melepas disk cloud

Anda dapat menggunakan API `DetachDisks` untuk melepas disk cloud.Untuk informasi selengkapnya, lihat [Melepas disk cloud](https://intl.cloud.tencent.com/document/product/362/16316).

