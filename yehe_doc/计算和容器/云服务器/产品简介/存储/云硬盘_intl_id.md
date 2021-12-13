Tencent Cloud Block Storage (CBS) menyediakan layanan penyimpanan blok persisten untuk instans CVM.

- CBS secara otomatis menyimpan data dalam beberapa salinan redundan di zona ketersediaan untuk menghilangkan risiko titik tunggal kegagalan data, yang menyediakan keandalan data hingga 99,9999999%.
- CBS menawarkan disk cloud dari berbagai jenis dan spesifikasi untuk mencapai performa penyimpanan yang stabil dan latensi rendah.
- Disk cloud dapat dipasang dan dilepaskan dari instans CVM di zona ketersediaan yang sama. Hanya perlu beberapa menit untuk menyesuaikan kapasitas disk. 


## Kasus Penggunaan Standar
- Saat CVM kehabisan ruang disk, Anda dapat membeli satu atau beberapa disk cloud dan memasangnya ke CVM.
- Anda tidak perlu membeli kapasitas penyimpanan tambahan saat membeli CVM. Anda dapat membeli disk cloud nanti jika diperlukan.
- Saat Anda perlu mentransfer data dari satu CVM ke CVM lainnya, cukup lepaskan disk data cloud dari CVM sumber dan pasang ke CVM target.
- Gunakan beberapa disk cloud untuk membentuk Logical Volume Manager (LVM) guna melampaui batas fisik satu disk cloud.
- Gunakan beberapa disk cloud untuk membentuk konfigurasi Redundant Array of Independent Disks (RAID) guna melampaui batas performa I/O dari satu disk cloud.


## Siklus pemakaian
- Siklus proses **non-elastic cloud disk** (disk cloud non-elastis) sama dengan CVM. Disk tersebut dibeli dengan CVM dan digunakan sebagai disk sistem. Disk tersebut tidak dapat dipasang atau dilepaskan dari CVM.
- Siklus proses **elastic cloud disk** (disk cloud elastis) tidak bergantung pada instans CVM. Anda dapat melampirkan beberapa disk cloud ke instans CVM sebagai disk data, melepaskannya, lalu memasangnya kembali ke instans lain.

## Jenis
Empat jenis disk cloud disediakan, termasuk **Premium Cloud Storage**, **SSD**, **Enhanced SSD**, and **Tremendous SSD**. Setiap jenis memiliki performa dan karakteristik yang unik, serta harganya berbeda-beda. Anda dapat memilih jenis disk cloud yang paling sesuai dengan persyaratan aplikasi Anda. Untuk informasi selengkapnya, lihat [Jenis Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31636) dan [Ikhtisar Harga](https://intl.cloud.tencent.com/document/product/362/2413).

## Operasi yang Relevan
- Untuk informasi tentang instans CVM dan konfigurasi disk cloud, lihat [Membuat Disk Cloud](https://intl.cloud.tencent.com/document/product/362/5744) dan [Memasang Disk Cloud](https://intl.cloud.tencent.com/document/product/362/32401).
- Untuk informasi tentang praktik terbaik untuk perluasan kapasitas, pelepasan, penghentian, dan operasi lainnya, lihat [dokumentasi CBS](https://intl.cloud.tencent.com/document/product/362).



