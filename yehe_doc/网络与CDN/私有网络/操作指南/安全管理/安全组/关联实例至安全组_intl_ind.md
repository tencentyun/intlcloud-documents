## Skenario Operasi
Sebagai metode isolasi keamanan jaringan yang penting, grup keamanan digunakan untuk mengonfigurasi kontrol akses jaringan untuk satu atau lebih CVM. Anda dapat menghubungkan instans CVM dengan satu atau beberapa grup keamanan berdasarkan kebutuhan bisnis Anda. Dokumen ini menjelaskan cara menghubungkan instans CVM dengan grup keamanan di konsol.

## Prasyarat
Instans CVM telah dibuat.

## Langkah
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm).
2. Di bilah sisi kiri, klik **[Security Group] (https://console.cloud.tencent.com/cvm/securitygroup)** (Grup Keamanan) untuk masuk ke halaman manajemen grup keamanan.
3. Pada halaman manajemen grup keamanan, pilih **Region** (Wilayah), dan temukan baris grup keamanan yang ingin Anda tetapkan aturannya.
4. Di kolom operasi, klik **Manage instance** (Kelola instans) untuk masuk ke halaman **Associate with Instance** (Hubungkan ke Instans).
5. Di halaman **Associate with Instance** (Hubungkan ke Instans), klik **Add Association** (Tambahkan Hubungan).
6. Di jendela "Add Instance Association" (Tambahkan Hubungan Instans) yang muncul, pilih instans yang akan dihubungkan dengan grup keamanan dan klik **OK** (Oke).

## Operasi Selanjutnya
- Untuk melihat semua grup keamanan yang telah dibuat di suatu wilayah, mengkueri daftar grup keamanan.
Untuk detail tentang operasi, lihat [Melihat Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35507).
- Jika Anda tidak ingin instans CVM menjadi bagian dari satu atau beberapa grup keamanan, hapus instans dari grup tersebut.
Untuk detail tentang operasi, lihat [Menghapus dari Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35508).
- Jika bisnis tidak lagi membutuhkan satu atau beberapa grup keamanan, Anda dapat menghapusnya. Setelah Anda menghapus grup keamanan, semua aturan grup keamanan di dalamnya juga akan dihapus.
Untuk detail tentang operasi, lihat [Menghapus Grup Keamanan](https://intl.cloud.tencent.com/document/product/215/35510).

