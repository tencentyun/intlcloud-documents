## Masalah yang Diketahui
Jika Anda menggunakan beberapa layanan Tencent Cloud seperti TcaplusDB, VPC, CVM, dan TencentDB yang dikelola oleh pengguna berbeda yang membagikan kunci akun Tencent Cloud Anda, Anda mungkin menghadapi masalah berikut:
- Kunci Anda dibagikan oleh banyak pengguna, sehingga berisiko tinggi untuk disusupi.
- Anda tidak dapat membatasi izin akses pengguna lain, yang menimbulkan risiko keamanan karena potensi kesalahan operasi.

## Solusi
Anda dapat mengizinkan pengguna yang berbeda untuk mengelola layanan yang berbeda melalui sub-akun untuk menghindari masalah di atas. Secara default, sub-akun tidak memiliki izin untuk menggunakan layanan atau sumber daya TcaplusDB. Dengan demikian, Anda perlu membuat kebijakan untuk memberikan izin yang diperlukan ke sub-akun.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) adalah layanan Tencent Cloud berbasis web yang membantu Anda mengelola dan mengontrol izin akses ke sumber daya Tencent Cloud dengan aman. Menggunakan CAM, Anda dapat membuat, mengelola, dan menghentikan pengguna (grup), dan mengontrol sumber daya Tencent Cloud yang dapat digunakan oleh pengguna tertentu melalui manajemen identitas dan kebijakan.

Saat menggunakan CAM, Anda dapat mengaitkan kebijakan dengan pengguna atau grup pengguna untuk mengizinkan atau melarang mereka menggunakan sumber daya tertentu untuk menyelesaikan tugas tertentu. Untuk informasi selengkapnya tentang kebijakan CAM, silakan lihat [Sintaksis Kebijakan](https://intl.cloud.tencent.com/document/product/598/10603).

Jika Anda tidak perlu mengelola izin akses ke sumber daya TcaplusDB untuk sub-akun, Anda dapat melewati bagian ini. Ini tidak akan memengaruhi pemahaman dan penggunaan Anda atas bagian lain dalam dokumentasi.

### Memulai
Kebijakan CAM harus mengizinkan atau menolak penggunaan satu atau beberapa operasi TcaplusDB. Pada saat yang sama, kebijakan harus menentukan sumber daya yang dapat digunakan untuk operasi (yang dapat berupa semua sumber daya atau sebagian sumber daya untuk operasi tertentu). Kebijakan juga dapat mencakup kondisi yang ditetapkan untuk sumber daya yang dimanipulasi.

TencentCloud API tertentu untuk TcaplusDB tidak mendukung izin tingkat sumber daya, yang berarti bahwa untuk jenis operasi API ini, Anda tidak dapat menentukan sumber daya yang diberikan untuk digunakan saat dijalankan; sebagai gantinya, Anda harus menentukan semua sumber daya yang akan digunakan.


| Tugas | Tautan |
| -------------------------- | ------------------------------------------------------------ |
| Struktur kebijakan dasar | [Sintaksis Kebijakan](https://intl.cloud.tencent.com/document/product/1016/35751) |
| Definisi operasi dalam kebijakan | [Operasi TcaplusDB](https://intl.cloud.tencent.com/document/product/1016/35751) |
| Definisi sumber daya dalam kebijakan | [Jalur Sumber Daya TcaplusDB](https://intl.cloud.tencent.com/document/product/1016/35751) |
| Izin tingkat sumber daya yang didukung di TcaplusDB | [Izin Tingkat Sumber Daya yang Didukung di TcaplusDB](https://intl.cloud.tencent.com/document/product/1016/35750) |
| Contoh Konsol | [Contoh Konsol](https://intl.cloud.tencent.com/document/product/1016/35752) |

