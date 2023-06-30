## Pengantar
Akun dan kata sandi CVM dapat digunakan sebagai kredensial untuk instans CVM. Artikel ini menjelaskan cara menggunakan dan mengelola kata sandi saat login ke instans CVM.

## Persyaratan Kata Sandi

Kata sandi harus memenuhi persyaratan ini:
- Kata sandi instans Linux: kata sandi harus terdiri dari 8 hingga 30 karakter. Sebaiknya gunakan kata sandi minimal 12 karakter. Kata sandi tidak boleh dimulai dengan `/` dan harus berisi setidaknya tiga hal berikut: (`a-z`, `A-Z`, `0-9`, dan simbol khusus ```()`~!@#$%^&*-+=_|{}[]:;'<>,.?/ ```).
- Kata sandi instans Windows: kata sandi harus terdiri dari 12 hingga 30 karakter. Kata sandi tidak boleh dimulai dengan `/` dan harus berisi setidaknya tiga hal berikut: (`a-z`, `A-Z`, `0-9`, dan simbol khusus ```()`~!@#$%^&*-+=_|{}[]:;'<>,.?/ ```), dan tidak boleh berisi nama pengguna Anda.

## Petunjuk

### Mengatur kata sandi awal
Ada dua cara untuk mengatur kata sandi awal, bergantung pada cara Anda mengonfigurasi instans CVM saat membelinya:
 - Jika Anda menggunakan opsi [**Konfigurasi Cepat**](https://buy.cloud.tencent.com/cvm?tab=custom&step=1&devPayMode=hourly&regionId=33&zoneId=330001&instanceType=SA2.SMALL1&platform=CentOS&bandwidthType=TRAFFIC_POSTPAID_BY_HOUR), kata sandi awal dikirimkan kepada Anda melalui email dan pesan ke konsol [Pusat Pesan](https://console.cloud.tencent.com/message).
 - Jika Anda menggunakan opsi [**Konfigurasi Kustom**](https://buy.cloud.tencent.com/cvm?tab=custom&step=1&devPayMode=hourly&regionId=33&zoneId=330001&instanceType=SA2.SMALL1&platform=CentOS&systemDiskType=CLOUD_PREMIUM&systemDiskSize=50&bandwidthType=TRAFFIC_POSTPAID_BY_HOUR&bandwidth=1), kata sandi awal diatur dengan cara berikut tergantung pada cara Anda memilih untuk login:
<table>
	<tr><th>Metode Login</th><th>Deskripsi</th></tr>
	<tr><td>Pembuatan kata sandi otomatis</td><td>Kata sandi awal dikirimkan kepada Anda melalui email dan konsol <a href="https://console.cloud.tencent.com/message">Pusat Pesan</a>.</td></tr>
	<tr><td>Kaitkan kunci sekarang</td><td><b>Dinonaktifkan secara default</b>. Anda login menggunakan nama pengguna dan kata sandi, namun kata sandi awal dikirimkan kepada Anda melalui email dan <a href="https://console.cloud.tencent.com/message">Pusat Pesan</a> konsol.</td></tr>
	<tr><td>Atur kata sandi</td><td>Anda mengatur kata sandi awal.</td></tr>
</table>


### Melihat kata sandi

Kata sandi login Anda dikirimkan kepada Anda melalui email dan konsol [Pusat Pesan](https://console.cloud.tencent.com/message). Berikut ini menjelaskan cara memeriksa pesan Anda di pusat pesan.
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/).
2. Klik <img src="https://main.qcloudimg.com/raw/f5d915ab4297418f3eae30fd28f41122.png" style="margin: 0;"></img> di sudut kanan atas dan pilih pesan produk yang sesuai, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/e3c624a805d2f5776807df44bd373b59.png)
Lihat kata sandi Anda di halaman pesan.
![](https://main.qcloudimg.com/raw/73bef8b11ded3d0cee5441d3d3218e25.png)

### Mengatur ulang kata sandi

Untuk petunjuk tentang cara mengatur ulang kata sandi Anda, lihat [Mengatur Ulang Kata Sandi Instans](http://intl.cloud.tencent.com/document/product/213/16566).
