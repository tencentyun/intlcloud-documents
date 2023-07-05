## Skenario
Dokumen ini menjelaskan cara mendapatkan alamat IP publik melalui konsol, API, atau metadata Instans.


## Petunjuk

### Mendapatkan alamat IP publik di konsol
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/).
2. Pada halaman manajemen instans, gerakkan mouse ke kolom IP utama, dan <img src = "https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style = "margin: 0;"> </ img> akan muncul, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/952664b0a70077ba49a031b98a57c782.png)
3. Klik <img src="https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style="margin: 0;"> untuk menyalin alamat IP.	
>! Alamat IP publik dipetakan ke alamat IP pribadi melalui NAT. Jika Anda melihat atribut antarmuka jaringan dari dalam instans (misalnya dengan menggunakan perintah seperti `ifconfig (Linux)` atau `ipconfig (Windows)`), alamat IP publik tidak ditampilkan. Untuk mendapatkan IP publik dari dalam instans, lihat [Memperoleh Alamat IP Publik Instans Menggunakan Metadata Instans](#jump).
>

### Mendapatkan alamat IP publik dengan menggunakan API
Harap lihat [DescribeInstances](https://intl.cloud.tencent.com/document/product/213/33258).

<span id = "jump">  </span>
### Mendapatkan alamat IP publik menggunakan metadata instans
1. Login ke instans CVM.
Untuk informasi selengkapnya, lihat [Log in ke Instans Linux](https://intl.cloud.tencent.com/document/product/213/5436) dan [Login ke Instans Windows](https://intl.cloud.tencent.com/document/product/213/5435).
2. Untuk mendapatkan alamat IP publik, Anda dapat mengakses metadata dengan menggunakan alat cURL atau permintaan HTTP GET.
```
curl http://metadata.tencentyun.com/meta-data/public-ipv4
```
Jika nilai yang ditampilkan dalam struktur berikut, Anda dapat melihat alamat IP publik:
![](https://main.qcloudimg.com/raw/03f603e433b7a5da09e33a8b09d731b4.png)
Untuk informasi selengkapnya, lihat [Metadata Instans](http://intl.cloud.tencent.com/document/product/213/4934).
