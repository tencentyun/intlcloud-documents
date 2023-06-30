
Performa disk cloud tergantung pada kapasitasnya. Anda dapat meningkatkan performanya dengan menyesuaikan kapasitasnya hingga mencapai batas. Saat batas tercapai, Anda dapat membeli performa ekstra untuk mendapatkan performa yang lebih tinggi. Perhatikan bahwa performa ekstra hanya tersedia untuk instans SSD yang ditingkatkan. Untuk informasi selengkapnya, lihat [Performa SSD yang Ditingkatkan](https://intl.cloud.tencent.com/document/product/362/39611).
>!
>- Saat ini, hanya **Enhanced SSD** (SSD yang Ditingkatkan) yang mendukung penyesuaian performa independen.
>- [Performa ekstra](https://intl.cloud.tencent.com/document/product/362/39611#.E5.A2.9E.E5.BC.BA.E5.9E.8B-ssd-.E4.BA.91.E7.A1.AC.E7.9B.98.E9.A2.9D.E5.A4.96.E6.80.A7.E8.83.BD) dapat disesuaikan secara independen hanya setelah [performa dasar](https://intl.cloud.tencent.com/document/product/362/39611#.E5.A2.9E.E5.BC.BA.E5.9E.8B-ssd-.E4.BA.91.E7.A1.AC.E7.9B.98.E5.9F.BA.E5.87.86.E6.80.A7.E8.83.BD) mencapai batas maksimal.
>- Penyesuaian performa tidak akan memengaruhi pengoperasian disk cloud dan bisnis Anda.



## Penagihan Penyesuaian Performa

### Peningkatan

- Untuk disk cloud bayar sesuai pemakaian, peningkatan performa akan segera berlaku, dan disk cloud langsung diisi oleh konfigurasi baru.

### Penurunan


- Untuk disk cloud bayar sesuai pemakaian, peningkatan performa akan segera berlaku, dan disk cloud langsung diisi oleh konfigurasi baru.

## Peningkatan Performa

#### Meningkatkan disk melalui konsol
Ketika prasyarat terpenuhi, Anda dapat meningkatkan disk seperti yang diinstruksikan di bawah ini di konsol: 

1. Login ke [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).
2. Pilih wilayah dan disk cloud yang memerlukan penyesuaian performa.
3. Klik **More** (Lainnya) > **Adjust Performance** (Sesuaikan Performa) di bawah kolom **Operation** (Operasi) dari disk cloud yang dipilih.
4. Pilih konfigurasi target di jendela pop-up.
5. Baca dan konfirmasi catatan, lalu mulai penyesuaian.

#### Meningkatkan disk melalui API
Anda juga dapat menggunakan `ModifyDiskExtraPerformance` API untuk meningkatkan disk cloud tertentu. Untuk petunjuk mendetail, lihat [ModifyDiskExtraPerformance](https://intl.cloud.tencent.com/document/product/362/40191).


## Penurunan Performa

#### Menurunkan disk melalui konsol
Ketika prasyarat terpenuhi, Anda dapat menurunkan versi disk seperti yang diinstruksikan di bawah ini di konsol:

1. Login ke [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).
2. Pilih wilayah dan disk cloud yang memerlukan penyesuaian performa.
3. Klik **More** (Lainnya) > **Adjust Performance** (Sesuaikan Performa) di bawah kolom **Operation** (Operasi) dari disk cloud yang dipilih.
4. Pilih konfigurasi target di jendela pop-up.
5. Baca dan konfirmasi catatan, lalu mulai penyesuaian.

#### Menurunkan disk melalui API
Anda juga dapat menggunakan `ModifyDiskExtraPerformance` API untuk menurunkan disk cloud tertentu. Untuk petunjuk mendetail, lihat [ModifyDiskExtraPerformance](https://intl.cloud.tencent.com/document/product/362/40191).

