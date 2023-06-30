### Bagaimana cara mengonfigurasi iptables perangkat lunak firewall pada OS Linux?
> **Catatan:**
> iptables sangat berbeda antara versi sebelum CentOS 7 dan yang lebih baru.
> - Dalam versi sebelum CentOS 7, layanan iptables digunakan sebagai firewall secara default. Setelah menjalankan perintah `service iptables stop`, pertama-tama layanan iptables akan menghapus aturan dan kemudian membongkar modul iptables. Ketika layanan iptables dimulai ulang, layanan ini akan memuat aturan dari file konfigurasi. Anda dapat menghentikan layanan iptables untuk menguji apakah pembatasan firewall sudah diterapkan.
>[](https://main.qcloudimg.com/raw/4a404e0187b0ee677034c0df82468e4a.png)
> - Dalam versi yang lebih baru dari CentOS 7, layanan firewall digunakan sebagai firewall secara default, dan modul iptables_filter dimuat untuk memastikan kompatibilitas. Anda dapat menggunakan perintah iptables untuk menambahkan aturan. Meski demikian, layanan iptables dinonaktifkan secara default. Setelah Anda mengonfirmasi bahwa modul iptable_filter sudah dimuat, aturan akan berlaku.

Untuk menentukan firewall, jalankan `iptables -nvL` untuk melihat aturan. 
Dua skenario berikut menjelaskan cara mengonfigurasi program perangkat lunak firewall iptables. 
#### Skenario 1
Di OS Ubuntu 14, grup keamanan dan port mendengarkan diaktifkan, tapi koneksi Telnet gagal.
Aturan masuk grup keamanan:
![](https://main.qcloudimg.com/raw/4a6a1c7eca94a76ddbce457dbe28affa.png)
Aturan keluar grup keamanan:
![](https://main.qcloudimg.com/raw/90914e729ba27a6a9253e719bf4a9703.png)
Kegagalan koneksi telnet:
![](https://main.qcloudimg.com/raw/74c521a97d4b9dab64b85ce62ab2cf86.png)
#### Solusi
1. Tangkap paket pada CVM untuk memeriksa apakah paket dikirim ke CVM.
 - Jika tidak, paket mungkin diblokir oleh grup keamanan, TGW atas, atau ISP.
 - Jika ya tetapi CVM tidak menanggapi, masalah ini mungkin disebabkan oleh kebijakan iptables dari CVM. Seperti yang ditunjukkan pada gambar berikut, CVM tidak mengembalikan paket TCP ke 64.11 setelah koneksi Telnet dibuat.
![](https://main.qcloudimg.com/raw/1052893022c8786a9b7b0166a57ce16d.png)  

2. Setelah mengonfirmasi bahwa masalah disebabkan oleh kebijakan iptables, jalankan `iptables –nvL` untuk memeriksa apakah kebijakan membuka port 8081. Dalam contoh ini, port 8081 ditutup. 
![](https://main.qcloudimg.com/raw/f214d470f1d40ed7061ea155de756bca.jpg) 
3. Jalankan perintah berikut untuk membuka port 8081:
```
iptables -I INPUT 5 -p tcp --dport 8081 -j ACCEPT
```
4. Periksa apakah port 8081 dibuka. Jika ya, maka masalah sudah terpecahkan.  


#### Skenario 2
Berdasarkan konfigurasi iptables, kebijakan telah diaktifkan, tetapi server tujuan masih tidak dapat di-ping.
![](https://main.qcloudimg.com/raw/46fdf4e20187c5b366c7773d73eb1cee.png)
#### Solusi
Jika informasi yang ditunjukkan di bawah ini sudah muncul,
![](https://main.qcloudimg.com/raw/babfa7fcfe9dd7536ba011c3fbaab7bc.jpg)
jalankan perintah berikut untuk menghapus aturan output pertama:
```
iptabels –D OUTPUT 1
```
Uji untuk memverifikasi bahwa masalah sudah dipecahkan.

### Bagaimana cara menghapus firewall?
#### Instans Windows:
1. Setelah masuk ke instans, pilih **Start** (Mulai) > **Control Panel** (Panel Kontrol) > **Firewall Settings** (Pengaturan Firewall) untuk mengakses halaman "Firewall Settings" (Pengaturan Firewall).

2. Periksa apakah firewall dan perangkat lunak keamanan lainnya, seperti safedog, sudah diaktifkan. Jika ya, nonaktifkan firewall dan perangkat lunak lain.

#### Instans Linux:
1. Jalankan perintah berikut untuk memeriksa apakah kebijakan firewall sudah diaktifkan. Jika tidak, lewati langkah 2 dan lanjutkan ke langkah 3.
```
iptables -vnL
```

2. Jika kebijakan firewall sudah diaktifkan, jalankan perintah berikut untuk mencadangkan kebijakan firewall:
```
iptables-save
```

3. Jalankan perintah berikut untuk menghapus kebijakan firewall:
```
iptables -F
```

### Apakah firewall akan menghadang CVM Cloud CDN non-Tencent?
Tidak. Jika khawatir firewall mengganggu bisnis, Anda dapat menonaktifkan firewall.
