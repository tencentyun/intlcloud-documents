## Ikhtisar Kluster
Kluster adalah unit manajemen TcaplusDB dasar yang menyediakan layanan TcaplusDB independen untuk bisnis.
Dari perspektif bisnis game, kluster dapat menyediakan layanan untuk submodul independen game atau keseluruhan game.

## Membuat Cluster
Untuk petunjuk terperinci, silakan lihat [Membuat Kluster](https://intl.cloud.tencent.com/document/product/1016/32714).


## Detail Kluster
Anda dapat melihat konfigurasi kluster dan detail atribut dengan masuk ke [Konsol TcaplusDB](https://console.cloud.tencent.com/tcaplusdb/app) dan mengklik ID kluster target.
Detail kluster terdiri dari tiga bagian:

##### Informasi Dasar
- ID Kluster: ID kluster unik yang dapat digunakan untuk menemukan kluster dan mengontrol akses ke kluster tetapi tidak dapat digunakan untuk koneksi database.
- ID Akses: ID koneksi kluster yang mengidentifikasi kluster saat Anda mengakses database melalui SDK atau alat klien.
- Protokol koneksi: protokol definisi tabel yang didukung oleh kluster. Saat ini, hanya Protocol Buffer yang didukung.
- Nama kluster: nama kluster yang dapat disesuaikan dengan kebutuhan.
- Wilayah: wilayah kluster.
- RESTful API	: alamat yang digunakan untuk akses database melalui RESTful API di subnet VPC yang sama.

##### Informasi jaringan
- Jaringan: informasi VPC tempat kluster saat ini berada.
- Subnet: informasi subnet tempat kluster saat ini berada.
- Alamat pribadi: alamat IP pribadi yang ditetapkan ke kluster saat ini. Instans CVM dalam subnet VPC yang sama dengan kluster dapat mengakses alamat IP ini.
- Port pribadi: nomor port akses yang ditetapkan ke kluster saat ini.

##### Informasi lainnya
- Waktu pembuatan: waktu pembuatan kluster saat ini.
- Kata sandi koneksi: jika lupa kata sandi, Anda dapat melihat kata sandi akses kluster di [konsol](https://console.cloud.tencent.com/tcaplusdb/app).
