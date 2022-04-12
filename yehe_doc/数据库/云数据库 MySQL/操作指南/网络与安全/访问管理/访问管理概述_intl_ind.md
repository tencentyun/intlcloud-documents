## Masalah yang Diketahui
Jika Anda memiliki beberapa pengguna yang mengelola berbagai layanan Tencent Cloud seperti CVM, VPC, dan TencentDB, dan mereka semua berbagi kunci akses akun Tencent Cloud Anda, Anda mungkin menghadapi masalah berikut:
- Risiko tinggi disusupinya kunci Anda karena banyak pengguna membagikannya.
- Pengguna Anda mungkin menimbulkan risiko keamanan dari kesalahan operasi karena kurangnya kontrol akses pengguna.

## Solusi
Anda dapat menghindari masalah di atas dengan mengizinkan pengguna yang berbeda untuk mengelola layanan yang berbeda melalui sub-akun. Secara default, sub-akun tidak memiliki izin untuk menggunakan layanan atau sumber daya Tencent Cloud. Dengan demikian, Anda perlu membuat kebijakan untuk memberikan izin yang berbeda ke sub-akun.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) adalah layanan Tencent Cloud berbasis web yang membantu Anda mengelola dan mengontrol akses ke sumber daya Tencent Cloud dengan aman. Dengan menggunakan CAM, Anda dapat membuat, mengelola, dan menghentikan pengguna dan grup pengguna. Anda dapat mengelola identitas dan kebijakan untuk mengizinkan pengguna tertentu mengakses sumber daya Tencent Cloud Anda.

Saat menggunakan CAM, Anda dapat mengaitkan kebijakan dengan pengguna atau grup pengguna untuk mengizinkan atau melarang mereka menggunakan sumber daya tertentu untuk menyelesaikan tugas tertentu. Untuk informasi selengkapnya tentang kebijakan CAM, harap lihat [Logika Sintaksis](https://intl.cloud.tencent.com/document/product/598/10603).

Anda dapat melewati bagian ini jika Anda tidak perlu mengelola izin ke sumber daya TencentDB untuk sub-akun. Ini tidak akan memengaruhi pemahaman dan penggunaan Anda atas bagian lain dalam dokumen.

### Mulai
Kebijakan CAM digunakan untuk mengizinkan atau menolak satu atau lebih operasi TencentDB. Saat mengonfigurasi kebijakan, Anda harus menentukan sumber daya target operasi, yang dapat berupa semua sumber daya atau sumber daya tertentu. Kebijakan juga dapat mencakup kondisi di mana sumber daya dapat digunakan.

>?
>- Sebaiknya kelola sumber daya TencentDB dan mengizinkan operasi TencentDB melalui kebijakan CAM. Meskipun pengalaman pengguna tidak berubah untuk pengguna yang sudah ada yang diberikan izin oleh proyek, kami tidak menyarankan Anda untuk terus mengelola sumber daya dan mengotorisasi operasi dengan cara berbasis proyek.
>- Kondisi tidak dapat diatur di TencentDB untuk saat ini.

| Tugas | Tautan | 
|---------|---------|
| Pelajari selengkapnya tentang struktur kebijakan dasar | [Sintaksis Kebijakan](https://intl.cloud.tencent.com/document/product/236/14466) |
| Menentukan operasi dalam kebijakan | [Operasi TencentDB](https://intl.cloud.tencent.com/document/product/236/14466) | 
| Menentukan sumber daya dalam kebijakan | [Jalur Sumber Daya TencentDB](https://intl.cloud.tencent.com/document/product/236/14466)|
| Izin tingkat sumber daya yang didukung oleh TencentDB | [Jenis Sumber Daya yang Dapat Diotorisasi](https://intl.cloud.tencent.com/document/product/236/14467)|
| Sampel konsol | [Sampel Konsol](https://intl.cloud.tencent.com/document/product/236/14468) |
