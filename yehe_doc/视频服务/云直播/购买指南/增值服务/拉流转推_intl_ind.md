Fitur relai melakukan pull dan push pada konten. Anda dapat menggunakan relai untuk melakukan pull pada konten video atau streaming langsung yang sudah ada, lalu melakukan push ke URL tujuan tanpa memulai sesi streaming langsung. Fitur ini dikenai tagihan berdasarkan [durasi tugas relai](#time) dan [penggunaan push ke URL pihak ketiga](#third_part).



## Catatan
- Aturan penagihan untuk relai **telah berlaku efektif sejak pukul 00.00 tanggal 1 Juli 2021**. Tugas relai yang dilakukan setelah waktu tersebut akan dikenai biaya tanpa mempertimbangkan waktu pembuatan tugas tersebut.
- Ketika Anda menggunakan relai, pull akan menyebabkan penggunaan lalu lintas/bandwidth pemutaran ulang. Pull dari URL sumber milik CSS, VOD, COS, dll. akan dikenai biaya pemutaran ulang yang sesuai dan biaya pengunduhan.


[](id:time)
## Durasi Tugas Relai

### Harga
Tugas relai dikenai tagihan berdasarkan durasi.

| Item yang Dapat Dikenai Tagihan       | Harga (USD/Menit) |
| ---------------- | ----------------- |
| Durasi tugas relai | 0,00032           |



### Penagihan
- Item yang dapat dikenai tagihan: durasi tugas relai
- Mode penagihan: bayar sesuai pemakaian
- Siklus penagihan: siklus penagihan harian. Total biaya relai selama satu hari akan dipotong pada pukul 10.00 hari berikutnya. Lihat laporan tagihan Anda untuk detailnya.
- Aturan penagihan: durasi tugas relai yang sedang dijalankan akan dikenai tagihan. Durasi tugas yang dijeda atau kedaluwarsa tidak dikenai tagihan dan akan dikenai tagihan setelah tugas dilanjutkan kembali.

>! Jika pulling gagal karena konten sumber tidak normal, tugas relai tidak akan berhenti sampai waktu akhir yang sudah ditetapkan, dan **durasi tugas terkait akan dikenai tagihan**.


[](id:third_part)
## Push ke URL Pihak Ketiga
>! 
>- Untuk tugas relai, push ke URL push CSS dalam akun Tencent Cloud yang membuat tugas tersebut tidak akan dikenai tagihan.
>- Push ke URL selain URL push CSS dari akun Tencent Cloud saat ini akan dikenai biaya untuk push ke URL pihak ketiga. 

### Harga

| Item yang Dapat Dikenai Tagihan      | Harga (USD/Mbps/Bulan) | Deskripsi              |
| :------------- | :------------------- | :------------------------- |
| Push ke URL pihak ketiga | 12,67        | Ditagih berdasarkan penggunaan bandwidth yang sesuai |


### Penagihan
- Mode penagihan: bayar sesuai pemakaian bulanan
- Siklus penagihan: siklus penagihan bulanan. Tagihan Anda untuk bulan tertentu akan muncul antara tanggal 1 dan 3 bulan berikutnya.
- Aturan penagihan: penggunaan bandwidth bersamaan dari semua push ke URL pihak ketiga akan dikenai tagihan. Mode penagihan default adalah tagihan berdasarkan bandwidth puncak harian rata-rata dengan biaya sesuai pemakaian dalam siklus penagihan. Jika mode tagihan berdasarkan bandwidth bulanan lain digunakan untuk layanan LVB dalam akun ini, mode tersebut akan diterapkan untuk push ke URL pihak ketiga.


