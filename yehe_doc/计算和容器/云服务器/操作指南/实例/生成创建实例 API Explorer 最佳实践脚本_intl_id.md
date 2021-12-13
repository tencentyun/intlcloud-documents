## Ikhtisar
Saat membeli CVM di halaman pembelian CVM, Anda dapat membuat skrip praktik terbaik OpenAPI yang dapat digunakan kembali dengan konfigurasi yang dipilih. Anda kemudian dapat menggunakan kode ini untuk membeli instans CVM dengan konfigurasi yang sama.

## Prasyarat
- Anda telah login ke konsol Tencent Cloud dan mengakses halaman CVM [**Custom Configuration** (Konfigurasi Kustom)](https://buy.cloud.tencent.com/cvm?tab=custom).
- Anda telah menyelesaikan konfigurasi CVM dan masuk ke halaman **Confirm Configuration** (Konfigurasi Kustom). Untuk mempelajari tentang cara mengonfigurasi parameter, lihat [Membuat Instans melalui Halaman Pembelian CVM](https://intl.cloud.tencent.com/document/product/213/4855).

## Petunjuk
1. Pada halaman **Confirm Configuration** (Konfirmasi Konfigurasi), klik **Generate API Explorer Reusable Scripts** (Buat Skrip API Explorer yang Dapat Digunakan Kembali) seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/7c095b6809c8815b15d4fe2c45b89305.png)
2. Anda dapat melihat informasi berikut di jendela pop-up.
![](https://main.qcloudimg.com/raw/5fba656be4ee0977245a7778f6a4c910.png)
 - **API Workflow** (Alur Kerja API): memberikan deskripsi dan parameter aktual dari `RunInstances` API berdasarkan konfigurasi yang dipilih. Parameter yang ditandai dengan "*" diperlukan untuk API. Anda dapat mengarahkan kursor ke data untuk menampilkannya sepenuhnya.
 - **API Script** (Skrip API): menghasilkan kode dalam bahasa pemrograman Java dan Python. Pilih tab Java atau Python sesuai kebutuhan, klik **Copy Script** (Salin Skrip) di sudut kanan atas, dan simpan kode untuk membeli instans CVM yang berisi konfigurasi yang sama.
>?
>- Kata sandi instans tidak akan ditampilkan pada halaman atau kode skrip untuk alasan keamanan. Harap modifikasinya dengan sendiri. 
>- Tanggal kedaluwarsa kolektif tidak dapat diatur dalam skrip API Explorer yang dapat digunakan kembali. Anda perlu mengaturnya setelah membuat CVM.
