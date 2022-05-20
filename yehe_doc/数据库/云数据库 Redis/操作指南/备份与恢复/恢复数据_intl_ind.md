
## Ikhtisar
TencentDB for Redis Edisi Memori (v2.8) dan Edisi CKV mendukung pemulihan seluruh instans dari file cadangan.
	
>?
>- Hanya TencentDB for Redis Edisi Memori (v2.8) dan Edisi CKV yang mendukung pemulihan instans. TencentDB for Redis Edisi Memori yang bukan v2.8 mendukung [kloning data](https://intl.cloud.tencent.com/document/product/239/31897) sebagai gantinya.
>- Memulihkan instans akan mengganggu layanan yang disediakan oleh instans tersebut.
>- Setelah instans dipulihkan, data yang ada akan ditimpa dan tidak dapat dipulihkan.
>- Jika instans Anda pernah diturunkan, Anda perlu memastikan bahwa spesifikasi instans lebih tinggi dari kapasitas data yang dipulihkan; jika tidak, pemulihan akan gagal.

## Prasyarat
Data instans telah dicadangkan. Untuk petunjuk pencadangan, lihat [Mencadangkan Data](https://intl.cloud.tencent.com/document/product/239/7071).

## Petunjuk
1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans dalam daftar instans, dan masuk ke halaman manajemen instans.
2. Pada tab **Backup and Restore** (Pencadangan dan Pemulihan), cari cadangan yang diinginkan dalam daftar cadangan, dan klik **Restore Instance** (Pulihkan Instans) di kolom **Operation** (Operasi).
3. Di kotak dialog pop-up, konfirmasikan bahwa semuanya sudah benar dan klik **OK** (OKE).
>!Jika instans dilindungi kata sandi, Anda harus memasukkan kata sandi instans di halaman ini, yang merupakan kata sandi yang Anda atur di halaman pembelian instans alih-alih kata sandi koneksi dengan format "ID instans:kata sandi instans" yang digunakan untuk akses instans.
>
4. Kembali ke daftar instans, di mana status instans ditampilkan sebagai **Restoring backup by backup ID** (Memulihkan cadangan dengan ID cadangan). Setelah status berubah menjadi "Running" (Berjalan), instans dapat digunakan secara normal.

