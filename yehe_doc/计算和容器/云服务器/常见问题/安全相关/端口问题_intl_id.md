### Port mana yang harus dibuka ke Internet sebelum saya login ke instans?
Biasanya, Anda perlu membuka port 22 untuk instans Linux, atau port 3389 untuk instans Windows. Untuk informasi selengkapnya tentang port yang berlaku untuk jenis instans lain, lihat [Kasus Penggunaan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/32369).

### Port mana yang sering digunakan di CVM?

Untuk informasi selengkapnya, lihat [Port Umum Server](https://intl.cloud.tencent.com/document/product/213/12451).

### Mengapa port harus dibuka ke Internet? Bagaimana cara membuka port tertentu?

Anda dapat menggunakan layanan hanya setelah membuka port ke Internet dalam grup keamanan. Contohnya:
Jika Anda ingin mengakses halaman web menggunakan port 8080, port tersebut harus diaktifkan dan dibuka ke Internet dalam grup keamanan.
Untuk membuka port ke Internet, ikuti langkah-langkah berikut:
1. Buka halaman [grup keamanan] (https://console.cloud.tencent.com/vpc/securitygroup), dan klik ID/nama grup keamanan yang terikat dengan instans ini untuk membuka halaman detailnya.
2. Pilih **Inbound/Outbound rule** (Aturan Masuk/Keluar) dan klik **Add a Rule** (Tambahkan Aturan).
3. Masukkan alamat IP (rentang) dan port yang akan dibuka, lalu pilih **Allow** (Izinkan) untuk membuka port.
Untuk informasi selengkapnya, lihat [Menambahkan Aturan Grup Keamanan](https://intl.cloud.tencent.com/document/product/213/34272).

### Bagaimana cara mengubah port jarak jauh default pada instans CVM?

Untuk informasi selengkapnya, lihat [Mengubah Port Jarak Jauh Default pada CVM](https://intl.cloud.tencent.com/document/product/213/35376).


### Mengapa layanan tidak dapat digunakan setelah saya mengubah port?

Setelah mengubah port layanan, Anda juga perlu membuka port yang sesuai ke Internet dalam grup keamanan.

### Port mana yang tidak didukung oleh Tencent Cloud?

- Secara default, port TCP 25 diblokir oleh Tencent Cloud. Jika Anda perlu membuka blokir port ini, lihat [Membuka Blokir Port 25](https://intl.cloud.tencent.com/document/product/213/34833).
- Beberapa port memiliki risiko keamanan. Meskipun port ini tidak diblokir oleh Tencent Cloud, port tersebut akan diblokir oleh ISP dan tidak dapat diakses. Agar hal ini tidak terjadi, sebaiknya Anda mengubah port dan tidak menggunakan port berikut untuk mendengarkan:
<table>
<tr><th>Protokol</th><th>Port yang Diblokir</th></tr>
<tr><td>TCP</td><td>42, 135, 137, 138, 139, 445, 593, 1025, 1434, 1068, 3127, 3128, 3129, 3130, 4444, 5554, 5800, 5900, 9996</td></tr>
<tr><td>UDP</td><td>1026, 1027, 1434, 1068, 5554, 9996, 1028, 1433, 135 - 139</td></tr>
</table>


### Mengapa saya tidak dapat menggunakan port TCP 25?
Port TCP 25 adalah port layanan email default. Karena alasan keamanan, port 25 instans CVM diblokir secara default. Jika Anda perlu menggunakannya, lihat [Membuka Blokir Port 25](https://intl.cloud.tencent.com/document/product/213/34833).

