### Bagaimana CVM atau Database Berinterkoneksi melalui Jaringan Pribadi?
Komunikasi jaringan pribadi CVM atau database di VPC sebenarnya adalah komunikasi alamat IP pribadi di tingkat jaringan, dan oleh karena itu tidak ada perbedaan di antara keduanya. Metode komunikasi di bawah skenario alamat IP pribadi yang berbeda adalah sebagai berikut:

| Skenario Komunikasi | Metode Komunikasi |
|---------------|------------|
| Wilayah berbeda | CVM atau database di wilayah berbeda dimiliki oleh instans VPC yang berbeda dan saling berkomunikasi melalui [peeering connection](https://intl.cloud.tencent.com/document/product/553/18836) atau [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Baik komunikasi akun yang sama maupun lintas akun didukung.) |
| Zona ketersediaan berbeda | VPC yang sama: mendukung interkoneksi secara default.<br>Instans VPC yang berbeda: berkomunikasi melalui [koneksi peering](https://intl.cloud.tencent.com/document/product/553/18836) atau [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Baik komunikasi akun yang sama maupun lintas akun didukung.) |
| Instans VPC yang berbeda | Berkomunikasi melalui [koneksi peering](https://intl.cloud.tencent.com/document/product/553/18836) atau [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Baik komunikasi akun yang sama maupun lintas akun didukung.) |
| Subnet yang berbeda | VPC yang sama: mendukung interkoneksi secara default.<br>VPC yang berbeda: berkomunikasi melalui [koneksi peering](https://intl.cloud.tencent.com/document/product/553/18836) atau [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Baik komunikasi akun yang sama maupun lintas akun didukung.) |
| Lintas akun | Komunikasi lintas-akun melalui [koneksi peering](https://intl.cloud.tencent.com/document/product/553/18836) atau [CCN](https://intl.cloud.tencent.com/document/product/1003/31985). (Baik komunikasi wilayah yang sama dan lintas wilayah didukung.) |
 
>!
>- Untuk interkoneksi VPC lintas akun melalui koneksi peering atau CCN, perhatikan hal-hal berikut: 
    - Akun root memiliki sumber daya. Jika Anda ingin berkomunikasi dengan akun lain melalui koneksi peering atau CCN, masukkan akun root. 
    - Sub-akun hanya memiliki izin operasi secara default. Terapkan izin dari akun root untuk membuat koneksi peering atau CCN jika diperlukan.
>- **Private network default interconnection** (Interkoneksi default jaringan pribadi) ada di antara subnet yang berbeda dengan VPC yang sama (baik berada di zona ketersediaan yang sama maupun tidak). Jika tidak dapat saling terhubung, Anda dapat memecahkan masalah kebijakan firewall [grup keamanan](https://intl.cloud.tencent.com/document/product/213/12452) dan [ACL jaringan](https://intl.cloud.tencent.com/document/product/215/5132) terlebih dahulu.


### Apa yang Harus Saya Lakukan Ketika Koneksi Peering Gagal Dibuat Karena Konflik Rentang IP VPC?
Saat Anda mencoba membuat koneksi peering, blok CIDR dari dua instans VPC tidak boleh tumpang tindih, jika tidak, koneksi peering tidak dapat dibuat.

- Jika rentang IP dari kedua instans VPC yang perlu saling berkomunikasi tumpang tindih tetapi rentang IP subnet tidak tumpang tindih, maka Anda dapat mencoba membangun komunikasi melalui [CCN](https://intl.cloud.tencent.com/product/ccn). CCN dapat menurunkan batas rentang alamat IP ke tingkat subnet saat instans VPC saling berkomunikasi.
Misalnya, rentang IP dari kedua instans VPC yang perlu saling berkomunikasi adalah `10.0.0.0/16`, tetapi subnetnya masing-masing adalah `10.0.1.0/24` dan `10.0.2.0/24`. Dalam kasus ini, Anda dapat membangun komunikasi melalui CCN. Untuk informasi selengkapnya, lihat [CCN](https://intl.cloud.tencent.com/document/product/1003).
- Jika kebutuhan Anda tidak dapat dipenuhi menggunakan CCN, Anda perlu memigrasikan sumber daya di dalam subnet yang tumpang tindih.
    - Untuk detail tentang mengubah subnet CVM, lihat [Mengubah Subnet Instans](https://intl.cloud.tencent.com/document/product/213/16565).
    - Untuk detail tentang migrasi antar-VPC, lihat [Mengalihkan Instans VPC](https://intl.cloud.tencent.com/document/product/213/20278).

### Jika VPC1 Secara Terpisah Membuat Koneksi Peering Dengan VPC2 dan VPC3, Lalu Bisakah VPC2 dan VPC3 Saling Berkomunikasi?
Tidak, tidak bisa. Dua instans VPC dapat membuat interkoneksi melalui koneksi peering, tetapi hubungan interkoneksi ini tidak transitif. Ini berarti bahwa ketika koneksi peering dibuat antara VPC1 dan VPC2, sementara koneksi peering lain dibuat antara VPC1 dan VPC3, interkoneksi lalu lintas tidak tersedia antara VPC2 dan VPC3 karena koneksi peering tidak transitif.

