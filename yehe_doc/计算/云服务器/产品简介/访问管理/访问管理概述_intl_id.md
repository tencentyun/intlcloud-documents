Jika Anda menggunakan beberapa layanan Tencent Cloud seperti Cloud Virtual Machine (CVM), VPC, dan TencentDB, kemungkinan layanan tersebut dikelola oleh pengguna yang berbeda yang menggunakan semua kunci akun Anda. Tindakan ini menimbulkan tantangan berikut:
- Kunci Anda dibagikan oleh beberapa pengguna, sehingga berisiko tinggi untuk disusupi.
- Anda tidak dapat membatasi akses pengguna ke sumber daya yang berbeda, yang akan menimbulkan risiko keamanan karena potensi kesalahan operasi.

Anda dapat menggunakan sub-akun untuk menyelesaikan masalah ini. Sub-akun memungkinkan Anda menetapkan akun yang berbeda kepada setiap pengguna agar dapat melakukan tugasnya tanpa risiko mengganggu orang lain. Namun, sub-akun secara default tidak memiliki izin untuk mengakses instans CVM dan sumber daya terkait. Anda perlu membuat kebijakan yang sesuai untuk setiap sub-akun guna memberikan akses ke sub-akun tersebut.

Tencent Cloud menyediakan layanan web yang disebut Cloud Access Management (CAM) untuk membantu pelanggan mengelola akses ke sumber dayanya dengan aman menggunakan akun Tencent Cloud mereka. CAM memungkinkan Anda membuat, mengelola, atau menghentikan pengguna dan grup pengguna, serta menyediakan manajemen identitas dan manajemen kebijakan untuk mengontrol pengguna yang diizinkan untuk mengakses dan menggunakan sumber daya Tencent Cloud.

Anda dapat mengaitkan kebijakan CAM dengan pengguna atau grup pengguna untuk memberikan atau menolak izin mereka untuk menggunakan sumber daya tertentu guna melakukan tugas tertentu. Untuk mengetahui informasi selengkapnya tentang kebijakan CAM, lihat [Sintaksis Kebijakan](https://intl.cloud.tencent.com/document/product/598/10603). Untuk mengetahui informasi selengkapnya tentang cara menggunakan kebijakan CAM, lihat [Kebijakan](https://intl.cloud.tencent.com/document/product/598/10601).

Jika tidak perlu mengelola akses sumber daya multi-pengguna, Anda dapat melewati bagian ini. Melakukan tindakan ini tidak akan memengaruhi pemahaman Anda tentang artikel lainnya.

#### Memulai

Kebijakan CAM harus mengizinkan atau menolak satu atau beberapa operasi CVM, serta sumber daya yang ditargetkan oleh tindakan ini. Kebijakan juga dapat mencakup kondisi yang mengatur penggunaan sumber daya.

Beberapa CVM API tidak mendukung izin tingkat sumber daya, yang berarti Anda harus menentukan semua sumber daya, bukan sumber daya tertentu saat melakukan operasi API tersebut.

| Tugas | Tautan | 
|---------|---------|
| Pelajari selengkapnya tentang struktur kebijakan dasar | [Sintaksis Kebijakan](https://intl.cloud.tencent.com/document/product/213/10313) |
| Menentukan operasi dalam kebijakan | [Operasi CVM](https://intl.cloud.tencent.com/document/product/213/10313) | 
| Menentukan sumber daya dalam kebijakan | [Jalur Sumber Daya CVM](https://intl.cloud.tencent.com/document/product/213/10313) |
| Membatasi kebijakan dengan kondisi | [Kunci Kondisi CVM](https://intl.cloud.tencent.com/document/product/213/10313) |
| Izin tingkat sumber daya yang didukung oleh CVM | [Izin Tingkat Sumber Daya yang Didukung oleh CVM](https://intl.cloud.tencent.com/document/product/213/10314) |
| Sampel konsol | [Sampel Konsol](https://intl.cloud.tencent.com/document/product/213/10312) |
