Dokumen ini menyediakan contoh konfigurasi untuk skenario yang memerlukan VPC dan jaringan klasik selama migrasi bisnis.


### Skenario
Konfigurasi sumber daya bisnis berbasis jaringan klasik:
+ Klien CVM mengakses CLB jaringan pribadi.
+ CLB jaringan pribadi terikat dengan dua CVM (CVM 1 dan CVM 2) sebagai server sebenarnya.
+ Aplikasi yang di-deploy di CVM 1 dan CVM 2 dapat mengakses layanan TencentDB for MySQL backend.

Permintaan:
+ Memigrasikan sumber daya dari jaringan klasik ke VPC
+ Klien berbasis VPC memiliki akses prioritas ke layanan CLB jaringan pribadi di jaringan klasik.
+ Akses jaringan klasik tetap tersedia selama satu bulan setelah migrasi.

### Proses migrasi
<dx-steps>
- Buat VPC
- Migrasikan layanan TencentDB
- Konfigurasikan koneksi terminal
- Buat CLB jaringan pribadi dan konfigurasikan layanan backend-nya
- Konfigurasikan Classiclink
- Rilis sumber daya jaringan klasik
</dx-steps>


### Langkah-langkah
1.  Buat VPC seperti yang diinstruksikan di [Membuat VPC](https://intl.cloud.tencent.com/document/product/215/31805).
2.  Migrasikan layanan TencentDB for MySQL ke VPC seperti yang diinstruksikan di [Beralih Jaringan](https://intl.cloud.tencent.com/document/product/236/31915).
    >? Selama migrasi, instans TencentDB tetap terhubung. Baik alamat IP jaringan klasik maupun alamat IP VPC tetap valid setelah migrasi, sehingga menjaga ketersediaan layanan Anda.
    >
    ![]()
3.  Konfigurasikan layanan koneksi terminal untuk mengizinkan klien CVM di VPC mengakses layanan CLB jaringan publik di jaringan klasik.
     ![]()
4.  Buat instans CLB jaringan pribadi dan server aslinya di VPC, dan konfigurasikan layanan terkait.
   ![]()
5.  Konfigurasikan Classiclink untuk mengizinkan CVM berbasis jaringan klasik mengakses instans CLB jaringan pribadi di VPC. Uji apakah VPC menyediakan layanan secara normal.
    ![]()
6.  Setelah layanan VPC normal dan CVM berbasis VPC mulai mengakses CLB jaringan pribadi di VPC, hapus koneksi terminal, pertahankan Classiclink, dan lepaskan sumber daya di jaringan klasik.
    ![]()

