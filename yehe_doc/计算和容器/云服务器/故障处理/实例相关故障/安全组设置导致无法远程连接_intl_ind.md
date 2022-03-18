
Dokumen ini menjelaskan cara memecahkan masalah saat Anda tidak dapat terhubung ke CVM dari jarak jauh karena masalah konfigurasi grup keamanan.

## Alat Diagnostik

Anda dapat menggunakan [Verifikasi Port](https://console.cloud.tencent.com/vpc/helper) untuk memeriksa apakah masalah disebabkan oleh konfigurasi grup keamanan.
1. Login ke [Verifikasi Port](https://console.cloud.tencent.com/vpc/helper).
2. Di halaman **Port Verification** (Verifikasi Port), pilih instans yang akan diperiksa dan klik **Quick Check** (Pemeriksaan Cepat). Hal ini ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/a792a1692e0a21b3f9dfe111d4b86789.png)
Jika pemeriksaan menunjukkan bahwa instans memiliki port yang tidak terbuka, Anda dapat memilih **Open all ports** (Buka semua port) untuk membuka semua port CVM yang umum digunakan ke Internet, dan mencoba login lagi dari jarak jauh.

<img src="https://main.qcloudimg.com/raw/a743739b5885874c15a6b5c7869f5acd.png" height="400" width="420">


## Memodifikasi konfigurasi grup keamanan

Jika Anda tidak ingin menggunakan **Open all ports** (Buka semua port) untuk membuka semua port CVM yang umum digunakan ke Internet, atau Anda perlu menyesuaikan port login jarak jauh, Anda dapat menggunakan konfigurasi khusus dari aturan masuk dan keluar dari grup keamanan untuk mengatasi kegagalan login jarak jauh. Untuk informasi selengkapnya, lihat [Memodifikasi Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34825).
