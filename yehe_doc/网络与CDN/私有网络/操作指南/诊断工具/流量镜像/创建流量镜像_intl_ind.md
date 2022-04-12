Cermin lalu lintas menyediakan layanan pengumpulan lalu lintas yang memungkinkan Anda memfilter lalu lintas dari ENI yang ditentukan menggunakan 5-tupel dan aturan lainnya. Kemudian Anda dapat menyalin lalu lintas yang difilter ke instans CVM di VPC yang sama. Fitur ini berlaku untuk kasus penggunaan termasuk audit keamanan, pemantauan risiko, pemecahan masalah, dan analisis bisnis. Dokumen ini menjelaskan cara membuat cermin lalu lintas.
>? Fitur cermin lalu lintas saat ini dalam versi beta. Jika Anda ingin mencobanya, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category). Simpan tautan ke konsol Cermin Lalu Lintas untuk login nanti, jika tidak, Anda mungkin perlu mendaftar lagi.

## Prasyarat
Pastikan IP sumber dan ENI target berada di VPC yang sama dan IP sumber memiliki tabel rute yang mengarah ke ENI target.
## Petunjuk
### Langkah 1: buat sumber cermin lalu lintas
1. Buka tautan yang Anda peroleh setelah [mengirimkan tiket](https://console.cloud.tencent.com/workorder/category) dan login ke konsol Cermin Lalu Lintas. Pada pemilih **Region** (Wilayah) atas, pilih wilayah tempat cermin lalu lintas akan dibuat.
2. Klik **+New** (+Baru).
>? Hingga 5 cermin lalu lintas dapat dibuat dalam satu VPC.
>
3. Pada jendela pop-up, konfigurasikan sebagai berikut:
   - Masukkan nama untuk cermin lalu lintas (maksimal 60 karakter).
   - Pilih **Network** (Jaringan).
   - Pilih **ENI** (ENI) untuk **Collection Range** (Rentang Pengumpulan). - **ENI** (ENI): semua lalu lintas di VPC akan dikumpulkan, tetapi lalu lintas ENI yang terikat dengan IP penerima akan dikecualikan. Opsi ini memerlukan pemilihan ENI tertentu.
![](https://qcloudimg.tencent-cloud.cn/raw/902cad1c6ecd774e67ffe72d3ce4ab64.png)
   - Pilih **Collection Type** (Jenis Pengumpulan): pilih arah lalu lintas sesuai kebutuhan. Ada tiga opsi: Semua lalu lintas, Lalu Lintas keluar dan Lalu Lintas masuk.
   - Pilih **Traffic filtering** (Pemfilteran lalu lintas): pilih metode untuk memfilter lalu lintas yang tidak diperlukan dan jaga agar cermin tetap berukuran kecil dan ringan.
      - **N/A** (T/A): semua lalu lintas yang dikonfigurasi akan dikumpulkan.
      - **Quintuple** (Quintuple): lalu lintas yang memenuhi ketentuan 5-tupel akan dikumpulkan. Setelah opsi ini dipilih, tentukan **Protocol** (Protokol), **Source IP range** (Rentang IP sumber), **Destination IP range** (Rentang IP tujuan), **Source port** (Port sumber), dan **Destination port** (Port tujuan). Anda dapat mengeklik **Add** (Tambahkan) untuk membuat kondisi filter lain. Hanya lalu lintas yang memenuhi semua ketentuan filter yang akan dikumpulkan.
    ![](https://qcloudimg.tencent-cloud.cn/raw/ab47286ffbc185a6287552ac44de0c6f.png)
   - **The next hop is the NAT gateway** (Hop selanjutnya adalah NAT gateway): mengumpulkan lalu lintas yang alamat hop selanjutnya adalah NAT gateway. Setelah opsi ini dipilih, pilih NAT gateway yang sesuai di sebelah **Condition** (Kondisi).
4. Setelah konfigurasi selesai, klik **Next** (Selanjutnya).

### Langkah 2: buat target cermin lalu lintas
1. Atur lalu lintas penerima sebagai berikut:
   + **Target type** (Jenis target): pilih ENI target untuk menerima lalu lintas.
> ?
> + Setidaknya satu target ENI harus dipilih.
> + Lalu lintas ke ENI target dari dalam VPC tidak dikumpulkan.
>
   + **Balance method** (Metode Seimbang): 
        + **Evenly distribution** (Distribusi merata): semua lalu lintas didistribusikan di antara semua ENI target secara merata.
        + **HASH by ENI** (HASH berdasarkan ENI): lalu lintas dari ENI selalu diteruskan ke ENI target tetap.
![](https://qcloudimg.tencent-cloud.cn/raw/4b3e1c1c5bde43ed33d1724b072bb5e6.png)
2. Klik **OK** (OKE).

## Validasi Hasil
>! Dokumen ini mengambil pembuatan cermin lalu lintas yang mengumpulkan lalu lintas keluar dari 10.0.0.14 ENI yang mengakses situs web www.qq.com sebagai contoh.
>
1. Kembali ke halaman **Traffic mirroring** (Pencerminan lalu lintas). Jika cermin lalu lintas yang baru saja Anda buat ditampilkan dengan **Collect Traffic** (Kumpulkan Lalu Lintas) diaktifkan, cermin lalu lintas telah berhasil dibuat.
![](https://main.qcloudimg.com/raw/fd6191f3c858d0f2dd799a467c0d1c40.png)
2. Lakukan langkah-langkah berikut untuk memverifikasi apakah lalu lintas yang dikumpulkan dicerminkan ke IP penerima.
	1. Hasilkan lalu lintas ENI. Misalnya, Anda dapat login ke CVM sumber dan menjalankan perintah `ping ***public IP***` (IP publik).
    **Source data:** (Data sumber:)
	 ![](https://main.qcloudimg.com/raw/74ad4cbd7a6f2179b441cafee5976bba.png)
	Login ke CVM tujuan dan jalankan perintah berikut untuk mengambil data dan menyimpannya sebagai file “.cap” atau “.pcap”. Dokumen ini menggunakan file “.pcap” sebagai contoh.
```plaintext
tcpdump -i eth0 -w capture-2020-10-27.pcap    #Masukkan nama file aktual.
```
	**Destination packets:** (Paket tujuan:) 
 ![](https://main.qcloudimg.com/raw/404f6d2c612ae76b78aa63a624e98910.png)
	3. Gunakan simulator terminal (seperti SecureCRT) untuk login ke CVM tujuan dan mengekspor file yang disimpan di [Langkah ii](#buzhou2).
 ```plaintext
sz -bye capture-2020-10-27.pcap
 ```
	4. Gunakan pengurai paket (seperti Wireshark) untuk mendapatkan data dari file “capture-2020-10-27.pcap” yang telah diunduh. Dalam contoh ini, 12 paket tercermin dari CVM sumber diperoleh dari CVM tujuan.
	 **Packet verification:** (Verifikasi paket:)
![](https://main.qcloudimg.com/raw/8011aef82006411e35edd41bf5eae5c4.png)
3. Jika paket luar biasa diperoleh, atau tidak dapat memperoleh paket, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category).

## Operasi selanjutnya
- [Mengaktifkan atau menonaktifkan cermin lalu lintas](https://intl.cloud.tencent.com/document/product/215/36393)
- [Memodifikasi cermin lalu lintas](https://intl.cloud.tencent.com/document/product/215/36393)
- [Menambahkan tag](https://intl.cloud.tencent.com/document/product/215/36393)
- [Menghapus cermin lalu lintas](https://intl.cloud.tencent.com/document/product/215/36393)
