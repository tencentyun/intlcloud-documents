## Masalah yang Diketahui
Jika Anda menggunakan beberapa layanan Tencent Cloud seperti CVM, VPC, dan TencentDB yang dikelola oleh pengguna berbeda yang membagikan kunci akun Tencent Cloud Anda, Anda mungkin menghadapi masalah berikut:
- Kunci Anda dibagikan oleh beberapa pengguna, sehingga berisiko tinggi untuk disusupi.
- Anda tidak dapat membatasi izin akses pengguna lain, yang menimbulkan risiko keamanan karena potensi kesalahan operasi.

## Solusi
Anda dapat mengizinkan pengguna yang berbeda untuk mengelola layanan yang berbeda melalui sub-akun untuk menghindari masalah di atas. Secara default, sub-akun tidak memiliki izin untuk menggunakan layanan Tencent Cloud atau sumber daya terkait. Dengan demikian, Anda perlu membuat kebijakan untuk memberikan izin yang diperlukan ke sub-akun.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) adalah layanan Tencent Cloud berbasis web yang membantu Anda mengelola dan mengontrol izin akses ke sumber daya Tencent Cloud dengan aman. Menggunakan CAM, Anda dapat membuat, mengelola, dan menghentikan pengguna (grup), dan mengontrol sumber daya Tencent Cloud yang dapat digunakan oleh pengguna tertentu melalui manajemen identitas dan kebijakan.

Saat menggunakan CAM, Anda dapat menghubungkan kebijakan dengan pengguna atau grup pengguna untuk mengizinkan atau melarang mereka menggunakan sumber daya tertentu untuk menyelesaikan tugas tertentu. Untuk informasi selengkapnya tentang kebijakan CAM, silakan lihat [Sintaksis Kebijakan](https://intl.cloud.tencent.com/document/product/598/10603).

Jika Anda tidak perlu mengelola izin akses ke sumber daya TencentDB untuk sub-akun, Anda dapat melewati bagian ini. Tindakan ini tidak akan memengaruhi pemahaman dan penggunaan Anda atas bagian lain dalam dokumentasi.

### Mulai
Kebijakan CAM harus mengizinkan atau menolak penggunaan satu atau beberapa operasi TencentDB. Pada saat yang sama, kebijakan harus menentukan sumber daya yang dapat digunakan untuk operasi (yang dapat berupa semua sumber daya atau sebagian sumber daya untuk operasi tertentu). Kebijakan juga dapat mencakup kondisi yang ditetapkan untuk sumber daya yang dimanipulasi.

>- Sebaiknya kelola sumber daya TencentDB dan otorisasi operasi TencentDB melalui kebijakan CAM. Meskipun pengalaman tetap sama untuk pengguna yang sudah ada yang diberikan izin oleh proyek, tidak disarankan untuk terus mengelola sumber daya dan mengotorisasi operasi dengan cara berbasis proyek.
>- Kondisi efektivitas tidak dapat diatur di TencentDB untuk saat ini.

| Tugas | Tautan |
|---------|---------|
| Struktur kebijakan dasar | [Sintaksis Kebijakan](https://intl.cloud.tencent.com/document/product/238/34584)|
| Definisi operasi dalam kebijakan | [Operasi TencentDB](https://intl.cloud.tencent.com/document/product/238/34584) |
| Definisi sumber daya dalam kebijakan | [Jalur Sumber Daya TencentDB](https://intl.cloud.tencent.com/document/product/238/34584)|
| Izin tingkat sumber daya yang didukung oleh TencentDB | [Izin Tingkat Sumber Daya yang Didukung oleh TencentDB](https://intl.cloud.tencent.com/document/product/238/34585)|

