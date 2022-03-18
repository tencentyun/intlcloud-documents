## Deskripsi Kesalahan
CVM Linux tidak kehabisan memori dan memicu OOM (Kehabisan Memori/Out of Memory) seperti gambar di bawah ini:
![](https://main.qcloudimg.com/raw/72cbd63ac445a1caa8d82fa1e55ba5a5.png)

## Kemungkinan Alasan
Masalah ini mungkin disebabkan oleh konfigurasi `min_free_kbytes`. Konfigurasi ini menentukan memori diam minimum dari sistem Linux (dalam kilobyte). Ketika memori sistem yang tersedia berada di bawah nilai yang ditetapkan `min_free_kbytes`, sistem akan memanggil oom-killer atau memulai ulang secara paksa bergantung pada parameter kernel `vm.panic_on_oom`:
 - Jika `vm.panic_on_oom=0` ditetapkan, sistem akan meminta OOM dan memanggil oom-killer untuk menghentikan proses yang menggunakan sebagian besar memori.
 - Jika `vm.panic_on_oom =1` ditetapkan, sistem akan memulai ulang secara otomatis.

## Solusi
1. Lakukan [prosedur pemecahan masalah] untuk memeriksa penggunaan memori dan jumlah total utas.
2. Perbaiki konfigurasi `min_free_kbytes`.


## Prosedur Pemecahan Masalah[](id:ProcessingSteps)
1. Periksa penggunaan memori seperti yang diinstruksikan di [Penggunaan Memori Tinggi](https://intl.cloud.tencent.com/document/product/213/40501). Jika penggunaan memori normal, lanjutkan ke langkah berikutnya.
2. Periksa apakah jumlah utas melebihi batas seperti yang diinstruksikan di [Kesalahan Log “fork: Cannot allocate memory” (fork: Tidak dapat mengalokasikan memori)](https://intl.cloud.tencent.com/document/product/213/40502). Jika jumlah utas masih dalam batas, lanjutkan ke langkah berikutnya.
3. Login ke CVM dan jalankan perintah berikut untuk melihat konfigurasi `min_free_kbytes`.
```
sysctl -a | grep min_free
```
Nilai `min_free_kbytes` dalam kbyte. Misalnya, `min_free_kbytes = 1024000` yang ditunjukkan di bawah ini adalah 1 GB.
![](https://main.qcloudimg.com/raw/18ac6c04962abfbf67132eab1a604167.png)
4. Jalankan perintah berikut untuk membuka file konfigurasi `/etc/sysctl.conf` dengan editor VIM.
```
vim /etc/sysctl.conf
```
5. Tekan **i** (i) untuk masuk ke mode edit dan ubah item konfigurasi `vm.min_free_kbytes`.
>? Sebaiknya ubah nilai `vm.min_free_kbytes` menjadi tidak lebih dari 1% dari total memori.
>
6. Tekan **Esc**, masukkan **:wq**, dan tekan **Enter** untuk menyimpan konfigurasi dan keluar dari editor VIM.
7. Jalankan perintah berikut agar konfigurasi berlaku.
```
sysctl -p
```
