## Skenario

Dokumen ini menjelaskan cara login ke instans Windows melalui desktop jarak jauh di komputer lokal.

## OS yang Berlaku

Windows

## Prasyarat

- Anda harus sudah memiliki akun/kata sandi admin untuk login ke instans Windows dari jarak jauh.
 - Jika Anda menggunakan kata sandi default sistem untuk login ke instans, dapatkan dengan membuka [Pesan Internal](https://console.cloud.tencent.com/message).
 Jika Anda lupa kata sandi, [atur ulang kata sandi instans](https://intl.cloud.tencent.com/document/product/213/16566).
- IP publik telah dibeli untuk instans CVM Anda, dan port 3389 terbuka (jika CVM dibeli dengan “Konfigurasi Cepat”, port ini terbuka secara default.)

## Langkah-Langkah
>? Langkah-langkah berikut mengambil sistem operasi Windows 7 sebagai contoh.
>
1. Di komputer Windows lokal, klik <img src="https://main.qcloudimg.com/raw/370daffec54024ee262d1e5dbcd4bde2.png" style="margin: 0;width: 35px;">, dan masukkan **mstsc** (mstsc) di **Search program and files** (Cari program dan file), lalu tekan **Enter** (Enter) untuk membuka kotak dialog koneksi desktop jarak jauh, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/d8a4b0f70f876f6c0edc6e995a02c37d.png)
2. Masukkan IP publik server Windows setelah **Computer** (Komputer), lalu klik **Connect** (Hubungkan).
Untuk informasi selengkapnya tentang cara mendapatkan IP publik, lihat [Mendapatkan Alamat IP Publik](https://intl.cloud.tencent.com/document/product/213/17940).
3. Masukkan akun/kata sandi admin instans di jendela pop-up **Windows Security** (Keamanan Windows), seperti yang ditunjukkan di bawah ini:
> Jika kotak dialog **Do you trust this remote connection?** (Apakah Anda percaya koneksi jarak jauh ini?) muncul, Anda dapat mencentang **Don’t ask me again for this connection to this computer** (Jangan tanya saya lagi untuk koneksi ke komputer ini), lalu klik **Connect** (Hubungkan).

![](https://main.qcloudimg.com/raw/5d3d89e3ec4616a367b80ba377a3f541.png)
4. Klik **OK** (OKE) untuk login ke instans CVM Windows.

