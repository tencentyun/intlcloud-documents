CVM di Tencent Cloud VPC mendukung DHCP. Opsi DHCP yang dapat dikonfigurasi termasuk alamat DNS dan nama domain. Dokumen ini menjelaskan cara mengubah alamat DNS dan nama domain VPC.
>?
>+ Dynamic Host Configuration Protocol (DHCP) adalah protokol jaringan LAN yang mendefinisikan standar untuk mentransfer informasi konfigurasi ke server jaringan TCP/IP. 
>+ Untuk saat ini, VPC yang dibuat sebelum 1 April 2018 tidak mendukung fitur DHCP. Jika Anda tidak dapat mengubah alamat DNS dan nama domain di konsol, berarti VPC Anda tidak mendukung fitur ini.

## Catatan
Konfigurasi baru akan berlaku pada semua CVM di VPC.
 + Untuk CVM yang baru dibuat, konfigurasi yang dimodifikasi langsung berlaku.
 + Untuk CVM yang ada, konfigurasi yang dimodifikasi berlaku setelah CVM atau layanan jaringan dimulai ulang.

## Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih wilayah VPC di bagian atas halaman **VPC**.
3. Klik ID VPC untuk mengakses halaman **Basic Information** (Informasi Dasar).
4. Klik ikon edit untuk mengubah DNS dan nama domain masing-masing.
   + DNS: Alamat server DNS
     >?
     >+ DNS default Tencent Cloud adalah “183.60.83.19” dan “183.60.82.98”. Jika DNS default tidak digunakan, layanan internal seperti aktivasi Windows, NTP, dan YUM tidak akan tersedia.
     + DNS mendukung maksimal empat alamat IP. Pisahkan IP dengan koma. Perhatikan bahwa sistem operasi tertentu mungkin tidak dapat mendukung empat alamat DNS.
   + Nama Domain: Akhiran nama host CVM, seperti “example.com”. Anda dapat memasukkan hingga 60 karakter, atau tetap menggunakan konfigurasi default jika Anda tidak memiliki persyaratan khusus.
    ![](https://main.qcloudimg.com/raw/50129c5b14c7c6d5923263719eec5bd2.png)
