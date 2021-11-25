Jika Anda menggunakan beberapa layanan Tencent Cloud seperti CVM, CBS, VPC, dan TencentDB yang dikelola oleh pengguna berbeda yang membagikan kunci akun Tencent Cloud Anda, Anda dapat menghadapi masalah berikut.
- Kunci Anda dibagikan oleh banyak pengguna, yang mengarah ke risiko pengungkapan yang tinggi.
- Anda tidak dapat mengontrol izin akses pengguna lain, yang menimbulkan risiko keamanan karena potensi kesalahan operasi.

Dalam hal ini, Anda dapat menggunakan sub-akun untuk memungkinkan pengguna yang berbeda mengelola layanan yang berbeda untuk menghindari masalah ini.Secara default, sub-akun tidak memiliki izin untuk menggunakan CVM atau sumber daya terkait CVM.Oleh karena itu, Anda perlu membuat kebijakan untuk memberikan sumber daya atau izin yang diperlukan ke sub-akun.

[Cloud Access Management (CAM)](https://intl.cloud.tencent.com/document/product/598/10583) adalah serangkaian layanan Tencent Cloud berbasis web yang membantu Anda mengelola dan mengontrol izin akses ke sumber daya Tencent Cloud.Dengan menggunakan CAM, Anda dapat membuat, mengelola, dan menghapus pengguna (grup) dan mengontrol siapa yang dapat menggunakan sumber daya Tencent Cloud dan sumber daya Tencent Cloud mana yang dapat mereka gunakan melalui Manajemen identitas dan kebijakan.

Saat menggunakan CAM, Anda dapat mengaitkan kebijakan dengan pengguna atau grup pengguna, yang memberikan atau menolak izin untuk menggunakan sumber daya tertentu untuk melakukan tugas tertentu.Untuk informasi selengkapnya tentang dasar-dasar kebijakan CAM, lihat [Sintaks Kebijakan](https://intl.cloud.tencent.com/document/product/598/10603).Untuk informasi selengkapnya tentang penggunaan kebijakan CAM, lihat [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601).

Jika Anda tidak perlu mengelola izin akses sub-akun ke sumber daya CBS, Anda dapat melewati bagian ini.Ini tidak akan memengaruhi pemahaman dan penerapan Anda terhadap bagian-bagian lain dari dokumen ini.

#### Memulai

Kebijakan CAM harus memberikan atau menolak izin ke satu atau lebih operasi CBS.Pada saat yang sama, kebijakan tersebut harus menentukan sumber daya yang dapat dioperasikan (yang dapat berupa semua sumber daya atau beberapa sumber daya untuk operasi tertentu).Kebijakan ini juga dapat mencakup kondisi yang ditetapkan untuk operasi sumber daya.

| Tugas | Tautan |
|---------|---------|
| Mempelajari struktur dasar suatu kebijakan | [Sintaks Kebijakan](https://intl.cloud.tencent.com/document/product/362/34221) |
| Menentukan operasi dalam kebijakan | [Operasi CBS](https://intl.cloud.tencent.com/document/product/362/34221) |
| Menentukan sumber daya dalam kebijakan | [Jalur Sumber Daya CBS](https://intl.cloud.tencent.com/document/product/362/34221) |
| Membatasi kebijakan dengan kondisi | [Kunci kondisi CBS](https://intl.cloud.tencent.com/document/product/362/34221) |
| Mempelajari izin tingkat sumber daya yang didukung oleh CBS | [Izin Tingkat Sumber Daya yang Didukung oleh CBS](https://intl.cloud.tencent.com/document/product/362/34220) |
| Melihat contoh konsol | [Contoh Konsol](https://intl.cloud.tencent.com/document/product/213/10312) |
