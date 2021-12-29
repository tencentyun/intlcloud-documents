### Mengunduh file
Klik [di sini](https://main.qcloudimg.com/raw/037dee0e98e30eb15055645ff0a48694.zip) untuk mengunduh file.

## Versi Umum
## Deskripsi File

| File | Deskripsi |
| ----------------- | ------------------------------------------------------------ |
| WinPcap_4_1_3.exe | Driver WinPcap, lihat [Dokumentasi WinPcap](https://www.winpcap.org/) untuk detailnya |
| lib_toa.lib | Pustaka statis TOA |
| toa_fetcher.h | File header yang diandalkan oleh pustaka statis |
| pcap.h | File header yang diandalkan oleh pustaka statis |

### Mempersiapkan lingkungan
1. Klik dua kali WinPcap_4_1_3.exe untuk menginstal driver WinPcap (mulai ulang tidak diperlukan).
2. Tambahkan lib_toa.lib ke jalur pustaka .lib proyek.
3. Tambahkan toa_fetcher.h dan pcap.h ke file header proyek.

## Versi Go
## Deskripsi Filte

| File | Description |
| ------------------- | ------------------------------------------------------------ |
| WinPcap_4_1_3.exe | Driver WinPcap, lihat [Dokumentasi WinPcap](https://www.winpcap.org/) untuk detailnya |
| toa_win.exe | Program TOA untuk server Windows |
| toa_win.conf | File konfigurasi program TOA untuk server Windows |
| program_auto_up.bat | bat script for Windows server |
| demo.go | Contoh program yang ditulis dalam bahasa Go, digunakan untuk mengakses layanan TOA |

### Langkah Deployment
1. Ubah file toa_win.conf seperti yang diinstruksikan di bawah ini:
<table>
<tr>
<th>Parameter</th><th>Diperlukan</th><th>Deskripsi</th>
</tr>
<tr>
<td>ToaWinPort</td><td>Ya</td><td>Port layanan toa_win.exe, digunakan untuk berkomunikasi dengan klien TOA, defaultnya adalah 9999.</td>
</tr>
<tr>
<td>NetworkCardIP</td><td>Ya</td><td>Ini digunakan untuk mengidentifikasi alamat IP dari antarmuka jaringan, misalnya, 10.75.132.39. Ini adalah NIC yang berkomunikasi dengan klien.</td>
</tr>
<tr>
<td>ServerListenIP</td><td>Ya</td><td>Alamat IP server, misalnya, 10.75.132.39. Ini digunakan untuk memfilter aliran TCP.</td>
</tr>
<tr>
<td>ServerListenPortList</td><td>Tidak</td><td>Daftar port server. Ini digunakan untuk memfilter aliran TCP. Maksimal 3 port dapat ditambahkan.<br><b>ServerListenPortList atau PortRange harus dikonfigurasi.</b></td>
</tr>
<tr>
<td>PortRange</td><td>Tidak</td><td>Rentang port server. Ini digunakan untuk memfilter aliran TCP. Maksimal 3 rentang port dapat ditambahkan.<br><b>ServerListenPortList atau PortRange harus dikonfigurasi.</b></td>
</tr>
<tr>
<td>CacheSeconds</td><td>Tidak</td><td>Panjang waktu cache, satuan dalam detik. Nilai default adalah 15 detik. </td>
</tr>
</table>

 >!File konfigurasi harus ditempatkan di direktori yang sama dengan toa_win.exe.
 
 ![](https://main.qcloudimg.com/raw/d53c1cb161f45c9ad75789ac1c832af6.png)
2. Memodifikasi program_auto_up.bat.
Modifikasi jalur ke direktori tempat program berada. Tambahkan skrip ke tugas terjadwal, dan jalankan secara berkala. Skrip tersebut digunakan untuk memantau program toa_win.exe dan secara otomatis mengaktifkan program saat keluar.
![](https://main.qcloudimg.com/raw/046bbd4282aa51f85baa6879de8586d4.png)
3. Jalankan program toa_win.exe. Log disimpan ke toa_win.log di direktori yang sama. Sekarang, Anda bisa mendapatkan alamat IP yang nyata dari layanan TOA melalui komunikasi UDP. Untuk detailnya, lihat [Cara Menggunakan](https://cloud.tencent.com/document/product/608/17670).
