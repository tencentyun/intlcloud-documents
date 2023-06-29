## Deskripsi Algoritme
**Format URL akses**
`http://DomainName/FileName?sign=md5hash&t=timestamp`

**Deskripsi algoritme**
- `timestamp`: stempel waktu desimal atau heksadesimal dalam format UNIX.
- `md5hash`:MD5 (kunci khusus + jalur file + stempel waktu).

**Sampel permintaan**
`http://cloud.tenloud.tencent.com/test.jpg?sign=0f8201d814dfaf64cf54e74c5f7dbcb0&t=1582791032`

> !Saat nilai MD5 dihitung, jika jalur permintaan adalah `http://cloud.tencent.com/test.jpg`, jalur yang digunakan untuk penghitungan MD5 adalah `/test.jpg`.

## Panduan Konfigurasi
### Deskripsi Parameter
TipeD memerlukan konfigurasi berikut:
![](https://main.qcloudimg.com/raw/6caae33f26a263699003ccb2e4e562c5.png)
**Custom authentication key** (Kunci autentikasi khusus): berisi 6 hingga 40 angka, huruf besar dan huruf kecil.Kunci harus dirahasiakan dan hanya diketahui oleh klien dan server.
**Custom authentication parameter name and timestamp parameter name** (Nama parameter autentikasi khusus dan nama parameter stempel waktu): `sign` dalam contoh dapat diganti dengan nama parameter yang berisi 1 hingga 100 huruf besar dan kecil, angka, dan garis bawah.Setelah CDN menerima permintaan, CDN akan membaca nilai parameter tanda tangan yang ditentukan dan menghitung nilai MD5.Jika hasilnya cocok dengan nilai `md5hash` yang diteruskan, tanda tangan akan berhasil diverifikasi.Jika tidak, kesalahan 403 akan langsung dikembalikan.
**Custom validity period** (Periode validitas khusus): nilai `timestamp` dalam parameter stempel waktu, ditambah periode validitas yang dikonfigurasi, dibandingkan dengan waktu saat ini untuk menentukan apakah permintaan telah kedaluwarsa.Jika ya, kesalahan 403 akan langsung dikembalikan.Periode validitas dalam hitungan detik.

### Objek
Setelah mengonfigurasi kunci, nama parameter, dan periode validitas, Anda dapat menentukan objek autentikasi sesuai kebutuhan.Tiga mode autentikasi berikut didukung:
![](https://main.qcloudimg.com/raw/8a9b8c36cfc91a31cf96b31f0e6553c2.png)

+ Semua file dengan nama domain yang ditentukan harus diautentikasi.
+ Semua file kecuali file dalam jenis yang ditentukan perlu diautentikasi.
+ Hanya file dalam jenis yang ditentukan yang perlu diautentikasi.

## Catatan
**Hit rate cache**
Jika Anda telah mengaktifkan mode autentikasi TipeD untuk nama domain, URL akses akan membawa parameter autentikasi.Saat simpul CDN meng-cache sumber daya, CDN akan secara otomatis mengabaikan parameter yang sesuai dan dengan demikian tidak akan memengaruhi hit rate cache.
>!Karena parameter yang sesuai akan diabaikan secara otomatis setelah konfigurasi, yaitu, parameter autentikasi dan stempel waktu yang dikonfigurasi akan difilter, kunci cache dari file yang akan diautentikasi akan terpengaruh, dan prioritas di sini lebih tinggi daripada aturan kunci cache di **Cache Configuration** -> **Cache Key Rule Configuration** (Konfigurasi Cache -> Konfigurasi Aturan Kunci Cache).
Misalnya, konfigurasi TipeD di sini adalah sebagai berikut:"Authentication Parameter: `sigh`"; "Timestamp Parameter: `t`"; "Authentication Scope: `jpg`"; maka parameter `sign` dan `t` akan otomatis difilter untuk file JPG meskipun konfigurasinya adalah "All Files:Do Not Filter" dalam **Cache Configuration** -> **Cache Key Rule Configuration** (Konfigurasi Cache -> Konfigurasi Aturan Kunci Cache).

**Kebijakan tarik-asal**
Format akses nama domain dengan mode autentikasi TipeD yang diaktifkan adalah sebagai berikut:
`http://DomainName/FileName?sign=md5hash&t=timestamp`

Jika simpul CDN tidak terkena hit setelah autentikasi berhasil, simpul tersebut akan memulai permintaan tarik-asal, **yang dalam format yang sama dengan permintaan akses dengan parameter `sign/t` dipertahankan**.Server asal dapat mengabaikannya atau melakukan autentikasi lagi jika dibutuhkan.
