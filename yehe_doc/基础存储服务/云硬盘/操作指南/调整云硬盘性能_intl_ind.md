
Kinerja disk cloud tergantung pada kapasitasnya.Anda dapat meningkatkan kinerjanya dengan menyesuaikan kapasitasnya hingga mencapai batas maksimum.Saat batas maksimum tercapai, Anda dapat membeli kinerja ekstra untuk mendapatkan kinerja yang lebih tinggi lagi.Perhatikan bahwa kinerja ekstra hanya tersedia untuk instance Enhanced SSD.Untuk informasi selengkapnya, lihat [Kinerja Enhanced SSD](https://intl.cloud.tencent.com/document/product/362/39611).
>!
>- Saat ini, hanya **Enhanced SSD** yang mendukung penyesuaian kinerja secara terpisah.
>- [Kinerja ekstra](https://intl.cloud.tencent.com/document/product/362/39611#.E5.A2.9E.E5.BC.BA.E5.9E.8B-ssd-.E4.BA.91.E7.A1.AC.E7.9B.98.E9.A2.9D.E5.A4.96.E6.80.A7.E8.83.BD) dapat disesuaikan secara terpisah hanya setelah [kinerja dasar](https://intl.cloud.tencent.com/document/product/362/39611#.E5.A2.9E.E5.BC.BA.E5.9E.8B-ssd-.E4.BA.91.E7.A1.AC.E7.9B.98.E5.9F.BA.E5.87.86.E6.80.A7.E8.83.BD) mencapai batas maksimum.
>- Penyesuaian kinerja tidak akan memengaruhi jalannya disk cloud dan bisnis Anda.



## Penagihan Penyesuaian Kinerja

### Meningkatkan kinerja

- Untuk disk cloud yang dibayar sesuai pemakaian, peningkatan kinerja akan segera berlaku, dan disk cloud langsung dikenakan biaya atas konfigurasi baru.

### Menurunkan kinerja


- Untuk disk cloud yang dibayar sesuai pemakaian, peningkatan kinerja akan segera berlaku, dan disk cloud langsung dikenakan biaya atas konfigurasi baru.

## Peningkatan Kinerja

#### Meningkatkan kinerja disk melalui konsol
Ketika prasyarat terpenuhi, Anda dapat meningkatkan kinerja disk seperti yang diinstruksikan di bawah ini di konsol:

1.Masuk ke [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).
2.Pilih wilayah dan disk cloud yang memerlukan penyesuaian kinerja.
3.Klik **More** > **Adjust Performance** (Selengkapnya > Sesuaikan Kinerja) di bawah kolom **Operation** (Operasi) dari disk cloud yang dipilih.
4.Pilih konfigurasi target di jendela pop-up.
5.Baca dan konfirmasikan catatan dan mulai penyesuaian.

#### Meningkatkan kinerja disk melalui API
Anda juga dapat menggunakan API `ModifyDiskExtraPerformance` untuk meningkatkan kinerja disk cloud tertentu.Untuk membaca petunjuk mendetail, lihat [ModifyDiskExtraPerformance](https://intl.cloud.tencent.com/document/product/362/40191).


## Penurunan Kinerja

#### Menurunkan kinerja disk melalui konsol
Ketika prasyarat terpenuhi, Anda dapat menurunkan kinerja disk seperti yang diinstruksikan di bawah ini di konsol:

1.Masuk ke [konsol CBS](https://console.cloud.tencent.com/cvm/cbs).
2.Pilih wilayah dan disk cloud yang memerlukan penyesuaian kinerja.
3.Klik **More** > **Adjust Performance** (Selengkapnya > Sesuaikan Kinerja) di bawah kolom **Operation** (Operasi) dari disk cloud yang dipilih.
4.Pilih konfigurasi target di jendela pop-up.
5.Baca dan konfirmasikan catatan dan mulai penyesuaian.

#### Menurunkan kinerja disk melalui API
Anda juga dapat menggunakan API `ModifyDiskExtraPerformance` untuk menurunkan kinerja disk cloud tertentu.Untuk membaca petunjuk mendetail, lihat [ModifyDiskExtraPerformance](https://intl.cloud.tencent.com/document/product/362/40191).

