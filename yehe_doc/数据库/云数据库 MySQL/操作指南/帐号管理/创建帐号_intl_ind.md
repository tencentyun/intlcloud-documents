
## Ikhtisar
Selain akun root default yang dibuat oleh sistem, Anda dapat membuat akun bisnis lain di konsol TencentDB for MySQL berdasarkan kebutuhan aktual bisnis Anda.

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman manajemen instans.
2. Pada halaman manajemen instans, pilih **Database Management** (Manajemen Database)> **Account Management** (Manajemen Akun) dan klik **Create Account** (Buat Akun).
![](https://main.qcloudimg.com/raw/244439e05841ec094ff337ca56f845c1.png)
3. Pada jendela pop-up, masukkan nama akun, host, kata sandi, dan konfirmasi kata sandi, lalu klik **OK** (OKE).
 - **Account name** (Nama akun):
    - Nama akun di MySQL versi 5.5 dan 5.6 dapat berisi 1–16 huruf, angka, dan garis bawah (_) dan harus dimulai dengan huruf dan diakhiri dengan huruf atau angka.
    - Nama akun di MySQL versi 5.7 dan 8.0 dapat berisi 1-32 huruf, angka, dan garis bawah (_) dan harus dimulai dengan huruf dan diakhiri dengan huruf atau angka.
 - **Host** (Host): alamat host untuk akses database dapat berupa IP dan berisi `%` (menunjukkan untuk tidak membatasi rentang IP). Beberapa host harus dipisahkan oleh jeda baris, spasi, titik koma, koma, atau panel vertikal.
    - Contoh 1: masukkan `%` untuk menunjukkan tidak membatasi rentang IP, yaitu, klien di semua alamat IP diizinkan menggunakan akun ini untuk mengakses database.
    - Contoh 2: masukkan `10.5.10.%`, yang berarti bahwa klien yang rentang IP-nya dalam `10.5.10.%` diizinkan menggunakan akun ini untuk mengakses database.
 - **Password** (Kata Sandi): kata sandi harus berisi 8–64 karakter yang setidaknya dua jenis karakter berikut: huruf, angka, dan simbol khusus `\_+-&amp;=!@#$%^\*( )`.
 - **Connection Limit** (Batas Koneksi): jumlah koneksi untuk akun ini, yang tidak boleh lebih dari 10.240. Jika Anda tidak memasukkan nilai, tidak ada batasan yang akan diterapkan (tergantung pada jumlah koneksi maksimum).
4. Setelah berhasil dibuat, akun database dapat dikelola dalam daftar akun database dari instans saat ini.

## API Terkait

| Nama API                                                      | Deskripsi     |
| ------------------------------------------------------------ | -------- |
| [CreateAccounts](https://intl.cloud.tencent.com/document/product/236/17502) | Membuat akun TencentDB |


