## Ikhtisar

**Shared image** (Citra yang dibagikan) berarti Anda berbagi dengan **others users** (pengguna lain) [**custom image** (citra kustom)](https://intl.cloud.tencent.com/document/product/213/4942) yang telah Anda buat. Anda juga dapat memperoleh citra yang dibagikan oleh pengguna lain, mendapatkan komponen yang diperlukan, dan menambahkan konten kustom.

>! Tencent Cloud tidak menjamin integritas atau keamanan citra yang dibagikan. Harap hanya gunakan citra yang dibagikan dari sumber yang dapat dipercaya.
>

## Catatan
 - Setiap citra dapat dibagikan kepada maksimal 50 pengguna Tencent Cloud.
 - Nama dan deskripsi citra yang dibagikan tidak dapat diubah. Komponen tersebut hanya digunakan untuk membuat instans CVM.
 - Citra yang dibagikan dengan pengguna lain tidak menempati kuota citra Anda sendiri.
 - Citra kustom yang telah dibagikan dengan orang lain dapat dihapus, asalkan Anda membatalkan berbagi citra terlebih dahulu. Untuk informasi selengkapnya, lihat [Membatalkan Berbagi Citra](https://intl.cloud.tencent.com/document/product/213/7148). Citra yang dibagikan yang Anda peroleh dari orang lain tidak dapat dihapus.
 - Citra kustom hanya dapat dibagikan dengan akun di wilayah yang sama dengan akun sumber. Untuk berbagi citra dengan pengguna di wilayah lain, Anda perlu menyalinnya ke wilayah target sebelum berbagi.
 - Citra yang dibagikan yang Anda peroleh dari orang lain tidak dapat dibagikan dengan pengguna ketiga.

## Petunjuk

### Mendapatkan ID akun root yang ingin Anda bagikan citranya

Citra yang dibagikan Tencent Cloud diidentifikasi oleh ID unik dari akun root yang ingin Anda bagikan citranya. Anda dapat memperoleh ID akun pengguna lain sebagai berikut:
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/).
2. Klik nama akun di sudut kanan atas dan pilih **Account Information** (Informasi Akun).
3. Lihat dan catat ID akun.
4. Minta pengguna lain untuk mengirimkan ID akun kepada Anda.

### Membagikan citra melalui konsol

 1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/).
 2. Klik **[Images](https://console.cloud.tencent.com/cvm/image)** ([Citra]) di bilah sisi kiri.
 3. Klik tab **Custom Image** (Citra Kustom) untuk masuk ke halaman pengelolaan citra kustom.
 4. Pilih citra kustom yang ingin Anda bagikan di daftar citra kustom, lalu klik **Share** (Bagikan) di sebelah kanan.
 5. Di jendela pop-up **Shared Image** (Citra yang Dibagikan), masukkan ID akun tempat Anda ingin membagikan citra, lalu klik **Share** (Bagikan).
 6. Akun lain harus masuk ke [konsol CVM](https://console.cloud.tencent.com/cvm/), lalu pilih **Images** (Citra) > **Shared Image** (Citra yang Dibagikan) untuk melihat citra yang telah Anda bagikan.
 7. Ulangi langkah-langkah di atas untuk membagikan citra dengan beberapa pengguna.

### Membagikan citra melalui API

Anda dapat menggunakan `ShareImage` API untuk membagikan citra. Untuk informasi selengkapnya, lihat [`ShareImage`](https://intl.cloud.tencent.com/document/api/213/2361) API.

