## Skenario
Dokumen ini menjelaskan cara membatalkan berbagi citra kustom. Anda dapat membatalkan status berbagi citra dengan pengguna lain kapan saja. Tindakan ini tidak memengaruhi instans yang dibuat oleh pengguna lain yang menggunakan citra yang dibagikan ini, tetapi instans tidak dapat lagi melihat citra atau membuat instans baru menggunakan citra ini.

## Petunjuk
### Membatalkan berbagi citra melalui konsol
 1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/).
 2. Di bilah sisi kiri, klik **Images** (Citra).
 3. Pilih tab **Custom Image** (Citra Kustom) untuk masuk ke halaman pengelolaan citra kustom.
 4. Dalam daftar citra kustom, pilih citra kustom yang ingin Anda batalkan berbaginya, lalu klik **More** (Lainnya) > **Cancel Sharing** (Batalkan Berbagi).
 5. Di halaman baru, pilih ID unik akun tempat Anda ingin membatalkan berbagi citra dan klik **Cancel Sharing** (Batalkan Berbagi).
 6. Di jendela pop-up, klik **OK** (OKE) untuk membatalkan berbagi citra.

### Membatalkan berbagi citra melalui API
Anda dapat menggunakan ModifyImageSharePermission API untuk membatalkan berbagi citra. Untuk informasi selengkapnya, lihat [ModifyImageSharePermission](https://intl.cloud.tencent.com/document/product/213/33268).
