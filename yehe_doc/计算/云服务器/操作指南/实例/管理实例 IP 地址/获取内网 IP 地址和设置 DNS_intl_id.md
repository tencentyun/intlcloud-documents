Dokumen ini menjelaskan cara mendapatkan alamat IP pribadi dari instans dan mengonfigurasi DNS pribadi.

## Mendapatkan alamat IP pribadi dari instans
### Mendapatkan alamat IP pribadi di konsol
1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/).
2. Pada halaman manajemen instans, pilih instans dan gerakkan mouse ke kolom **Primary IP** (IP Primer) untuk melihat IP pribadinya, dan klik <img src = "https://main.qcloudimg.com/raw/6603ab4f907562addb1c01596c6296cd.png" style = "margin: 0;"> untuk menyalin IP pribadi, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/f4849355a4890861e2d07b35de1099a4.png)

### Mendapatkan alamat IP pribadi menggunakan API
Harap Lihat [DescribeInstances API](https://intl.cloud.tencent.com/document/product/213/33258).

### Mendapatkan alamat IP pribadi menggunakan metadata instans

1. Login ke CVM.
2. Akses metadata instans dengan menggunakan alat cURL atau permintaan HTTP GET.
> Operasi berikut menggunakan alat cURL sebagai contoh.
>
Jalankan perintah berikut untuk mendapatkan IP pribadi.
```
curl http://metadata.tencentyun.com/meta-data/local-ipv4
```
Informasi yang dikembalikan adalah alamat IP pribadi, seperti yang ditunjukkan di bawah ini:
![](https://mc.qcloudimg.com/static/img/14a13eccebc7eee6f83bc026adb30902/image.png)

Untuk informasi selengkapnya tentang metadata instans, lihat [Metadata Instans](http://intl.cloud.tencent.com/document/product/213/4934).

## Mengonfigurasi DNS jaringan pribadi 
Ketika terjadi kesalahan resolusi jaringan, Anda dapat mengonfigurasi DNS jaringan pribadi secara manual berdasarkan sistem operasi CVM Anda.

### Untuk sistem operasi Linux

1. Login ke CVM Linux.
2. Jalankan perintah berikut untuk membuka file `/etc/resolv.conf`.
```
vi /etc/resolv.conf
```
3. Tekan **i** (i) untuk beralih ke mode edit, dan ubah IP DNS sesuai dengan wilayah terkait dalam daftar [DNS Jaringan Pribadi](https://intl.cloud.tencent.com/document/product/213/5225).
Misalnya, untuk mengubah IP DNS jaringan pribadi menjadi server DNS jaringan pribadi di wilayah Beijing.
```
server nama 10.53.216.182
server nama 10.53.216.198
batas waktu opsi: 1 putar
```
4. Tekan **Esc** (Esc), masukkan **:wq** (:wq), simpan file dan kembalikan.

### Untuk sistem operasi Windows

1. Login ke CVM Windows.
2. Pada antarmuka sistem operasi, buka **Control Panel** (Panel Kontrol) > **Network and Sharing Center** (Pusat Jaringan dan Berbagi) > **Change adapter settings** (Ubah pengaturan adaptor).
3. Klik kanan **Ethernet** (Ethernet) dan pilih **Properties** (Properti) untuk membuka jendela “Ethernet Properties” (Properti Ethernet).
4. Di jendela “Ethernet Properties” (Properti Ethernet), klik dua kali **IP version 4 (TCP/IPv4)** (IP versi 4 (TCP/IPv4)), seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/1eef10b5919ba4db272fa0fc21fb1702.png)
5. Pilih [Gunakan alamat server DNS berikut] dan ubah IP DNS sesuai dengan wilayah yang sesuai dalam daftar [DNS Jaringan Pribadi](https://intl.cloud.tencent.com/document/product/213/5225).

6. Klik **OK** (OKE).
