## Skenario
Anda mungkin perlu mengkloning grup keamanan jika Anda:
- Telah membuat grup keamanan sg-A di wilayah A dan Anda ingin menerapkan aturan yang sama ke instans di wilayah B. Anda dapat mengkloning sg-A ke wilayah B, daripada membuat grup keamanan baru dari awal.
- Memerlukan grup keamanan baru untuk layanan Anda tetapi ingin mengkloning grup keamanan lama sebagai cadangan.



## Catatan
- Secara default, saat Anda mengkloning grup keamanan, hanya aturan yang dikloning, bukan asosiasi dengan instans.
- Anda dapat mengkloning grup keamanan di seluruh proyek dan wilayah.

## Petunjuk

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/index).
2. Di bilah sisi kiri, pilih **[Security Group](https://console.cloud.tencent.com/cvm/securitygroup)** ([Grup Keamanan]). Halaman Grup Keamanan kemudian akan muncul.
3. Pilih wilayah yang diinginkan. Daftar grup keamanan di bawah wilayah kemudian akan muncul.
4. Temukan grup keamanan yang diinginkan, lalu klik **More** (Lainnya). Kemudian klik **Clone** (Kloning). Halaman **Clone security group** (Kloning grup keamanan) kemudian akan muncul.
5. Pilih **Target region** (Wilayah target) dan **Target project** (Proyek target), lalu masukkan **New name** (Nama baru) untuk grup keamanan baru. Klik **OK** (OKE).






