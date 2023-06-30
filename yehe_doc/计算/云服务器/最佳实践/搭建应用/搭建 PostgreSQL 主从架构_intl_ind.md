## Ikhtisar

PostgreSQL adalah sistem manajemen database relasional sumber terbuka yang menekankan skalabilitas dan kepatuhan standar. PostgreSQL sangat ideal untuk sistem pemrosesan transaksi online (OLTP) kompleks tingkat perusahaan. Ini mendukung jenis data NoSQL (JSON/XML/hstore) dan Sistem Informasi Geografis (GIS). Menampilkan keandalan dan integritas data yang kuat, PostgreSQL cocok untuk situs web, sistem aplikasi lokasi, pemrosesan objek data yang kompleks, dan kasus penggunaan lainnya.

Dokumen ini menjelaskan cara membangun sistem PostgreSQL pada instans CVM yang menjalankan CentOS 7.

## Perangkat Lunak
Dokumen ini menggunakan perangkat lunak berikut sebagai contoh untuk membangun PostgreSQL.
Linux: Sistem operasi Linux. Dokumen ini menggunakan CentOS 7.6 sebagai contoh.
PostgreSQL: Sistem manajemen database relasional. Dokumen ini menggunakan PostgreSQL 11.2 sebagai contoh.


## Prasyarat
- Dua instans CVM yang dibuat. Satu instans CVM berfungsi sebagai node utama dan yang lainnya berfungsi sebagai node sekunder.
Untuk informasi selengkapnya, lihat [Membuat Instans melalui Halaman Pembelian CVM](https://intl.cloud.tencent.com/document/product/213/4855).
- Aturan grup keamanan untuk dua instans CVM telah dikonfigurasi. Buka port 5432.
Untuk informasi selengkapnya, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272).

## Petunjuk

### Mengonfigurasi node utama

1. Login ke instans CVM utama.
2. Jalankan perintah berikut untuk meningkatkan semua paket, versi sistem, dan kernel.
```
yum update -y
```
3. Jalankan perintah berikut untuk menginstal repositori penyimpanan PostgreSQL.
```
yum install https://download.postgresql.org/pub/repos/yum/reporpms/EL-6-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
4. Jalankan perintah berikut untuk menginstal paket klien.
```
yum install postgresql11
```
5. Jalankan perintah berikut untuk menginstal paket server.
```
yum install postgresql11-server
```
6. Jalankan perintah berikut untuk menginisialisasi database.
```
/usr/pgsql-11/bin/postgresql-11-setup initdb
```
7. Jalankan perintah berikut untuk memulai layanan.
```
systemctl start postgresql-11
```
8. Jalankan perintah berikut untuk mengaktifkan layanan mulai otomatis.
```
systemctl enable postgresql-11
```
9. Jalankan perintah berikut untuk beralih ke pengguna `postgres`.
```
su - postgres
```
10. Jalankan perintah berikut untuk masuk ke terminal PostgreSQL.
```
psql
```
11. Jalankan perintah berikut untuk mengatur kata sandi untuk pengguna `postgres`.
```
ALTER USER postgres WITH PASSWORD 'Kata sandi kustom';
```
12. Jalankan perintah berikut untuk membuat akun database (seperti `postuser`) dan mengatur kata sandi, izin login, dan izin cadangan.
```
buat nama akun peran, login, replikasi, kata sandi terenkripsi, 'Kata sandi kustom';
```
Misalnya, gunakan perintah berikut untuk membuat akun database dengan nama `postuser` dengan kata sandi `postuser`:
```
buat peran replikasi login postuser kata sandi terenkripsi 'postuser';
```
13. Jalankan perintah berikut untuk memeriksa apakah akun telah dibuat.
```
SELECT usename from pg_user;
```
Jika hasil berikut ditampilkan, ini menunjukkan bahwa akun telah berhasil dibuat.
```
usename  
 ----------
postgres
postuser
(2 baris)
```
14. Jalankan perintah berikut untuk memeriksa apakah izin telah ditetapkan.
```
SELECT rolname from pg_roles;
```
Jika hasil berikut dikembalikan, itu menunjukkan bahwa izin telah berhasil ditetapkan.
```
rolname  
 ----------
postgres
postuser
(2 baris)
```
15. Masukkan **\q** (\q) dan tekan **Enter** (Enter) untuk keluar dari terminal PostgreSQL.
16. Masukkan **exit** (keluar) dan tekan **Enter** (Enter) untuk keluar dari PostgreSQL.
17. Jalankan perintah berikut untuk membuka file `pg_hba.conf`.
```
vim /var/lib/pgsql/11/data/pg_hba.conf
```
18. Tekan **i** (i) untuk beralih ke mode edit. Tambahkan dua baris berikut ke `IPv4 local connections`.
```
host    semua             semua             <IPv4 IP range of the secondary node’s VPC>          md5     #Aktifkan enkripsi kata sandi MD5 untuk koneksi dalam rentang IP VPC
akun    database     replikasi host        <IPv4 IP range of the secondary node’s VPC>        md5     ##Izinkan sinkronisasi data dari database `replication`.
```
Misalnya, jika akun database adalah `postuser` dan rentang IP IPv4 dari VPC node sekunder adalah `192.10.0.0/16`, tambahkan konten berikut ke `IPv4 local connection`:
```
host    semua             semua             192.10.0.0/16          md5
host    replikasi     postuser        192.10.0.0/16          md5
```
19. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan file.
20. Jalankan perintah berikut untuk membuka file `postgresql.conf`.
```
vim /var/lib/pgsql/11/data/postgresql.conf
```
21. Tekan **i** (i) untuk masuk ke mode edit, cari dan ubah parameter berikut.
```
listen_addresses = 'xxx.xxx.xxx.xxx'   #Alamat IP pribadi yang didengarkan.
max_connections = 100    #Koneksi maksimum. Nilai `max_connections` untuk node sekunder harus lebih besar dari pada node utama
wal_level = hot_standby  #Aktifkan mode siaga panas.
synchronous_commit = on  #Aktifkan replikasi sinkron
max_wal_senders = 32     #Jumlah maksimum proses sinkronisasi
wal_sender_timeout = 60 detik ##Nilai batas waktu untuk instans replikasi streaming untuk mengirim data.
```
22. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan dan menutup file.
23. Jalankan perintah berikut untuk memulai ulang layanan SSH.
```
systemctl restart postgresql-11
```

### Mengonfigurasi node sekunder

1. Login ke instans CVM sekunder.
2. Jalankan perintah berikut untuk meningkatkan semua paket, versi sistem, dan kernel.
```
yum update -y
```
3. Jalankan perintah berikut untuk menginstal repositori penyimpanan PostgreSQL.
```
yum install https://download.postgresql.org/pub/repos/yum/reporpms/EL-6-x86_64/pgdg-redhat-repo-latest.noarch.rpm
```
4. Jalankan perintah berikut untuk menginstal paket klien.
```
yum install postgresql11
```
5. Jalankan perintah berikut untuk menginstal paket server.
```
yum install postgresql11-server
```
6. Jalankan perintah berikut dan gunakan utilitas pg_basebackup untuk membuat direktori cadangan:
```
pg_basebackup -D /var/lib/pgsql/11/data -h Private IP of primary node -p 5432 -U Database account -X stream -P
```
Misalnya, jika IP pribadi dari node utama adalah `192.10.123.321`, dan akun database adalah `postuser`, jalankan perintah berikut:
```
pg_basebackup -D /var/lib/pgsql/11/data -h 192.10.123.321 -p 5432 -U postuser -X stream -P
```
Masukkan kata sandi seperti yang diminta, dan tekan **Enter** (Enter). Jika hasil berikut ditampilkan, ini menunjukkan bahwa direktori cadangan telah berhasil dibuat.
```
Kata sandi: 
24526/24526 kB (100%), 1/1 tablespace
```
7. Jalankan perintah berikut untuk menyalin file konfigurasi node utama.
```
cp /usr/pgsql-11/share/recovery.conf.sample /var/lib/pgsql/11/data/recovery.conf
```
8. Jalankan perintah berikut untuk membuka file `recovery.conf`.
```
vim /var/lib/pgsql/11/data/recovery.conf
```
9. Tekan **i** (i) untuk beralih ke mode edit, cari dan ubah parameter berikut:
```
standby_mode = on     #Deklarasikan node sekunder
primary_conninfo = ‘host=<Private IP of the primary node> port=5432 user=Database account password=Database password’ #Informasi koneksi node utama
recovery_target_timeline = ‘latest’ #Sinkronkan data terbaru menggunakan replikasi streaming
```
10. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan file.
11. Jalankan perintah berikut untuk membuka file `postgresql.conf`.
```
vim /var/lib/pgsql/11/data/postgresql.conf
```
12. Tekan **i** (i) untuk beralih ke mode edit, cari dan ubah parameter berikut:
```
listen_addresses= 'xxx.xx.xx.xx'   #Alamat IP pribadi yang didengarkan.
max_connections = 1000             #Koneksi maksimum. Nilai `max_connections` untuk node sekunder harus lebih besar dari pada node utama
hot_standby = on                   #Aktifkan mode siaga panas
max_standby_streaming_delay = 30 detik  #Penundaan maksimum untuk replikasi streaming
wal_receiver_status_interval = 1 detik  #Interval maksimum untuk node sekunder untuk melaporkan statusnya ke node utama
hot_standby_feedback = on          #Aktifkan node sekunder untuk melaporkan kesalahan selama replikasi.
```
13. Tekan **Esc** (Esc) dan masukkan **:wq** (:wq) untuk menyimpan file.
14. Jalankan perintah berikut untuk mengubah grup dan pemilik direktori data:
```
chown -R postgres.postgres /var/lib/pgsql/11/data
```
15. Jalankan perintah berikut untuk memulai layanan.
```
systemctl start postgresql-11
```
16. Jalankan perintah berikut untuk mengaktifkan layanan mulai otomatis.
```
systemctl enable postgresql-11
```

### Memverifikasi deployment
Lakukan hal berikut untuk memverifikasi deployment.
1. Jalankan perintah berikut untuk memeriksa proses `sender` pada node utama:
```
ps aux |grep receiver
```
Jika hasil berikut ditampilkan, ini menunjukkan bahwa proses `sender` tersedia.
![](https://main.qcloudimg.com/raw/d25daabc3d32c58237dd20d871e6852a.png)
2. Jalankan perintah berikut untuk memeriksa proses `receiver` pada node sekunder:
```
ps aux | grep receiver
```
Jika hasil berikut ditampilkan, ini menunjukkan bahwa proses `receiver` tersedia.
![](https://main.qcloudimg.com/raw/961283ed95a9640ba2121f5fafba2a7b.png)
3. Pada node utama, jalankan perintah berikut secara berurutan untuk memeriksa status node sekunder di terminal PostgreSQL.
```
su - postgres
```
```
psql
```
```
pilih * dari pg_stat_replication;
```
Jika hasil berikut ditampilkan, ini menunjukkan bahwa status node sekunder tersedia.
![](https://main.qcloudimg.com/raw/c85b5324929a4bffddd92c9dce906d56.png)
4. Verifikasi bahwa node sekunder menyinkronkan data dengan node utama.
 1. Pada node utama, jalankan perintah berikut untuk masuk ke terminal PostgreSQL dan membuat database (seperti `testdb`).
```
su - postgres
```
```
psql
```
```
buat database testdb;
```
 2. Pada node sekunder, jalankan perintah berikut secara berurutan untuk masuk ke terminal PostgreSQL dan periksa apakah node sekunder disinkronkan.
```
su - postgres
```
```
psql
```
```
"l",
```
Jika hasil berikut ditampilkan, ini menunjukkan bahwa node sekunder telah berhasil disinkronkan.
![](https://main.qcloudimg.com/raw/2912a3d9892665469bff1768c76c7ae9.png)




