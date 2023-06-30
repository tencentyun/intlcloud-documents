## Deskripsi Masalah
Saat Anda membuat namespace jaringan baru, perintah yang sesuai macet dan tidak dilanjutkan. Pesan Dmesg: "unregister_netdevice: menunggu lo menjadi gratis. Jumlah penggunaan = 1"

## Penyebab
Masalah ini disebabkan oleh bug di kernel. Versi kernel berikut memiliki bug ini:
- Versi kernel Ubuntu 16.04 x86_32: 4.4.0-92-generic.
- Versi kernel Ubuntu 16.04 x86_32: 4.4.0-92-generic.

## Solusi

Tingkatkan kernel ke versi 4.4.0-98-generic. Dalam versi ini, bug telah diperbaiki.

## Petunjuk
1. Jalankan perintah berikut untuk memeriksa versi kernel saat ini.

```
uname -r
```

2. Jalankan perintah berikut untuk memeriksa apakah versi 4.4.0-98-generic tersedia untuk peningkatan.

```
sudo apt-get update
sudo apt-cache search linux-image-4.4.0-98-generic
```

Jika informasi berikut ditampilkan, artinya versi ini ada di sumber dan tersedia untuk peningkatan. 

```
linux-image-4.4.0-98-generic - Gambar kernel Linux untuk versi 4.4.0 pada 64 bit x86 SMP
```

3. Jalankan perintah berikut untuk menginstal versi kernel baru dan paket Header yang sesuai.

```
sudo apt-get install linux-image-4.4.0-98-generic linux-headers-4.4.0-98-generic
```

4. Jalankan perintah berikut untuk memulai ulang sistem.

```
sudo reboot
```

5. Jalankan perintah berikut untuk masuk ke sistem untuk memeriksa versi kernel.

```
uname -r
```

Jika muncul hasil sebagai berikut, berarti peningkatan versi berhasil:

```
4.4.0-98-generic
```
