Metadata instans mengacu pada data yang relevan dengan sebuah instans. Metadata ini dapat digunakan untuk mengonfigurasi atau mengelola instans yang sedang berjalan.
>? Meskipun metadata instans hanya dapat diakses setelah login, data belum dienkripsi. Siapa pun yang mengakses instans dapat melihat metadatanya. Dengan demikian, Anda harus mengambil tindakan yang tepat untuk melindungi data sensitif.
>


## Ikhtisar
Tencent Cloud menyediakan metadata berikut:

<table>
<thead>
<tr>
<th>Nama</th>
<th width="50%">Deskripsi</th>
<th width="15%">Versi</th>
</tr>
</thead>
<tbody><tr>
<td>instance-id</td>
<td>ID Instans</td>
<td>1.0</td>
</tr>
<tr>
<td>instance-name</td>
<td>Nama instans</td>
<td>1.0</td>
</tr>
<tr>
<td>uuid</td>
<td>ID instans unik</td>
<td>1.0</td>
</tr>
<tr>
<td>local-ipv4</td>
<td>Alamat IP pribadi instans</td>
<td>1.0</td>
</tr>
<tr>
<td>public-ipv4</td>
<td>Alamat IP publik instans</td>
<td>1.0</td>
</tr>
<tr>
<td>mac</td>
<td>Alamat MAC perangkat eth0 instans</td>
<td>1.0</td>
</tr>
<tr>
<td>penempatan/wilayah</td>
<td>Wilayah instans</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>penempatan/zona</td>
<td>Zona ketersediaan instans</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/mac</td>
<td>Alamat MAC dari antarmuka jaringan instans</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/primary-local-ipv4</td>
<td>IP pribadi utama dari antarmuka jaringan instans</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/public-ipv4s</td>
<td>Alamat IP publik dari antarmuka jaringan instans</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/vpc-id</td>
<td>ID VPC dari antarmuka jaringan instans</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/subnet-id</td>
<td>ID Subnet dari antarmuka jaringan instans</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/gateway</td>
<td>Alamat gateway antarmuka jaringan instans</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/local-ipv4</td>
<td>Alamat IP pribadi dari antarmuka jaringan instans</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/public-ipv4</td>
<td>Alamat IP publik dari antarmuka jaringan instans</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/public-ipv4-mode</td>
<td>Mode jaringan publik dari antarmuka jaringan instans</td>
<td>1.0</td>
</tr>
<tr>
<td>network/interfaces/macs/<strong>${mac}</strong>/local-ipv4s/<strong>${local-ipv4}</strong>/subnet-mask</td>
<td>Subnet mask dari antarmuka jaringan instans</td>
<td>1.0</td>
</tr>
<tr>
<td>pembayaran/jenis tagihan</td>
<td>Paket penagihan instans</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>pembayaran/waktu pembuatan</td>
<td>Waktu pembuatan instans</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>pembayaran/waktu penghentian</td>
<td>Waktu penghentian instans</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>app-id</td>
<td>AppID dari pemilik instans</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>as-group-id</td>
<td>ID grup penskalaan otomatis dari instans</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>spot/waktu penghentian</td>
<td>Spot waktu penghentian instans</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>/meta-data/instans/instans-type</td>
<td>Jenis instans</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>/instans/image-id</td>
<td>ID citra instans</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>/instance/security-group</td>
<td>Informasi grup keamanan yang terikat pada instans</td>
<td>2017-09-19</td>
</tr>
<tr>
<td>/instans/bandwidth-limit-egress</td>
<td>Batas bandwidth keluar jaringan pribadi instans, dalam Kbit/d</td>
<td>2019-09-29</td>
</tr>
<tr>
<td>/instance/bandwidth-limit-ingress</td>
<td>Batas bandwidth masuk jaringan pribadi instans, dalam Kbit/d</td>
<td>2019-09-29</td>
</tr>
<tr>
<td>/cam/security-credentials/${role-name}</td>
<td>Kredensial sementara yang dibuat oleh kebijakan peran CAM, yang hanya dapat diperoleh jika instans dikaitkan dengan peran CAM. Ubah `${role-name}` menjadi nama peran CAM yang sebenarnya; jika tidak, `404` akan ditampilkan</td>
<td>2019-12-11</td>
</tr>
</tbody></table>

>? 
>- Bidang `${mac}` dan `${local-ipv4}` pada tabel di atas menunjukkan alamat MAC dan alamat IP pribadi dari antarmuka jaringan yang ditentukan untuk masing-masing instans.
>- Alamat URL tujuan permintaan peka huruf besar/kecil. Anda harus membuat alamat URL tujuan permintaan baru sesuai dengan hasil permintaan yang ditampilkan.
>- Data `penempatan` yang ditampilkan diubah dalam versi baru. Untuk menggunakan data di versi sebelumnya, tentukan jalur versi sebelumnya atau biarkan jalur versi kosong untuk mengakses data versi 1.0. Untuk informasi selengkapnya tentang data `penempatan` yang ditampilkan, lihat [Wilayah dan Zona Ketersediaan](https://intl.cloud.tencent.com/document/product/213/6091).

## Mengkueri Metadata Instans
Setelah login ke instans, Anda dapat mengakses metadata seperti alamat IP lokal dan alamat IP publik untuk mengelola koneksi dengan aplikasi eksternal.
Untuk melihat semua metadata instans dalam instans yang sedang berjalan, gunakan URI berikut:

```
http://metadata.tencentyun.com/latest/meta-data/
```
Anda dapat mengakses metadata dengan menggunakan alat cURL atau permintaan HTTP GET, misalnya:

```
curl http://metadata.tencentyun.com/latest/meta-data/
```
* Untuk sumber daya yang tidak ada, kode kesalahan HTTP "404 - Not Found" (404 - Tidak Ditemukan) akan ditampilkan.
* Untuk mengoperasikan metadata instans, silakan login ke instans terlebih dahulu. Untuk informasi selengkapnya, lihat [Login ke Instans Windows Menggunakan RDP (Direkomendasikan)(https://intl.cloud.tencent.com/document/product/213/5435) dan [Login ke Instans Linux Menggunakan Metode Login Standar](https://intl.cloud.tencent.com/document/product/213/5436).

### Contoh kueri metadata

Contoh berikut menunjukkan cara mendapatkan versi metadata.
>! Saat Tencent Cloud memodifikasi jalur akses metadata atau data yang ditampilkan, versi metadata baru akan dirilis. Jika aplikasi atau skrip Anda bergantung pada struktur atau data yang dikembalikan dari versi sebelumnya, Anda dapat mengakses metadata menggunakan versi sebelumnya yang ditentukan. Jika tidak ada versi yang ditentukan, versi 1.0 diakses secara default.
>

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/
1.0
2017-09-19
terbaru
meta-data
```

Contoh berikut menunjukkan cara melihat direktori root metadata. Baris yang diakhiri dengan `/` mewakili direktori dan baris lainnya mewakili data yang diakses. Untuk deskripsi data yang diakses, lihat bagian **Overview** (Ikhtisar) yang dijelaskan di atas.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/
instance-id
instance-name
local-ipv4
mac
network/
placement/
public-ipv4
uuid
```

Contoh berikut menunjukkan cara mendapatkan informasi lokasi fisik dari instans. Untuk hubungan antara data yang dikembalikan dan lokasi fisik, lihat [Wilayah dan Zona Ketersediaan](https://intl.cloud.tencent.com/document/product/213/6091).

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/placement/region
ap-guangzhou

[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/placement/zone
ap-guangzhou-3
```

Contoh berikut menunjukkan cara mendapatkan alamat IP pribadi instans. Jika instans memiliki beberapa ENI, alamat jaringan perangkat eth0 akan ditampilkan.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/local-ipv4
10.104.13.59
```

Contoh berikut menunjukkan cara mendapatkan alamat IP publik instans.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/public-ipv4
139.199.11.29
```

Contoh berikut menunjukkan cara mendapatkan ID instans. ID instans digunakan untuk mengidentifikasi instans secara unik.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/instance-id
ins-3g445roi
```

Contoh berikut menunjukkan cara mengkueri instans UUID. UUID instans juga dapat digunakan sebagai pengidentifikasi unik instans, tetapi sebaiknya gunakan ID instans untuk mengidentifikasi instans.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/uuid
cfac763a-7094-446b-a8a9-b995e638471a
```

Contoh berikut menunjukkan cara mendapatkan alamat MAC perangkat eth0 instans.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/mac
52:54:00:BF:B3:51
```

Contoh berikut menunjukkan cara mendapatkan informasi ENI instans. Dalam kasus beberapa ENI, beberapa baris data ditampilkan, dengan setiap baris menunjukkan direktori data dari ENI.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/
52:54:00:BF:B3:51/
```

Contoh berikut menunjukkan cara mendapatkan informasi dari ENI tertentu.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/
local-ipv4s/
mac
vpc-id
subnet-id
owner-id
primary-local-ipv4
public-ipv4s
local-ipv4s/
```

Contoh berikut menunjukkan cara mendapatkan informasi VPC dari ENI tertentu.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/vpc-id
vpc-ja82n9op

[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/subnet-id
subnet-ja82n9op
```

Contoh berikut menunjukkan cara mendapatkan daftar alamat IP pribadi yang terikat ke ENI yang ditentukan. Jika ENI terikat dengan beberapa alamat IP pribadi, beberapa baris data akan ditampilkan.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/
10.104.13.59/
```

Contoh berikut menunjukkan cara mendapatkan informasi alamat IP pribadi.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59
gateway
local-ipv4
public-ipv4
public-ipv4-mode
subnet-mask
```

Contoh berikut menunjukkan cara mendapatkan gateway alamat IP pribadi. Data ini hanya tersedia untuk model CVM berbasis VPC. Untuk informasi selengkapnya, harap lihat [Virtual Private Cloud (VPC)](https://intl.cloud.tencent.com/document/product/215).

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/gateway
10.15.1.1
```

Contoh berikut menunjukkan cara mendapatkan mode akses yang digunakan oleh alamat IP pribadi untuk mengakses jaringan publik. Data ini hanya dapat dikueri untuk CVM berbasis VPC. CVM berbasis jaringan klasik mengakses jaringan publik melalui gateway publik.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/public-ipv4-mode
NAT
```

Contoh berikut menunjukkan cara mendapatkan alamat IP publik yang terikat ke alamat IP pribadi.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/public-ipv4
139.199.11.29
```

Contoh berikut menunjukkan cara mendapatkan subnet mask dari alamat IP pribadi.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/network/interfaces/macs/52:54:00:BF:B3:51/local-ipv4s/10.104.13.59/subnet-mask
255.255.192.0
```

Contoh berikut menunjukkan cara mendapatkan jenis penagihan instans.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/charge-type
POSTPAID_BY_HOUR
```

Contoh berikut menunjukkan cara mendapatkan waktu pembuatan instans.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/payment/create-time
2018-09-18 11:27:33
```


Contoh berikut menunjukkan cara mendapatkan waktu penghentian untuk instans spot.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/spot/termination-time
2018-08-18 12:05:33
```

Contoh berikut menunjukkan cara mendapatkan AppId akun tempat CVM berada.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/app-id
123456789
```

Contoh berikut menunjukkan cara mendapatkan kredensial sementara yang dihasilkan oleh peran CAM yang menjadi milik instans. Dalam contoh ini, nama peran adalah `CVMas`.
```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/meta-data/cam/security-credentials/CVMas
{
  "TmpSecretId": "AKIDoQMxF8OPg0gA7pyZIA6cW447p225cIt9NW8dhA1dwl5UvxxxxxxxxxUqRlEb5_",
  "TmpSecretKey": "Q9z24VucjF4xQQNV64qwF6uWY71PEsH3exxxxxxxxxgA=",
  "ExpiredTime": 1615590047,
  "Expiration": "2021-03-12T23:00:47Z",
  "Token": "xxxxxxxxxxx",
  "Code": "Success"
}
```

## Mengkueri Data Pengguna Instans
Anda dapat menentukan data pengguna instans saat membuat instans. Instans CVM yang memiliki konfigurasi cloud-init dapat mengakses data.

### Mencari data pengguna
Setelah login, Anda dapat mengakses data pengguna dengan menggunakan metode berikut.

```shell
[qcloud-user]# curl http://metadata.tencentyun.com/latest/user-data
179, klien, shanghai
```
