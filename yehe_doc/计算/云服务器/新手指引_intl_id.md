Dokumen ini membantu Anda memulai instans Tencent Cloud Virtual Machine (CVM) dengan cepat. 

## 1. Ikhtisar
Tencent Cloud CVM adalah layanan komputasi cloud dapat diskalakan yang membebaskan Anda dari estimasi penggunaan sumber daya dan investasi di muka. Dengan Tencent Cloud CVM, Anda dapat memulai CVM dan men-deploy aplikasi secepatnya.


## 2. Mempelajari tentang CVM
Lihat dokumen berikut untuk mempelajari lebih lanjut tentang instans CVM.
- [Ikhtisar CVM](https://intl.cloud.tencent.com/document/product/213/495)
- [Mode Penagihan Instans](https://intl.cloud.tencent.com/document/product/213/2180)
- [Ikhtisar Batas Penggunaan](https://intl.cloud.tencent.com/document/product/213/15379)
- [Konsep](https://intl.cloud.tencent.com/document/product/213/38678).


## 3. Membuat Instans CVM
Anda dapat secara fleksibel memilih wilayah, model, citra, bandwidth jaringan publik, jumlah pembelian, dan masa berlaku di halaman [Konfigurasi Kustom](http://manage.qcloud.com/shoppingcart/shop.php?tab=cvm&_ga=1.91351132.770173325.1571651505) untuk membeli instans CVM guna memenuhi kebutuhan bisnis Anda.
Untuk membuat CVM dengan cara kustom, silakan lihat [Menyesuaikan Konfigurasi CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517) atau [Menyesuaikan Konfigurasi CVM Windows](https://intl.cloud.tencent.com/document/product/213/10516).
![](https://main.qcloudimg.com/raw/40c2812ff1294f901238cc3e39ba25f9.png)

## 4. Login ke Instans CVM
Setelah Anda membeli instans CVM, Anda dapat login ke instans tersebut. Untuk informasi selengkapnya, lihat:
 - [Login ke Instans Linux](https://intl.cloud.tencent.com/document/product/213/5436)
 - [Login ke Instans Windows](https://intl.cloud.tencent.com/document/product/213/5435)


Lalu Anda dapat login ke instans tersebut untuk menyimpan file lokal Anda, menggunakannya sebagai mesin virtual Anda atau situs web yang sudah dibuat. Untuk informasi dan praktik selengkapnya, lihat konten berikut.


## 5. Informasi yang Relevan

### Ikhtisar fitur konsol
| Fitur | Referensi |
|---------|---------|
| Buat instans CVM | [Panduan untuk Membuat Instans](https://intl.cloud.tencent.com/document/product/213/36302) |
| Beri nama instans atau CVM menurut aturan | [Penamaan Urutan Batch atau Penamaan Berbasis String Pola](https://intl.cloud.tencent.com/document/product/213/32020) |
| Melakukan upgrade atau downgrade spesifikasi CVM | [Mengubah Konfigurasi Instans](https://intl.cloud.tencent.com/document/product/213/2178) |
| Pilih pasangan kunci SSH sebagai metode login CVM terenkripsi dan kelola kunci SSH | [Mengelola Kunci SSH](https://intl.cloud.tencent.com/document/product/213/16691) |
| Ubah atau atur ulang kata sandi instans Anda | [Mengatur Ulang Kata Sandi Instans](https://intl.cloud.tencent.com/document/product/213/16566) |
| Hentikan, lepaskan, atau kembalikan instans CVM | [Menghentikan Instans](https://intl.cloud.tencent.com/document/product/213/4930) |
| Dapatkan daftar instans CVM dari suatu wilayah| [Ekspor Instans](https://intl.cloud.tencent.com/document/product/213/16563) |
| Telusuri instans CVM dan sumber daya lainnya| Penelusuran Lintas Wilayah |
| Buat citra kustom dan gunakan citra ini untuk memulai lebih banyak instans baru yang memiliki konfigurasi kustom yang sama dengan yang asli | [Membuat Citra Kustom](https://intl.cloud.tencent.com/document/product/213/4942) |
| Dapatkan citra yang dibagikan oleh pengguna lain, dapatkan komponen yang diperlukan, dan tambahkan konten kustom | [Berbagi Citra Kustom](https://intl.cloud.tencent.com/document/product/213/4944) |
| Impor citra disk sistem di komputer lokal atau platform lain ke citra kustom di CVM | [Ikhtisar](https://intl.cloud.tencent.com/document/product/213/4945) |
| Buat dan ekspor citra Linux | [Membuat Citra Linux](https://intl.cloud.tencent.com/document/product/213/17814) |
| Buat dan ekspor citra Windows | [Membuat Citra Windows](https://intl.cloud.tencent.com/document/product/213/17815) |
| Migrasikan sistem dan aplikasi di server sumber dari IDC Anda atau platform cloud lainnya ke Tencent Cloud | [Ikhtisar](https://intl.cloud.tencent.com/document/product/213/35639) |
| Perluas disk cloud untuk meningkatkan kapasitas penyimpanan | [Memperluas Disk Cloud](https://intl.cloud.tencent.com/document/product/213/32377) |
| Konversikan IP publik ke EIP untuk menutupi kegagalan instans | [IP Elastis](https://intl.cloud.tencent.com/document/product/213/16586) |
| Buat CVM dengan blok CIDR IPv6 dan aktifkan IPv6 untuk ENI, implementasikan komunikasi IPv6 melalui jaringan pribadi dan publik | [Mengonfigurasi IPv6](https://intl.cloud.tencent.com/document/product/213/34836) |
| Konfigurasikan grup keamanan berdasarkan kasus penggunaan | [Kasus Penggunaan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/32369) |
| Gunakan label untuk mengategorikan dan mengelola sumber daya CVM Anda | [Panduan Pengguna tentang Label](https://intl.cloud.tencent.com/document/product/213/19548) |
| Lihat data pemantauan instans CVM seperti CPU, memori, bandwidth jaringan, dan disk | [Mendapatkan Statistik Pemantauan](https://intl.cloud.tencent.com/document/product/213/5178) |

### Penggunaan lanjutan
Anda dapat membuat situs web atau forum pribadi pada instans CVM seperti yang diinstruksikan di [Menyiapkan Situs Web](https://intl.cloud.tencent.com/document/product/213/34815).

### Alat pengembang
Tencent Cloud API menyediakan berbagai alat termasuk API Explorer, TCCLI, SDK, dan API Inspector, membantu Anda dengan mudah menggunakan dan mengelola layanan Tencent Cloud dengan cepat dengan beberapa kode. 


## 6. Umpan Balik dan Saran
Jika memiliki keraguan atau saran saat menggunakan produk dan layanan Tencent Cloud CVM, Anda dapat mengirimkan umpan balik Anda melalui saluran berikut. Staf yang berdedikasi akan menghubungi Anda untuk memecahkan masalah Anda.
- Untuk melaporkan masalah dokumentasi produk seperti kesalahan tautan, konten, atau API, Anda dapat mengklik **Kirim Umpan Balik** di bagian bawah dokumen.
- Jika Anda mengalami masalah terkait produk, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category).

  


