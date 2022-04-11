TencentDB for MySQL mendukung fitur [Pengaktifan Enkripsi Data Transparan](https://intl.cloud.tencent.com/document/product/236/38491) yang dikembangkan oleh tim database Tencent Cloud. Enkripsi transparan berarti enkripsi dan dekripsi data tidak terlihat oleh Anda. Saat membuat tabel terenkripsi, Anda tidak perlu menentukan kunci enkripsinya, dan data akan dienkripsi saat menulis ke disk dan didekripsi saat membaca dari disk.

TDE menggunakan algoritme AES yang populer secara global dan kunci enkripsi 256-bit, yang dikelola di Tencent Cloud [KMS](https://intl.cloud.tencent.com/document/product/1030/31961). Anda harus mendapatkan izin untuk mengakses KMS dan dapat memutar kunci di Konsol KMS untuk lebih menyempurnakan keamanan sistem.

