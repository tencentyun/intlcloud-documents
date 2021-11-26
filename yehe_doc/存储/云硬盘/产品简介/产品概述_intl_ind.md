## Apa itu Cloud Block Storage Tencent?
Cloud Block Storage (CBS) adalah perangkat penyimpanan blok dengan ketersediaan tinggi, sangat andal, hemat biaya, dan dapat disesuaikan.Perangkat ini dapat digunakan sebagai disk terpisah dan dapat diperluas untuk CVM, yang menyediakan perangkat [penyimpanan](https://intl.cloud.tencent.com/document/product/213/4952) yang efisien dan andal.CBS menyediakan penyimpanan jangka panjang di tingkat blok data.Ini biasanya digunakan sebagai perangkat penyimpanan utama untuk data yang membutuhkan pembaruan yang sering dan mendetail (seperti sistem file dan basis data), yang menampilkan ketersediaan, keandalan, dan kinerja yang tinggi.CBS menggunakan mekanisme terdistribusi tiga salinan untuk mencadangkan data Anda pada komputer fisik yang berbeda untuk menghindari kehilangan data yang disebabkan oleh satu titik kegagalan, meningkatkan keandalan data.
Anda dapat dengan mudah membeli, menyesuaikan, dan mengelola perangkat disk cloud Anda melalui konsol, dan membangun sistem file untuk menciptakan ruang penyimpanan yang lebih besar dari ruang penyimpanan satu disk cloud.Disk cloud dapat diklasifikasikan menurut siklus hidup yang berbeda sebagai berikut:
- Siklus hidup disk cloud non-elastis yang sepenuhnya mengikuti siklus hidup CVM.Disk tersebut dibeli dengan CVM dan digunakan sebagai disk sistem.Jenis disk ini tidak mendukung pemasangan dan pelepasan.
- Siklus hidup disk cloud elastis yang terpisah dari siklus hidup CVM.Jenis disk ini dapat dibeli secara terpisah dan dipasang secara manual ke CVM.Jenis disk ini juga dapat dibeli dengan CVM dan secara otomatis dipasang ke CVM sebagai disk data.Disk cloud elastis mendukung pemasangan dan pelepasan dari CVM di zona ketersediaan yang sama kapan saja.Anda dapat memasang beberapa disk cloud elastis ke CVM yang sama, atau melepas disk cloud dari CVM A lalu memasangnya ke CVM B.

Tencent Cloud memberikan batasan kuota pada disk cloud pengguna.Untuk informasi selengkapnya, lihat [Batas Penggunaan](https://intl.cloud.tencent.com/document/product/362/32406).

## Kasus Penggunaan Standar
- Anda dapat membeli dan memasang satu atau beberapa disk cloud untuk memenuhi persyaratan kapasitas penyimpanan saat ruang disk pada CVM Anda tidak mencukupi.
- Saat membeli CVM, Anda tidak memerlukan ruang penyimpanan tambahan.Jika Anda memiliki persyaratan penyimpanan, Anda dapat memperluas kapasitas penyimpanan CVM dengan membeli disk cloud.
- Saat ada permintaan pertukaran data antara beberapa CVM, Anda dapat melepas disk cloud (disk data) dan memasangnya kembali ke CVM lain.
- Anda dapat memperluas kapasitas penyimpanan maksimum dari satu disk cloud dengan membeli beberapa disk cloud dan mengonfigurasi Logical Volume Manager (LVM).
- Anda dapat memperluas kapasitas I/O maksimum dari satu disk cloud dengan membeli beberapa disk cloud dan mengonfigurasi kebijakan Redundant Array of Independent Disks (RAID).

## Fitur
Tencent Cloud menyediakan berbagai perangkat penyimpanan jangka panjang, memungkinkan pengguna untuk memilih jenis disk cloud yang sesuai untuk menyimpan file, membangun basis data, dll.
- Tencent Cloud CBS hadir dengan empat jenis disk:Premium Cloud Storage, SSD, Enhanced SSD, dan Tremendous SSD.
- Pemasangan dan pelepasan elastis: semua jenis disk cloud elastis mendukung pemasangan dan pelepasan elastis.Anda dapat memasang beberapa disk cloud pada CVM untuk membangun sistem file dengan kapasitas tinggi.
- Perluasan elastis: satu disk mendukung kapasitas maksimum 32 TB.Anda dapat meningkatkan penskalaan disk kapan saja.
- Pencadangan snapshot: Anda dapat membuat dan mengembalikan snapshot untuk mencadangkan data.Anda juga dapat membuat disk cloud dari snapshot untuk mempercepat deployment bisnis Anda.
