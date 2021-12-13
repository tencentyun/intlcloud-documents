## Skenario
Instans dapat dimatikan saat Anda perlu menghentikan layanan, atau mengubah konfigurasi yang hanya dapat dilakukan dalam keadaan nonaktif. Menonaktifkan instans sama halnya seperti mematikan komputer lokal.

## Catatan

- Anda dapat mematikan instans menggunakan perintah sistem (seperti perintah pematian pada sistem Windows dan sistem Linux) atau melalui konsol Tencent Cloud. Sebaiknya lihat proses pematian di konsol untuk memeriksa apakah ada masalah yang terjadi.
- Instans tidak akan lagi menyediakan layanan setelah pematian. Sebelum pematian, pastikan CVM telah berhenti menerima permintaan layanan.
- Selama pematian, status instans akan berubah dari "shutting down" (sedang mematikan) menjadi "shutdown" (dimatikan). Jika proses pematian memakan waktu terlalu lama, mungkin ada pengecualian. Untuk informasi selengkapnya, lihat [Menutup CVM](https://intl.cloud.tencent.com/document/product/213/2917) untuk menghindari pematian paksa.
- Setelah instans dimatikan, semua penyimpanan masih terhubung ke instans, dan semua data disk disimpan. Data dalam memori akan hilang.
- Mematikan instans tidak mengubah atribut fisiknya. IP publik dan pribadi dari instans tetap tidak berubah. [IP Publik Elastis](https://intl.cloud.tencent.com/document/product/213/5733) masih terikat ke instans. Namun, karena gangguan layanan, Anda akan menerima respons kesalahan saat mengakses IP ini. Hubungan [Classiclink](https://intl.cloud.tencent.com/document/product/215/31807) tetap tidak berubah.
- Jika instans milik [kluster server nyata](https://intl.cloud.tencent.com/document/product/214/32388) dari instans CLB, instans tersebut tidak dapat lagi menyediakan layanan setelah pematian.
Jika kebijakan pemeriksaan kesehatan telah dikonfigurasi, instans yang telah dimatikan akan diblokir secara otomatis dan permintaan tidak akan lagi diteruskan. Jika tidak, klien mungkin menerima kode kesalahan 502. Untuk informasi selengkapnya, lihat [Pemeriksaan Kesehatan](https://intl.cloud.tencent.com/document/product/214/38451).
- Jika instans yang telah dimatikan berada dalam [grup penskalaan otomatis](https://intl.cloud.tencent.com/document/product/377/3590), layanan penskalaan otomatis akan menandai instans memiliki kinerja yang buruk, dan dapat mengganti dan memindahkannya dari grup penskalaan otomatis. Untuk informasi selengkapnya, lihat [Penskalaan Otomatis](https://intl.cloud.tencent.com/document/product/377).

## Petunjuk
### Mematikan instans melalui konsol
 1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/).
 2. Pilih metode yang berbeda berdasarkan kebutuhan aktual.
  - Mematikan instans: pilih instans yang akan dimatikan, lalu klik **More**(Lainnya)>**Instance Status**(Status Instans)> **Shutdown**(Matikan)di kolom operasi di sisi kanan.
  - Mematikan beberapa instans: pilih semua instans untuk dimatikan, lalu klik **Shutdown** (Matikan) di bagian atas daftar untuk mematikan instans dalam batch.
  Alasan diberikan untuk instans yang tidak dapat dionaktifkan.

### Mematikan instans melalui API
Untuk informasi selengkapnya, lihat [StopInstances](https://intl.cloud.tencent.com/document/product/213/33235) API.

## Operasi Selanjutnya
Anda dapat mengubah atribut berikut hanya jika instans telah dimatikan.
- **Instance configuration (CPU, memory):** (Konfigurasi instans (CPU, memori):) Untuk mengubah jenis instans, lihat [Ubah Konfigurasi Instans](https://intl.cloud.tencent.com/document/product/213/2178).
- **Change password** (Ubah kata sandi:) lihat [Kata Sandi Login](https://intl.cloud.tencent.com/document/product/213/6093).
- **Load SSH key:** (Muat kunci SSH:) lihat [Kunci SSH](https://intl.cloud.tencent.com/document/product/213/6092).
