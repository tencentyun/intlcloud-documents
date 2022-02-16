[//]: # (chinagitpath:XXXXX)

### Protobuf

Google Protocol buffer (Protobuf) adalah format penyimpanan data terstruktur yang ringan dan efisien yang dikembangkan oleh Google untuk serialisasi data terstruktur. Sangat cocok untuk penyimpanan data atau pertukaran data RPC. TcaplusDB mendefinisikan struktur tabel dan membuat serialisasi catatan data melalui Protobuf.

### Tabel TcaplusDB

Bagi tabel yang digunakan untuk penyimpanan data, strukturnya ditentukan menggunakan file Protobuf yang sesuai dengan semantik TcaplusDB. 
### Aplikasi

Ini adalah unit Aplikasi TcaplusDB, yang sesuai dengan Aplikasi game. AppID ditampilkan pada halaman informasi konfigurasi, dan digunakan sebagai parameter koneksi untuk tabel koneksi TcaplusDB SDK.

### AppKey

Ini adalah kunci unit Aplikasi TcaplusDB. AppKey ditampilkan pada halaman informasi konfigurasi, dan digunakan sebagai parameter koneksi untuk tabel koneksi TcaplusDB SDK.

### Unit Deployment (Zona)

Ini adalah unit deployment data dalam unit Aplikasi TcaplusDB, yang dapat diartikan sebagai zona. Beberapa zona dapat dibuat dalam Aplikasi, dan tabel dengan nama yang sama harus dibuat di zona yang berbeda. ZoneID ditampilkan di kolom **Deployment Unit** (Unit Deployment) dari daftar, dan digunakan sebagai parameter koneksi untuk tabel koneksi TcaplusDB SDK.

### Akses melalui jaringan VPC

Titik akses layanan direktori TcaplusDB adalah entri bagi pengguna untuk mengakses tabel TcaplusDB melalui Tcaplus SDK. URL jaringan VPC ditampilkan pada halaman informasi konfigurasi, dan digunakan sebagai parameter koneksi untuk tabel koneksi TcaplusDB SDK.





