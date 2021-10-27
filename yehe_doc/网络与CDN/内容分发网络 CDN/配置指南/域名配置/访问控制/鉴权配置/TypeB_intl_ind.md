## Deskripsi Algoritme
**Format URL akses**
`http://DomainName/timestamp/md5hash/FileName`

**Deskripsi algoritme**
- timestamp (stempel waktu):Stempel waktu dalam format `YYYYMMDDHHMM`.
- md5hash:MD5 (kunci khusus + stempel waktu + jalur file).

**Sampel permintaan**
`http://cloud.tencent.com/202003032017/b91bad39a0f9c885ddebd6b6164de3c4/test.jpg`

> !Saat nilai MD5 dihitung, jika jalur permintaan adalah `http://cloud.tencent.com/test.jpg`, jalur yang digunakan untuk penghitungan MD5 adalah `/test.jpg`.

## Panduan Konfigurasi

### Deskripsi parameter
TipeB memerlukan konfigurasi berikut:
![](https://main.qcloudimg.com/raw/d0cd00305ed4911a500995628bd45cfd.png)
**Custom Authentication Key** (Kunci Autentikasi Khusus): dapat berisi 6 hingga 40 angka, huruf besar dan huruf kecil.Kunci ini harus dirahasiakan dan diungkapkan hanya kepada klien dan server.
**Custom Validity Period** (Periode Validitas Khusus): nilai `timestamp` di jalur permintaan ditambah periode validitas yang dikonfigurasi dibandingkan dengan waktu saat ini untuk menentukan apakah permintaan telah kedaluwarsa; jika demikian, kesalahan 403 akan langsung dikembalikan.

### Objek
Setelah mengonfigurasi kunci, nama parameter, dan periode validitas, Anda dapat menentukan objek autentikasi sesuai kebutuhan.Tiga mode autentikasi berikut didukung:
![](https://main.qcloudimg.com/raw/13ccf23f34aaa9963e2ca36ea48b36f0.png)
- Semua file dengan nama domain yang ditentukan harus diautentikasi.
- Semua file kecuali file dalam jenis yang ditentukan perlu diautentikasi.
- Hanya file dalam jenis yang ditentukan yang perlu diautentikasi.

## Catatan:
**Hit rate cache**
Jika Anda telah mengaktifkan autentikasi TipeB untuk nama domain, tanda tangan dan stempel waktu akan dibawa di jalur URL akses.Saat simpul CDN meng-cache sumber daya, CDN akan secara otomatis mengabaikan bidang di jalur tersebut dan dengan demikian tidak memengaruhi hit rate cache.
**Kebijakan tarik-asal**
Format akses nama domain dengan mode autentikasi TipeB yang diaktifkan adalah sebagai berikut:
`http://DomainName/timestamp/md5hash/FileName`

Jika tidak ada hit yang ditemukan pada simpul CDN setelah autentikasi berhasil, simpul akan memulai permintaan tarik-asal, **dengan `md5hash` dan `timestamp` akan dihapus dari jalur.** Server asal tidak memerlukan konfigurasi apa pun.

