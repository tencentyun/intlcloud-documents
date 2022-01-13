>?Instance berlangganan bulanan tidak bisa dihapus, tetapi Anda bisa berhenti memperbaruinya saat kedaluwarsa.

Setelah Anda mengonfirmasi bahwa instance CLB tidak memiliki lalu lintas dan tidak lagi dibutuhkan, Anda bisa menghapusnya melalui konsol CLB atau API.
Setelah dihapus, instance CLB akan benar-benar dihentikan dan tidak bisa dipulihkan.Kami sangat menyarankan untuk memutus semua server asli dan mengamati untuk sementara sebelum menghapus instance apa pun.

## Menghapus instance CLB melalui konsol
1.Masuk ke [Konsol CLB](https://console.cloud.tencent.com/loadbalance).
2.Carilah instance CLB yang ingin Anda hapus dan klik **More** -> **Delete** (Lainnya - > Hapus) pada kolom **Operation** (Operasi) di sebelah kanan.
![](https://main.qcloudimg.com/raw/693acd714a4335920aea91b3ec4888f9.png)
3.Kotak dialog konfirmasi akan muncul.Setelah Anda membaca prompt keamanan operasi. klik **Submit** (Kirim) untuk mengonfirmasi penghapusan.
Kotak dialog seperti yang ditunjukkan di bawah ini.Kami menyarankan untuk mengonfirmasi penghapusan saat terdapat **0** aturan pengikatan, **none** (tidak ada) instance terikat CVM, dan tanda hijau di bawah kolom **Notes About Operation Security** (Catatan Mengenai Keamanan Operasi).                              ![](https://main.qcloudimg.com/raw/e3f3e2f08b4b9c4f61c478762de4b33a.png)

## Menghapus instance CLB melalui API
Untuk informasi selengkapnya, buka [DeleteLoadBalancers](https://intl.cloud.tencent.com/document/api/214/1257).
