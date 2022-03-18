## Deskripsi Kesalahan
Saya tidak dapat masuk ke CVM melalui VNC, dan muncul pesan kesalahan “Tidak dapat mengalokasikan memori”.
![](https://main.qcloudimg.com/raw/0a31fdd909701c27c9923b2fff24668a.png)

## Kemungkinan Alasan[](id:PossibleCauses)
Masalah ini mungkin disebabkan oleh terlalu banyak halaman besar. Ukuran halaman besar default adalah 2048 KB. Jumlah halaman besar dinyatakan dalam `/etc/sysctl.conf`. Jika ada 1280 halaman besar (seperti yang ditunjukkan di bawah), memori 2,5 GB diperlukan. Jika spesifikasi instans rendah, mungkin tidak ada cukup memori untuk menjalankan sistem dengan benar, dan Anda tidak dapat memasuki sistem setelah memulai ulang.
![](https://main.qcloudimg.com/raw/1978a0b2a85fc828674f720c108c48a3.png)


## Solusi
1. Lakukan [prosedur pemecahan masalah](#ProcessingSteps) untuk memeriksa apakah jumlah total utas melebihi batas. 
2. Ubah konfigurasi halaman besar sesuai kebutuhan.


## Prosedur Pemecahan Masalah[](id:ProcessingSteps)
1. Periksa apakah jumlah total utas melebihi batas seperti yang diinstruksikan di [Kesalahan Log “fork: Cannot allocate memory” (fork: Tidak dapat mengalokasikan memori)](https://intl.cloud.tencent.com/document/product/213/40502). Jika tidak, lanjutkan ke langkah berikutnya.
2. Masuk ke mode pengguna tunggal dan login ke CVM. Untuk petunjuk terperinci, lihat [Melakukan booting ke Mode Pengguna Tunggal Linux](https://intl.cloud.tencent.com/document/product/213/34819).
3. Jalankan perintah berikut untuk memeriksa konfigurasi halaman besar.
```
cat /etc/sysctl.conf | grep hugepages
```
Jika ada banyak halaman besar, lakukan langkah-langkah berikut untuk mengubah konfigurasi.
4. Jalankan perintah berikut untuk membuka file konfigurasi `/etc/sysctl.conf` dengan editor VIM.
```
vim /etc/sysctl.conf
```
5. Tekan **i** (i) untuk masuk ke mode edit dan kurangi nilai `vm.nr_hugepages` sesuai kebutuhan.
6. Tekan **Esc**, masukkan **:wq**, dan tekan **Enter** untuk menyimpan konfigurasi dan keluar dari editor VIM.
7. Jalankan perintah berikut agar konfigurasi segera berlaku.
```
sysctl -p
```
8. Lalu mulai ulang CVM, dan Anda dapat login secara normal.
