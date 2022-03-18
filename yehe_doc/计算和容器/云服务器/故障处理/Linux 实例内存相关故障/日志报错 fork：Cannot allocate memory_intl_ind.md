## Deskripsi Kesalahan
Log berisi pesan kesalahan “fork: Cannot allocate memory” (fork: Tidak dapat mengalokasikan memori).
![](https://main.qcloudimg.com/raw/db85a43e7495f1655a2b59063ffc33e3.png)

## Kemungkinan Alasan
Masalah ini mungkin disebabkan oleh utas yang berlebihan. Jika utas baru dibuat setelah nilai `pid_max` tercapai, pesan kesalahan “fork: Cannot allocate memory” (fork: Tidak dapat mengalokasikan memori) muncul.

## Solusi
1. Lakukan [prosedur pemecahan masalah](#ProcessingSteps) untuk memeriksa penggunaan memori.
2. Periksa jumlah utas dan ubah konfigurasi `pid_max`. 



## Prosedur Pemecahan Masalah[](id:ProcessingSteps)
1. Periksa penggunaan memori seperti yang diinstruksikan di [Penggunaan Memori Tinggi](https://intl.cloud.tencent.com/document/product/213/40501). Jika penggunaan memori normal, lanjutkan ke langkah berikutnya.
2. Jalankan perintah berikut untuk mendapatkan nilai `pid_max`.
```
sysctl -a | grep pid_max
```
Nilai default `pid_max` adalah `32768`, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/816a0bd183244aadf14e04c6ed200d68.png)
3. Jalankan perintah berikut untuk melihat jumlah total utas.
```
pstree -p | wc -l
```
Ketika jumlah total utas telah mencapai `pid_max`, utas baru akan menyebabkan kesalahan “fork: Cannot allocate memory” (fork: Tidak dapat mengalokasikan memori).
>?Anda dapat menggunakan perintah `ps -efL` untuk menemukan program yang menjalankan banyak utas.
>
4. Ubah nilai `kernel.pid_max` dalam file konfigurasi `/etc/sysctl.conf` menjadi `65535` untuk menambah jumlah utas. Hasilnya harus sebagai berikut:
![](https://main.qcloudimg.com/raw/a4bbf49b3236b9f50988e914298adb31.png)
5. Jalankan perintah berikut agar konfigurasi segera berlaku.
```
sysctl -p
```
