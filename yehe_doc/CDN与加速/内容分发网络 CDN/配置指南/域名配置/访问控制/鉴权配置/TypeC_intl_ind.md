## Deskripsi Algoritme
**Format URL akses**
`http://DomainName/md5hash/timestamp/FileName`

**Deskripsi algoritme**
- timestamp (stempel waktu):Stempel waktu heksadesimal dalam format UNIX.
- md5hash:MD5 (kunci khusus + jalur file + stempel waktu).

**Sampel permintaan**
`http://cloud.tencent.com/8fe9b5597c809d7ace147468c7c7eadb/5e577978/test.jpg`

> !Saat nilai MD5 dihitung, jika jalur permintaan adalah `http://cloud.tencent.com/test.jpg`, jalur yang digunakan untuk penghitungan MD5 adalah `/test.jpg`.

## Panduan Konfigurasi
### Deskripsi parameter
TipeC memerlukan konfigurasi berikut:
![](https://main.qcloudimg.com/raw/d7b8d589f8690f1e4c33985d6bcd3f09.png)
**Custom Authentication Key** (Kunci Autentikasi Khusus): dapat berisi 6 hingga 40 angka, huruf besar dan huruf kecil.Kunci ini harus dirahasiakan dan diungkapkan hanya kepada klien dan server.
**Custom Validity Period** (Periode Validitas Khusus): nilai `timestamp` di jalur permintaan ditambah periode validitas yang dikonfigurasi dibandingkan dengan waktu saat ini untuk menentukan apakah permintaan telah kedaluwarsa; jika demikian, kesalahan 403 akan langsung dikembalikan.

### Objek
Setelah mengonfigurasi kunci, nama parameter, dan periode validitas, Anda dapat menentukan objek autentikasi sesuai kebutuhan.Tiga mode autentikasi berikut didukung:
![](https://main.qcloudimg.com/raw/34d27c8908808cacddfde94c8a3f1d81.png)
+ Semua file dengan nama domain yang ditentukan harus diautentikasi.
+ Semua file kecuali file dalam jenis yang ditentukan perlu diautentikasi.
+ Hanya file dalam jenis yang ditentukan yang perlu diautentikasi.

## Catatan:
**Hit rate cache**
Jika Anda telah mengaktifkan autentikasi TipeC untuk nama domain, tanda tangan dan stempel waktu akan dibawa di jalur URL akses.Saat simpul CDN meng-cache sumber daya, CDN akan secara otomatis mengabaikan jalur autentikasi tersebut dan dengan demikian tidak memengaruhi hit rate cache.
**Kebijakan tarik-asal**
Format akses nama domain dengan mode autentikasi TipeC yang diaktifkan adalah sebagai berikut:
`http://DomainName/md5hash/timestamp/FileName`

Jika tidak ada hit yang ditemukan pada simpul CDN setelah autentikasi berhasil, simpul akan memulai permintaan tarik-asal, **dengan `md5hash` dan `timestamp` akan dihapus dari jalur.** Server asal tidak memerlukan konfigurasi apa pun.
