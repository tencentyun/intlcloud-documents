Jika Anda menggunakan beberapa layanan Tencent Cloud seperti VPC, CVM, dan TencentDB yang dikelola oleh pengguna berbeda yang membagikan kunci akun Tencent Cloud Anda, Anda mungkin mengalami masalah berikut:
- Kunci Anda dibagikan oleh beberapa pengguna, sehingga berisiko tinggi mengalami kebocoran.
- Anda tidak dapat membatasi izin akses pengguna lain yang menimbulkan risiko keamanan karena potensi kesalahan operasi.

Untuk mencegah masalah ini, sebaiknya gunakan sub-akun untuk mengizinkan pengguna yang berbeda mengelola layanan yang berbeda. Secara default, sub-akun tidak memiliki izin untuk menggunakan sumber daya terkait CVM atau CVM. Dengan demikian, Anda perlu membuat kebijakan untuk memberikan sumber daya atau izin yang diperlukan ke sub-akun.

## Ikhtisar
Tencent Cloud menyediakan layanan web yang disebut Cloud Access Management (CAM) untuk membantu pelanggan mengelola akses ke sumber dayanya dengan aman menggunakan akun Tencent Cloud mereka. Anda dapat menggunakan CAM untuk membuat, mengelola, dan menghentikan pengguna (atau grup pengguna), serta menggunakan manajemen identitas dan manajemen kebijakan untuk mengontrol sumber daya Tencent Cloud yang dapat digunakan oleh setiap pengguna.

Saat menggunakan CAM, Anda dapat menghubungkan kebijakan ke pengguna atau grup pengguna. Kebijakan dapat mengizinkan atau menolak permintaan pengguna untuk menggunakan sumber daya tertentu guna menyelesaikan tugas tertentu.
Untuk mengetahui informasi selengkapnya tentang kebijakan CAM, lihat [Sintaksis Kebijakan](https://intl.cloud.tencent.com/document/product/598/10603).
Untuk mengetahui informasi selengkapnya tentang cara menggunakan kebijakan CAM, lihat [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601).

Jika tidak perlu mengelola izin akses sub-akun untuk sumber daya VPC, Anda dapat melewati bagian ini. Ini tidak akan memengaruhi pemahaman Anda dan penggunaan bagian lain dalam dokumen.



## Memulai
Kebijakan CAM harus mengizinkan atau menolak penggunaan satu atau beberapa operasi VPC. Pada saat yang sama, kebijakan ini harus menentukan sumber daya (yang dapat berupa semua sumber daya atau sebagian sumber daya untuk operasi tertentu) yang dapat digunakan untuk operasi tersebut. Kebijakan juga dapat mencakup ketentuan yang ditetapkan untuk sumber daya operasi.

Beberapa operasi VPC API mendukung izin tingkat sumber daya. Artinya, saat memanggil API ini, Anda tidak dapat menentukan beberapa sumber daya untuk operasi tersebut. Sebaliknya, Anda harus menentukan semua sumber daya untuk operasi.


| Tugas | Tautan |
| -------------------- | -------------------- |
| Struktur dasar suatu kebijakan | Sintaksis Kebijakan |
| Menentukan operasi dalam kebijakan | Operasi VPC|
| Menentukan sumber daya dalam kebijakan | Jalur Sumber Daya VPC |
| Izin tingkat sumber daya yang didukung oleh VPC | [Izin Tingkat Sumber Daya yang Didukung oleh VPC](https://intl.cloud.tencent.com/document/product/215/31862) |
| Sampel konsol | [Sampel Konsol](https://intl.cloud.tencent.com/document/product/215/31861) |
