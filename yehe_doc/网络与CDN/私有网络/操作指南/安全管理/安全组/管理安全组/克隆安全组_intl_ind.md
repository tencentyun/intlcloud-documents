## Skenario Operasi
Anda mungkin perlu mengkloning grup keamanan dalam skenario berikut:
- Anda telah membuat grup keamanan bernama sg-A di wilayah A dan ingin menerapkan aturan sg-A ke instans di wilayah B. Dalam hal ini, Anda dapat mengkloning sg-A ke wilayah B alih-alih membuat grup keamanan lain di wilayah B.
- Bisnis Anda perlu menjalankan aturan grup keamanan baru. Dalam hal ini, Anda dapat mengkloning grup keamanan asli untuk cadangan.



## Catatan
- Secara default, hanya aturan masuk dan keluar dari grup keamanan yang dikloning, tetapi bukan instans yang terhubung ke grup keamanan.
- Grup keamanan dapat dikloning antar proyek atau wilayah.

## Langkah

1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm).
2. Di bilah sisi kiri, klik **[Security Group] (https://console.cloud.tencent.com/cvm/securitygroup)** (Grup Keamanan) untuk masuk ke halaman manajemen grup keamanan.
3. Pada halaman manajemen grup keamanan, pilih **Region** (Wilayah) dan temukan baris grup keamanan yang akan dikloning.
4. Di kolom operasi, klik **More** (Lainnya) > **Clone** (Kloning).
5. Di jendela "Clone Security Group" (Kloning Grup Keamanan" yang muncul, pilih **Target Project** (Proyek Target) dan **Target Region** (Wilayah Target) untuk kloning, masukkan **New Name** (Nama Baru) untuk grup keamanan, dan klik **OK** (Oke).






