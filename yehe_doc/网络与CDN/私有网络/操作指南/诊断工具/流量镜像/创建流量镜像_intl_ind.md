Cermin lalu lintas menyediakan layanan pengumpulan lalu lintas yang memungkinkan Anda memfilter lalu lintas dari ENI yang ditentukan menggunakan 5-tupel dan aturan lainnya. Kemudian Anda dapat menyalin lalu lintas yang difilter ke instans CVM di VPC yang sama. Fitur ini berlaku untuk kasus penggunaan termasuk audit keamanan, pemantauan risiko, pemecahan masalah, dan analisis bisnis. Dokumen ini menjelaskan cara membuat cermin lalu lintas.
>? Fitur cermin lalu lintas saat ini dalam versi beta. Jika Anda ingin mencobanya, harap [kirim tiket](https://console.cloud.tencent.com/workorder/category). Simpan tautan ke konsol Cermin Lalu Lintas untuk login nanti, jika tidak, Anda mungkin perlu mendaftar lagi.

## Prasyarat
Pastikan IP yang dikumpulkan dan IP penerima berada di VPC yang sama dan IP yang dikumpulkan memiliki tabel rute yang menunjuk ke IP penerima.
## Petunjuk
### Langkah 1: buat sumber cermin lalu lintas
1. Buka tautan yang Anda peroleh setelah [mengirimkan tiket](https://console.cloud.tencent.com/workorder/category) dan login ke konsol Cermin Lalu Lintas. Pada pemilih **Region** (Wilayah) atas, pilih wilayah tempat cermin lalu lintas akan dibuat.
2. Klik **+New** (+Baru).
>? Hingga 5 cermin lalu lintas dapat dibuat dalam satu VPC.

3. Pada jendela pop-up, konfigurasikan sebagai berikut:
 - Masukkan nama untuk cermin lalu lintas, yang tidak boleh melebihi 60 karakter.
 - Pilih **Network** (Jaringan).
 - Pilih **Collection Range** (Rentang Koleksi):
    - **Virtual Private Cloud**: semua lalu lintas di VPC kecuali lalu lintas cermin dari IP penerima akan dikumpulkan, yang biasanya berlaku untuk skenario cermin penuh.
    - **Subnet** (Subnet): semua lalu lintas di subnet VPC kecuali lalu lintas yang dicerminkan dari IP penerima akan dikumpulkan. Opsi ini memerlukan pemilihan subnet tertentu.
    - **ENI** (ENI): semua lalu lintas di VPC akan dikumpulkan, tetapi lalu lintas ENI yang terikat dengan IP penerima akan dikecualikan. Opsi ini memerlukan pemilihan ENI tertentu.
      ![](https://main.qcloudimg.com/raw/5a359241aabeccd7424324e8357d8251.png)
 - Pilih **Collection Type** (Jenis Koleksi): pilih arah lalu lintas sesuai kebutuhan. Ada tiga opsi: Semua lalu lintas, Lalu Lintas keluar dan Lalu Lintas masuk.
 - Pilih **Traffic filtering** (Pemfilteran lalu lintas): pilih metode untuk memfilter lalu lintas yang tidak perlu dan menjaga cermin tetap kecil dan ringan.
    - **N/A** (T/A): semua lalu lintas yang dikonfigurasi akan dikumpulkan.
    - **Quintuple** (Quintuple): lalu lintas yang memenuhi ketentuan 5-tupel akan dikumpulkan. Setelah opsi ini dipilih, tentukan **Protocol**, **Source IP range**, **Destination IP range**, **Source port**, dan **Destination port** (Protokol, Rentang IP Sumber, Rentang IP Tujuan, Port Sumber, dan Port Tujuan). Anda dapat mengeklik **Add** (Tambahkan) untuk membuat kondisi filter lain. Hanya lalu lintas yang memenuhi semua ketentuan filter yang akan dikumpulkan.
    ![](https://main.qcloudimg.com/raw/1b49eca6a1e7f736633ee2762f5d6620.png)
    - **The next hop is the NAT gateway** (Hop selanjutnya adalah NAT gateway): mengumpulkan lalu lintas yang alamat hop selanjutnya adalah NAT gateway. Setelah opsi ini dipilih, pilih NAT gateway yang sesuai di sebelah **Condition** (Kondisi).
4. Setelah konfigurasi selesai, klik **Next** (Selanjutnya).

### Langkah 2: buat target cermin lalu lintas
1. Atur lalu lintas penerima sebagai berikut:
    + **Receiving IP** (Penerimaan IP): masukkan alamat IP yang menerima lalu lintas yang dicerminkan.
       > ?
       > + Jika bidang ini dibiarkan kosong, tidak ada lalu lintas yang akan dicerminkan. Jadi masukkan setidaknya satu IP penerima.
       > + Pisahkan IP dengan jeda baris atau koma.
       > + Lalu lintas yang dihasilkan oleh IP penerima di VPC tidak akan dikumpulkan.

    + **Balance method** (Metode Saldo): pilih salah satu dari:
        + **Evenly distribute traffic** (Distribusikan lalu lintas secara merata): semua lalu lintas akan disalin ke IP penerima ini secara merata.
        + **HASH by ENI** (HASH oleh ENI): lalu lintas dari ENI yang sama akan disalin ke IP penerima yang sama.
 ![](https://main.qcloudimg.com/raw/8bec0de6223c109daed7eefef1394959.png)
2. Setelah konfigurasi selesai, klik **OK** (Oke).

## Validasi Hasil
>! Dokumen ini mengambil pembuatan cermin lalu lintas yang mengumpulkan lalu lintas keluar dari 10.0.0.14 ENI yang mengakses situs web www.qq.com sebagai contoh.

1. Kembali ke halaman **Traffic mirroring** (Pencerminan lalu lintas). Jika cermin lalu lintas yang baru saja Anda buat ditampilkan dengan **Collect Traffic** (Kumpulkan Lalu Lintas) diaktifkan, cermin lalu lintas telah berhasil dibuat.
![](https://main.qcloudimg.com/raw/fd6191f3c858d0f2dd799a467c0d1c40.png)
2. Lakukan langkah-langkah berikut untuk memverifikasi apakah lalu lintas yang dikumpulkan dicerminkan ke IP penerima.
	1. Hasilkan lalu lintas ENI. Misalnya, Anda dapat login ke CVM sumber dan menjalankan perintah `ping ***public IP***` (IP publik).
    **Source data:** (Data Sumber:)
	 ![](https://main.qcloudimg.com/raw/74ad4cbd7a6f2179b441cafee5976bba.png)
	 <span id="buzhou2"></span>
	2. Login ke CVM tujuan dan jalankan perintah berikut untuk mengambil data dan menyimpannya sebagai file “.cap” atau “.pcap”. Dokumen ini menggunakan file “.pcap” sebagai contoh.
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
3. Jika paket luar biasa diperoleh, atau tidak dapat memperoleh paket, [kirim tiket](https://console.cloud.tencent.com/workorder/category).

## Operasi Selanjutnya
- [Mengaktifkan atau menonaktifkan cermin lalu lintas](https://intl.cloud.tencent.com/document/product/215/36393)
- [Memodifikasi cermin lalu lintas](https://intl.cloud.tencent.com/document/product/215/36393)
- [Menambahkan tag](https://intl.cloud.tencent.com/document/product/215/36393)
- [Menghapus cermin lalu lintas](https://intl.cloud.tencent.com/document/product/215/36393)
