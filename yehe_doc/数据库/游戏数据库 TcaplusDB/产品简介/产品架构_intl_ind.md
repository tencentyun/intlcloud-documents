TcaplusDB adalah layanan database NoSQL terdistribusi yang sepenuhnya dihosting dan terutama terdiri dari lapisan manajemen, akses, dan penyimpanan. Lapisan akses dan penyimpanan keduanya terdiri dari beberapa node koneksi dan node penyimpanan dan mendukung penskalaan node horizontal. Setiap lapisan memiliki perannya sendiri, dan arsitektur keseluruhannya seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/3afc344e14b9f2d2b6eacf46b0751af6.jpg)

#### Lapisan manajemen
Lapisan manajemen TcaplusDB digunakan untuk menyimpan metadata dan informasi manajemen, menjadwalkan sistem TcaplusDB, dan mengelola data TcaplusDB.

#### Lapisan akses
Lapisan akses TcaplusDB digunakan untuk memproses permintaan pengguna, berinteraksi dengan node data di lapisan penyimpanan, dan mendapatkan data dan mengembalikannya ke pengguna.

#### Lapisan penyimpanan
Layanan lapisan penyimpanan adalah layanan inti dari TcaplusDB yang digunakan untuk menyimpan data pengguna, menanggapi permintaan lapisan akses, dan mengembalikan informasi data.

### Struktur Logika TcaplusDB
Struktur logika TcaplusDB terdiri dari kluster, grup tabel, dan tabel seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/486543524b9eb422f86682524c7aa3ad.jpg)

