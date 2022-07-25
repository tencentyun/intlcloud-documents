Fitur pengambilan tangkapan layar dan deteksi pornografi dinonaktifkan secara default untuk push langsung. Dokumen ini menjelaskan cara mengikat/melepaskan ikatan nama domain push ke/dari template pengambilan tangkapan layar dan deteksi pornografi guna mengaktifkan/menonaktifkan fitur pengambilan tangkapan layar dan deteksi pornografi.

## Catatan
- Konfigurasi templat akan diterapkan dalam waktu sekitar **5–10 menit**.
- Setelah mengonfigurasikan templat pengambilan tangkapan layar dan deteksi pornografi, Anda perlu mengonfigurasikan templat panggilan balik agar Anda dapat menerima hasil pengambilan tangkapan layar atau deteksi pornografi. Informasi selengkapnya tentang cara mengonfigurasikan templat panggilan balik dapat dilihat di [Callback Configuration (Konfigurasi Panggilan Balik)](https://intl.cloud.tencent.com/document/product/267/31065).
- Satu nama domain hanya dapat diikatkan ke satu templat pengambilan tangkapan layar dan deteksi pornografi. Setelah pengikatan, pengambilan tangkapan layar dan deteksi pornografi akan dilakukan pada semua streaming yang diikat sesuai dengan templat ini.

## Prasyarat
 - Anda telah login ke [konsol CSS](https://console.cloud.tencent.com/live) dan menambahkan [nama domain push](https://intl.cloud.tencent.com/document/product/267/35970). 
 - Anda telah membuat [templat pengambilan tangkapan layar dan deteksi pornografi](https://intl.cloud.tencent.com/document/product/267/31072).


## Mengikat Templat Pengambilan Tangkapan Layar dan Deteksi Pornografi

1. 	Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik nama domain push yang akan dikonfigurasikan atau **Manage** (Kelola) untuk membuka halaman detail nama domain.
2. Pilih **Template Configuration** (Konfigurasi Templat), lalu klik **Edit** di bagian **Screencapture & Porn Detection Configuration** (Konfigurasi Pengambilan Tangkapan Layar & Deteksi Pornorafi).
![](https://qcloudimg.tencent-cloud.cn/raw/17f2d3e8f3fff6a1c3eeec09651caf37.png)
3. Pilih templat pengambilan tangkapan layar dan deteksi pornografi, lalu klik **Confirm** (Konfirmasi).
![](https://qcloudimg.tencent-cloud.cn/raw/39d729e20b7bb2b152d29eba3723f382.png)


## Melepaskan Ikatan Templat Pengambilan Tangkapan Layar dan Deteksi Pornografi
1. Buka **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** (Manajemen Domain), lalu klik nama domain push yang akan dikonfigurasikan atau **Manage** (Kelola) untuk membuka halaman detail nama domain.
2. Pilih **Template Configuration** (Konfigurasi Templat), lalu klik **Edit** di bagian **Screencapture & Porn Detection Configuration** (Konfigurasi Pengambilan Tangkapan Layar & Deteksi Pornorafi).
3. Hapus templat target dan klik **Confirm** (Konfirmasi).
![](https://qcloudimg.tencent-cloud.cn/raw/f369adcf9c705a00024c50e8d6f94fea.png)
