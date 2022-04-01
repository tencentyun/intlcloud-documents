## Ikhtisar

Setelah [memperluas disk cloud](https://intl.cloud.tencent.com/document/product/362/5747) di konsol, Anda perlu menetapkan kapasitas yang diperluas ke partisi yang ada, atau memformatnya menjadi partisi baru yang terpisah.
- Jika Anda memperluas disk cloud yang terlampir ke CVM yang sedang berjalan, Anda perlu [memindai ulang disk](#Scaning) untuk mengenali kapasitas disk setelah perluasan.
- Jika disk cloud yang akan diperluas tidak terlampir ke CVM atau CVM yang terlampir dimatikan, kapasitas disk setelah perluasan akan dikenali secara otomatis.

>!
>- Memperluas sistem file dapat memengaruhi data yang ada.Kami sangat menyarankan Anda untuk secara manual [membuat snapshot](https://intl.cloud.tencent.com/document/product/362/5755) untuk mencadangkan data Anda sebelum melakukan operasi tersebut.
>- Untuk memperluas sistem file, Anda perlu [memulai ulang instance](https://intl.cloud.tencent.com/document/product/213/4928) atau memindai ulang disk, yang akan menyebabkan gangguan bisnis untuk periode tertentu.Kami menyarankan Anda memilih waktu yang tepat untuk operasi ini.
>- Setelah perluasan sistem file, kami sangat menyarankan Anda untuk [memindai ulang disk](#Scaning) untuk mengenali kapasitasnya.Jika Anda **menyegarkan** sistem atau melakukan operasi lain, kapasitas yang diperluas mungkin tidak dikenali.
>


## Prasyarat
- Anda telah [memperluas disk cloud melalui konsol](https://intl.cloud.tencent.com/document/product/362/5747).
- Anda telah [melampirkan disk cloud](https://intl.cloud.tencent.com/document/product/362/32401) ke CVM Windows melalui konsol dan membuat sistem file.
- Anda telah masuk ke instance Windows CVM dan Anda ingin memperluas partisi dan sistem file.Lihat [Masuk ke Instance Windows Menggunakan RDP (Direkomendasikan)](https://intl.cloud.tencent.com/document/product/213/5435).
>?Dokumen ini menjelaskan cara memperluas disk yang terlampir ke CVM dengan Windows Server 2012 R2 yang terinstal.Perhatikan bahwa langkah-langkahnya dapat berbeda sesuai dengan versi sistem operasi.
>

## Petunjuk
>!
>- Jika Anda [memperluas disk cloud](https://intl.cloud.tencent.com/document/product/362/5747) yang terlampir ke CVM yang sedang berjalan, Anda harus [memindai ulang disk](#Scaning) untuk mengenali kapasitas sebelum [memperluas sistem file dari partisi yang ada atau membuat partisi](#Extending).
>- Jika disk cloud yang akan diperluas tidak terlampir ke CVM atau CVM yang terlampir dimatikan, Anda dapat langsung melanjutkan dengan [memperluas sistem file dari partisi yang ada atau membuat partisi](#Expanding).
>- Jika driver Virtio dari CVM lebih lama dari versi 58003, silakan [mulai ulang instance](https://intl.cloud.tencent.com/document/product/213/4928) sebelum melakukan operasi.Anda dapat terlebih dahulu [memeriksa versi driver Virtio](#VirtioVersion).


### Memindai ulang disk[](id:Scaning)
1.Klik kanan <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px">, dan pilih **Computer Management** (Manajemen Komputer).
2.Di bilah sisi kiri jendela **Computer Management** (Manajemen Komputer), pilih **Storage** > **Disk Management** (Penyimpanan > Manajemen Disk).
3.Klik kanan **Disk Management** (Manajemen Disk), dan pilih **Rescan Disks** (Pindai Ulang Disk).

4.Setelah pemindaian selesai, periksa apakah disk data memiliki ukuran setelah perluasan.(Dalam contoh ini, pemindaian menunjukkan bahwa disk cloud diperluas dari 10 GB menjadi 50 GB).



### Memperluas sistem file dari partisi yang ada atau membuat partisi[](id:Extending)
Anda dapat memperluas sistem file dari partisi yang ada atau membuat partisi seperti yang diinstruksikan di bawah ini:
<dx-tabs>
::: Memperluas sistem file dari partisi yang ada
1.Klik kanan di mana saja pada ruang kosong disk, dan pilih **Extend Volume** (Perluas Volume).

2.Ikuti **Extend Volume Wizard** (Wizard Perluas Volume) untuk memperluas volume.
Kapasitas disk data baru akan ditambahkan ke volume asli.
:::
::: Membuat partisi
1.Klik kanan ruang disk yang tidak terisi, dan pilih **New Simple Volume** (Volume Sederhana Baru).

2.Ikuti **New Simple Volume Wizard** (Wizard Volume Sederhana Baru) untuk membuat volume sederhana dengan pengaturan default.
Kapasitas disk data baru akan diformat menjadi partisi baru.
:::
</dx-tabs>


## Operasi yang Relevan
### Memeriksa versi driver Virtio[](id:VirtioVersion)
1.Klik kanan <img src="https://main.qcloudimg.com/raw/87d894e564b7e837d9f478298cf2e292.png" style="margin:-3px 0px">, dan pilih **Device Manager** (Pengelola Perangkat).
2.Buka item **Storage Controller** (Pengontrol Penyimpanan) dan klik dua kali **Tencent VirtIO SCSI controller** (Pengontrol Tencent VirtIO SCSI).
3.Pilih tab **Driver** untuk memeriksa versi saat ini.Versi 58005 digunakan, seperti yang ditunjukkan di bawah ini.



## Referensi
- [Memperluas Kapasitas Disk Cloud](https://intl.cloud.tencent.com/document/product/362/5747)
- [Memperluas Partisi dan Sistem File (Linux)](https://intl.cloud.tencent.com/document/product/362/31602)


