## Deskripsi Kesalahan
Kesalahan “Account locked due to XXX failed logins” (Akun terkunci karena XXX gagal login) muncul sebelum saya memasukkan kata sandi login.
![](https://main.qcloudimg.com/raw/0dcc0c3b62a36ba0f269e629a3365564.png)

## Kemungkinan Alasan
Masalah ini mungkin disebabkan oleh konfigurasi `pam_tally2.so` di file `/etc/pam.d/login`. Untuk login VNC, `/etc/pam.d/login` dipanggil untuk autentikasi, sementara `pam_tally2.so` menunjukkan untuk secara otomatis mengunci akun pengguna sementara atau permanen setelah gagal login berturut-turut sesuai jumlah yang ditentukan. Saat akun terkunci secara permanen, Anda harus membukanya secara manual.

Akun login akan dikunci ketika jumlah login gagal berturut-turut melebihi nilai yang dikonfigurasi. Perhatikan bahwa akun juga dapat dikunci untuk serangan brute force.
![](https://main.qcloudimg.com/raw/806c1d8ccded0746f5457320df479177.png)
Lihat di bawah untuk parameter modul `pam_tally2`.
<table>
<tr>
<th>Parameter</th><th>Deskripsi</th>
</tr>
<tr>
<td><code>deny=n</code></td>
<td>Kunci akun jika jumlah login gagal berturut-turut melebihi <code>n</code>.</td>
</tr>
<tr>
<td><code>lock_time=n </code></td>
<td>Kunci akun selama <code>n</code> detik jika jumlah login gagal berturut-turut melebihi batas</td>
</tr>
<tr>
<td><code>un lock_time=n</code></td>
<td>Buka kunci akun secara otomatis <code>n</code> detik kemudian</td>
</tr>
<tr>
<td><code>no_lock_time </code></td>
<td>Jangan gunakan bidang <code>.fail_locktime</code> di <code>/var/log/faillog</code></td>
</tr>
<tr>
<td><code>magic_root   </code></td>
<td>Jika modul dipanggil oleh pengguna root (uid=0), penghitung tidak bertambah.</td>
</tr>
<tr>
<td><code>even_deny_root </code></td>
<td>Pengguna root akan dikunci setelah <code>deny=n</code> login gagal berturut-turut.</td>
</tr>
<tr>
<td><code>root_unlock_time=n  </code></td>
<td>Parameter ini diperlukan jika <code>even_deny_root</code> dikonfigurasi. Ini menunjukkan berapa lama pengguna root terkunci ketika jumlah login gagal berturut-turut melebihi batas. </td>
</tr>
</table>

## Solusi
1. Lihat [prosedur pemecahan masalah](#ProcessingSteps) untuk mengakses file konfigurasi login dan untuk sementara mengomentari konfigurasi modul `pam_limits.so`.
2. Cari alasan mengapa akun Anda dikunci, dan tingkatkan kebijakan keamanan Anda.

[](id:ProcessingSteps)

## Prosedur Pemecahan Masalah

1. Coba [login ke CVM Linux melalui kunci SSH](https://intl.cloud.tencent.com/document/product/213/32501).
	- Jika login berhasil, lanjutkan ke langkah berikutnya.
	- Jika login gagal, coba mode pengguna tunggal.
2. Jalankan perintah berikut untuk melihat log.
```
vim /var/log/secure
```
File ini mencatat informasi keamanan, sebagian besar log login CVM. Anda dapat memeriksa log kesalahan `pam_tally2` seperti yang ditunjukkan di bawah ini.
![](https://main.qcloudimg.com/raw/f45fb4564cfea44f0210a6e9b7124b73.png)
3. Jalankan perintah berikut secara berurutan untuk membuka direktori `/etc/pam.d` dan mencari `pam_tally2`.
```
cd /etc/pam.d
```
```
find . | xargs grep -ri "pam_tally2" -l
```
Jika hasil yang mirip dengan gambar berikut dikembalikan, `pam_tally2` disertakan dalam file `login`.
![](https://main.qcloudimg.com/raw/a5d272e11a88d4f9cee347244fb98441.png)
4. Jalankan perintah berikut untuk mengomentari sementara konfigurasi `pam_tally2.so`. Kemudian Anda dapat login secara normal.
```
sed -i "s/.*pam_tally.*/#&/" /etc/pam.d/login
```
5. Periksa apakah akun terkunci karena kesalahan operasi atau serangan brute force. Dalam kasus selanjutnya, sebaiknya Anda memperkuat kebijakan keamanan sebagai berikut:
 - Ubah kata sandi CVM menjadi kata sandi yang lebih kuat yang berisi 12-16 karakter, yang menyertakan huruf besar, huruf kecil, karakter khusus, dan angka. Untuk informasi selengkapnya, lihat [Mengatur Ulang Kata Sandi Instans](https://intl.cloud.tencent.com/document/product/213/16566).
 - Hapus akun login CVM yang tidak digunakan.
 - Ubah port ssh default 22 ke port yang kurang umum antara 1024-65525. Untuk informasi selengkapnya, lihat [Mengubah Port Jarak Jauh Default pada CVM](https://intl.cloud.tencent.com/document/product/213/35376).
 - Kelola aturan grup keamanan terkait untuk hanya membuka port dan protokol yang diperlukan oleh bisnis Anda. Untuk informasi selengkapnya, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272).
 - Tutup port untuk akses internet untuk aplikasi inti seperti database MySQL dan Redis. 
 - Instal perangkat lunak keamanan (seperti agen CWP), dan konfigurasikan alarm secara real time untuk mendapat pemberitahuan tentang login yang mencurigakan sesegera mungkin.


