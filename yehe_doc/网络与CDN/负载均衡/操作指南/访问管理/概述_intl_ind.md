Jika Anda menggunakan beberapa layanan Tencent Cloud seperti CLB, CVM, dan TencentDB yang dikelola oleh beberapa pengguna yang berbagi kunci akun Tencent Cloud Anda, mungkin Anda akan mengalami masalah berikut:
- Kunci Anda dibagikan oleh beberapa pengguna sehingga berisiko tinggi untuk disusupi.
- Anda tidak dapat membatasi izin akses pengguna lain, yang menimbulkan risiko keamanan karena potensi kesalahan operasi.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/17848) digunakan untuk mengelola izin akses ke sumber daya Tencent Cloud.Dengan CAM, Anda dapat menggunakan fitur manajemen identitas dan manajemen kebijakan untuk mengontrol sumber daya Tencent Cloud yang dapat diakses oleh subakun.

Misalnya, jika memiliki beberapa instance CLB dalam akun yang diterapkan di beberapa proyek, untuk mengelola izin akses dan memberi izin sumber daya, Anda dapat mengikat admin proyek A dengan kebijakan otorisasi, yang mengatur bahwa hanya admin ini yang dapat menggunakan sumber daya CLB dalam proyek A.

Jika Anda tidak perlu mengelola izin akses ke sumber daya CLB untuk subakun, silakan lewati bagian ini.Tindakan ini tidak akan memengaruhi pemahaman Anda dan penggunaan bagian lain dalam dokumentasi.

## Konsep Dasar di CAM
Akun root mengotorisasi subakun dengan mengikat kebijakan.Pengaturan kebijakan dapat ditetapkan khusus ke tingkat **API, Resource, User/User Group, Allow/Deny, and Condition** (API, Sumber Daya, Pengguna/Grup Pengguna, Izinkan/Tolak, dan Kondisi).

1.Akun
- **Root account** (Akun root)
Sebagai pemilik utama sumber daya Tencent Cloud, akun root berfungsi sebagai dasar bagi penagihan dan penghitungan biaya penggunaan sumber daya, serta dapat digunakan untuk masuk ke layanan Tencent Cloud.
- **Sub-account** (Subakun)
subakun dibuat oleh akun root, serta memiliki ID khusus dan kredensial identitas yang dapat digunakan untuk masuk ke Tencent Cloud Console.Akun root dapat membuat beberapa subakun (pengguna).**Subakun tidak memiliki sumber daya apa pun secara default; sebagai gantinya, sumber daya tersebut akan diotorisasi oleh akun root subakun.**
- **Identity credential** (Kredensial identitas)
Mencakup kredensial masuk dan sertifikat akses.**Login credential** (Kredensial masuk) merujuk pada nama pengguna dan kata sandi.**Access certificate** (Sertifikat akses) merujuk pada kunci API TencentCloud (SecretId dan SecretKey).
2.Sumber daya dan izin
- **Resource** (Sumber daya)
Sumber daya merupakan objek yang dioperasikan di layanan Tencent Cloud, seperti instance CVM dan instance VPC.
- **Permission** (Izin)
Izin adalah otorisasi untuk mengizinkan atau melarang pengguna tertentu ketika menjalankan operasi tertentu.Secara default, **akun root memiliki akses penuh ke sumber daya yang dimilikinya**, sedangkan **subakun tidak memiliki akses ke sumber daya apa pun yang dimiliki akun root**.
- **Policy** (Kebijakan)
Kebijakan adalah aturan sintaks yang digunakan untuk menetapkan dan menjelaskan satu atau beberapa izin.**Akun root** menjalankan otorisasi dengan **mengaitkan kebijakan** dengan pengguna/grup pengguna.

Untuk informasi selengkapnya, lihat [Ringkasan CAM](https://intl.cloud.tencent.com/document/product/598/10583).

## Dokumen Terkait

| Deskripsi Dokumen | Tautan |
| ----------------------- | ------------------------------------------------------------ |
| Hubungan antara kebijakan dan pengguna | [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601) |
| Struktur dasar kebijakan | [Referensi Elemen](https://intl.cloud.tencent.com/document/product/598/10603) |
| Produk lain yang mendukung CAM | [Layanan Cloud yang Didukung CAM](https://intl.cloud.tencent.com/document/product/598/10588) |
