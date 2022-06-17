Mengirim kode verifikasi melalui SMS adalah cara paling populer dan paling aman untuk memverifikasi identitas pengguna. Saat ini, kode verifikasi SMS banyak digunakan dalam berbagai skenario aplikasi, seperti pendaftaran pengguna, pengaturan ulang kata sandi, perlindungan login, verifikasi identitas, pembuatan kata sandi acak, dan konfirmasi transaksi.
Dokumen ini menggunakan pengembangan layanan login dan pendaftaran dengan kode verifikasi berdasarkan [SCF](https://Intl.cloud.tencent.com/document/product/583) sebagai contoh untuk menjelaskan cara menerapkan fitur kode verifikasi SMS.

Selain SCF, Anda dapat menggunakan API [SendSms](https://intl.cloud.tencent.com/document/product/382/34859) untuk tujuan ini.

## Persiapan
- Anda telah [membuat akun Tencent Cloud](https://intl.cloud.tencent.com/document/product/378/17985) dan [menyelesaikan verifikasi organisasi Anda](https://intl.cloud.tencent.com/document/product/378/10496).
- Anda telah membeli paket SMS.
- Siapkan sertifikat kualifikasi pemilik tanda tangan SMS.
 Misalnya, dokumen ini menggunakan izin usaha sebagai sertifikat kualifikasi.
- Pahami standar peninjauan konten isi SMS.
- Dapatkan `SDKAppID` untuk aplikasi SMS.

## Dokumen Terkait
- [Kode sumber demo](https://github.com/tencentyun/scf-demo-repo/tree/master/Nodejs8.9-SmsVerificationCode)
- Dokumentasi produk lainnya
 - [Dokumentasi VPC](https://intl.cloud.tencent.com/document/product/215)
 - [Dokumentasi TencentDB for Redis](https://intl.cloud.tencent.com/document/product/239/3205)
 - [Dokumentasi SCF](https://intl.cloud.tencent.com/zh/document/product/583)

## Langkah 1. Konfigurasikan konten SMS[](id:Step1)
Tanda tangan atau templat isi SMS umumnya akan ditinjau dalam waktu dua jam setelah dikirim. Anda dapat [mengonfigurasikan kontak alarm](https://intl.cloud.tencent.com/document/product/382/35470) dan mengatur pemberitahuan peninjauan templat/tanda tangan untuk menerima pemberitahuan hasil peninjauan.

### Langkah 1.1. Buat tanda tangan[](id:Step1_1)

1. Login ke [konsol SMS](https://console.cloud.tencent.com/smsv2).
2. Pilih **Chinese Mainland SMS** > **Signatures** (SMS Tiongkok Daratan > Tanda Tangan) di bilah sisi kiri, lalu klik **Create Signature** (Buat Tanda Tangan).
3. Atur parameter berikut sesuai dengan kebutuhan:
 <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th>Nilai Sampel</th>  
     </tr>
	 <tr>      
       <td>Tujuan tanda tangan</td>   
	     <td>Untuk entitas terverifikasi (seperti organisasi, situs web, atau nama produk dengan tanda tangan yang diverifikasi oleh akun)</td>   
     </tr> 
	 <tr>      
       <td>Jenis tanda tangan</td>   
	     <td>Aplikasi</td>   
     </tr> 
	 <tr>      
       <td>Konten tanda tangan</td>   
	     <td>Demo pengujian</td>   
     </tr> 
	 <tr>      
       <td>Jenis sertifikat</td>   
	     <td>Tangkapan layar halaman pengaturan Program Mini WeChat</td>   
     </tr> 
</table>
3. Klik **OK** (Oke).
Tunggu peninjauan tanda tangan. Tanda tangan SMS hanya akan tersedia setelah statusnya berubah menjadi **approved** (disetujui).


### Langkah 1.2. Buat templat isi[](id:Step1_2)
1. Login ke [konsol SMS](https://console.cloud.tencent.com/smsv2).
2. Pilih **Chinese Mainland SMS** > **Body Templates** (SMS Tiongkok Daratan > Templat Isi) di bilah sisi kiri, lalu klik **Create Body Template** (Buat Templat Isi).
3. Atur parameter berikut sesuai dengan kebutuhan:
 <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th>Nilai Sampel</th>  
     </tr>
	 <tr>      
        <td>Nama templat</td>   
	     <td>SMS kode verifikasi</td>   
     </tr> 
	 <tr>      
        <td>Jenis SMS</td>   
	     <td>SMS biasa</td>   
     </tr> 
	 <tr>      
        <td>Konten SMS</td>   
	     <td>Kode verifikasi pendaftaran Anda adalah {1}. Masukkan kode verifikasi pendaftaran dalam {2} menit. Abaikan pesan ini jika Anda tidak melakukan pendaftaran.</td>   
     </tr> 
</table>
4. Klik **OK** (Oke).
Tunggu peninjauan templat isi. Templat isi hanya akan tersedia setelah statusnya berubah menjadi **approved** (disetujui). Harap catat ID templat.

## Langkah 2. Atur batas frekuensi pengiriman SMS (opsional)[](id:Step2)
>!Pengguna individu tidak memiliki izin untuk mengubah batas frekuensi pengiriman. Untuk menggunakan fitur ini, ubah "Individual Verification" (Verifikasi Individu) menjadi "Organization Verification" (Verifikasi Organisasi).

Untuk memastikan keamanan bisnis dan saluran serta meminimalkan potensi kerugian finansial yang disebabkan oleh panggilan berbahaya dari API SMS, Anda sebaiknya [mengatur batas frekuensi pengiriman](https://intl.cloud.tencent.com/document/product/382/35469). Selain itu, Anda dapat menggunakan Captcha Tencent Cloud untuk memaksimalkan perlindungan keamanan bisnis Anda.
Dokumen ini menggunakan kebijakan batas frekuensi pengiriman SMS default sebagai contoh.

- Untuk pesan SMS dengan konten sama, maksimum satu pesan dengan konten sama dapat dikirim ke nomor ponsel yang sama dalam periode 30 detik.
- Maksimum 10 pesan dapat dikirim ke nomor ponsel yang sama pada satu hari kalender.

## Langkah 3. Konfigurasikan VPC dan subnet[](id:Step3)
Secara default, SCF di-deploy di jaringan publik dan hanya dapat mengakses jaringan publik. Jika Anda perlu mengakses sumber daya Tencent Cloud, seperti instans TencentDB, Anda perlu membangun VPC untuk memastikan keamanan data dan koneksi.

1. [Rencanakan desain jaringan](https://intl.cloud.tencent.com/document/product/215/31795) sesuai kebutuhan.
2. Buat VPC. Untuk petunjuk mendetail, lihat [Creating VPC (Membuat VPC)](https://intl.cloud.tencent.com/document/product/215/31805).
 >!CIDR dari VPC dan subnet tidak dapat diubah setelah dibuat.
 >
 <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th>Nilai Sampel</th>  
     </tr>
	 <tr>      
        <td>Wilayah</td>   
	     <td>Tiongkok Selatan (Guangzhou)</td>   
     </tr> 
	 <tr>      
        <td>Nama</td>   
	     <td>VPC Demo</td>   
     </tr> 
	 <tr>      
        <td>CIDR IPv4</td>   
	     <td>10.0.0.0/16</td>   
     </tr> 
	 <tr>      
        <td>Nama subnet</td>   
	     <td>Subnet demo</td>   
     </tr> 
	 <tr>      
        <td>CIDR IPv4</td>   
	     <td>10.0.0.0/16</td>   
     </tr> 
	 <tr>      
        <td>AZ</td>   
	     <td>Zona Guangzhou 3</td>   
     </tr> 
</table>

## Langkah 4. Konfigurasikan instans TencentDB for Redis[](id:Step4)
Wilayah dan subnet AZ dari instans TencentDB for Redis harus sama dengan wilayah dan subnet AZ dari VPC yang dikonfigurasikan di [langkah 3](#Step3).

1. Beli instans TencentDB for Redis. Untuk petunjuk mendetail, lihat [Creating TencentDB for Redis Instance (Membuat Instans TencentDB for Redis)](https://intl.cloud.tencent.com/document/product/239/37712).
 <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th>Nilai Sampel</th>  
     </tr>
	 <tr>      
        <td>Mode penagihan</td>   
	     <td>Bayar sesuai pemakaian</td>   
     </tr> 
	 <tr>      
        <td>Wilayah</td>   
	     <td>Guangzhou</td>   
     </tr> 
	 <tr>      
        <td>Versi database</td>   
	     <td>Redis 4.0</td>   
     </tr> 
	 <tr>      
        <td>Arsitektur</td>   
	     <td>Arsitektur standar</td>   
     </tr> 
	 <tr>      
        <td>Jaringan</td>   
	     <td>VPC demo dan subnet demo</td>   
     </tr> 
	 <tr>      
        <td>Nama instans</td>   
	     <td>Database demo</td>   
     </tr> 
	 <tr>      
        <td>Kuantitas pembelian</td>   
	     <td>1</td>   
     </tr> 
</table>

## Langkah 5. Buat fungsi[](id:Step5)
SCF saat ini mendukung pengembangan di Python, Node.js, PHP, Java, dan Go. Dokumen ini menggunakan Node.js sebagai contoh.

1. Buat fungsi di wilayah VPC yang dibuat di [langkah 3](#Step3). Untuk petunjuk mendetail, lihat [Fungsi Penulisan](https://intl.cloud.tencent.com/document/product/583/32742).
  <table>
     <tr>
         <th width="20%">Parameter</th>  
         <th>Nilai Sampel</th>  
     </tr>
	 <tr>      
        <td>Nama fungsi</td>   
	     <td>Demo</td>   
     </tr> 
	 <tr>      
        <td>Lingkungan runtime</td>   
	     <td>Node.js 8.9</td>   
     </tr> 
	 <tr>      
        <td>Metode pembuatan</td>   
	     <td>Fungsi templat: helloworld</td>   
     </tr> 
</table>
2. Deploy fungsi dan atur **API Gateway Trigger** (Pemicu Gateway API) sebagai pemicu. Untuk petunjuk mendetail, lihat [Men-deploy Fungsi](https://intl.cloud.tencent.com/document/product/583/32742).

## Langkah 6. Aktifkan akses jaringan publik (opsional)[](id:Step6)
- Fungsi yang di-deploy di VPC sebelum 29 April 2020 diisolasi dari jaringan publik secara default. Anda dapat mengaktifkan akses jaringan publik jika ingin fungsi tersebut memiliki akses ke jaringan pribadi dan jaringan publik.
 Login ke [konsol SCF](https://console.cloud.tencent.com/scf/index?rid=1), pilih **Function Service** (Layanan Fungsi), klik nama fungsi target dalam daftar fungsi untuk masuk ke halaman konfigurasi fungsi. Klik **Edit**, periksa **Public Network Access** (Akses Jaringan Publik), lalu klik **Save** (Simpan) untuk menyimpan konfigurasi.
- Fungsi yang di-deploy pada atau setelah 29 April 2020 memiliki akses jaringan publik yang diaktifkan secara default, dan tidak memerlukan operasi tambahan.

## Langkah 7. Deploy demo SMS[](id:Step7)
1. Buka [konsol SCF](https://console.cloud.tencent.com/scf/), lalu pilih demo SMS yang akan di-deploy.


2. Atur variabel lingkungan demo di **Advanced Configuration** (Konfigurasi Lanjutan).



| Bidang | Deskripsi |
| ----- | ----- |
| REDIS_HOST| Alamat database Redis. |
|REDIS_PASSWORD| Kata sandi database Redis. |
| SMS_TEMPLATE_ID| ID templat. Anda harus memasukkan ID templat yang disetujui, yang dapat dilihat di [konsol SMS](https://console.cloud.tencent.com/smsv2). |
| SMS_SIGN| Konten tanda tangan SMS, yang harus dikodekan dalam UTF-8. Anda harus memasukkan tanda tangan yang disetujui, yang dapat dilihat di [konsol SMS](https://console.cloud.tencent.com/smsv2). Catatan: parameter ini diperlukan untuk SMS Tiongkok Daratan. |
| SMS_SDKAPPID| `SdkAppid` SMS sebenarnya dibuat setelah aplikasi ditambahkan di [konsol SMS](https://console.cloud.tencent.com/smsv2), seperti 1400006666. |


3. Atur lingkungan VPC yang sama dengan database Redis di **Advanced Configuration** (Konfigurasi Lanjutan).



4. Atur izin **execution role** (peran eksekusi) SCF di **Advanced Configuration** (Konfigurasi Lanjutan).

Anda perlu mengaitkan kebijakan `QcloudSMSFullAccess` dengan peran `SCF_QcsRole` di [konsol CAM](https://console.cloud.tencent.com/cam/role).

Dengan cara ini, variabel lingkungan `TENCENTCLOUD_SECRETID`, `TENCENTCLOUD_SECRETKEY`, dan `TENCENTCLOUD_SESSIONTOKEN` dapat diperoleh dalam kode, yang akan digunakan oleh SMS SDK.

5. Klik **Complete** (Selesai) untuk men-deploy fungsi.

6. Buat **API Gateway trigger** (Pemicu Gateway API) SCF dan minta alamat pemicu untuk menggunakan kemampuan SMS.


## Langkah 8. Gunakan fitur
Kode verifikasi memiliki persyaratan yang tinggi untuk ketepatan waktu. Anda dapat menyimpan kode verifikasi di memori atau TencentDB for Redis dan menggunakan nomor ponsel sebagai kunci untuk menyimpan informasi, seperti waktu pengiriman, kode verifikasi, jumlah upaya verifikasi, dan hasil verifikasi.

### Fitur
#### Mengirim kode verifikasi SMS
Parameter permintaan:

| Bidang | Jenis | Deskripsi |
| ----- | ----- | ----- |
| method|string| Metode permintaan, yang memiliki nilai `getSms` |
|phone|string| Nomor ponsel dalam format kode area + nomor ponsel, misalnya 86185662466** |

#### Memverifikasi kode verifikasi (login)
Parameter permintaan:

| Bidang | Jenis | Deskripsi |
| ----- | ----- | ----- |
| method|string| Metode permintaan, yang memiliki nilai `login` |
|phone|string| Nomor ponsel dalam format kode area + nomor ponsel, misalnya 86185662466** |
| code|string| Kode verifikasi 6 digit |

### Kode kesalahan
| Bidang | Deskripsi |
| ----- | ----- |
| InValidParam| Parameter tidak ada |
| MissingCode| Parameter kode verifikasi tidak ada |
| CodeHasExpired| Kode verifikasi telah kedaluwarsa |
| CodeHasValid| Kode verifikasi tidak valid |
| CodeIsError| Harap periksa kesesuaian nomor ponsel dan kode verifikasi |
