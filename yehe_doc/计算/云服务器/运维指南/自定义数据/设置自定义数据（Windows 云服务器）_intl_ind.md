## Pengantar

Saat membuat instans CVM, Anda memiliki opsi untuk menentukan skrip sebagai **Custom Data** (Data Kustom) dan menggunakannya untuk menyesuaikan konfigurasi instans Anda. Saat instans dimulai untuk pertama kalinya, data kustom tersebut diteruskan dan dijalankan. Jika Anda membeli beberapa instans CVM, semua instans akan menjalankan skrip pada peluncuran pertama.
Artikel ini menjelaskan cara menentukan skrip PowerShell dan menggunakannya untuk mengonfigurasi instans CVM Windows.

## Pertimbangan

- Sistem operasi Windows yang mendukung data kustom meliputi:
 - Windows Server 2019 Datacenter Edition 64-bit versi bahasa Mandarin/Inggris
 - Windows Server 2016 Datacenter Edition 64-bit versi bahasa Mandarin/Inggris
 - Windows Server 2012 R2 Datacenter Edition 64-bit versi bahasa Mandarin/Inggris
- Skrip dijalankan ketika dan hanya ketika instans dijalankan untuk pertama kalinya.
- Sebelum pengkodean Base64, ukuran data kustom tidak boleh melebihi 16 KB.
- Data kustom yang dikodekan dengan Base64 dan kemudian diteruskan. Jika Anda menginginkan file skrip dalam bentuk aslinya, jangan pilih **The entry is Base64-encoded text** (Entrinya adalah teks dengan pengodean Base64).
- Konfigurasi kustom yang Anda tetapkan dalam skrip data kustom membutuhkan waktu untuk dijalankan. Kami sarankan Anda menunggu konfigurasi selesai dan memverifikasi hasilnya.
- Gunakan tag PowerShell, seperti &lt;powershell&gt;&lt;/powershell&gt; untuk mendeklarasikan konten skrip Windows PowerShell.

## Petunjuk

### Menyiapkan skrip

Siapkan skrip yang sesuai dengan kebutuhan Anda:

<span id="PowerShellScript"></span>
#### Skrip PowerShell
Gunakan tag PowerShell untuk mengapit konten skrip.
Misalnya, jika Anda ingin menggunakan skrip untuk membuat file bernama `tencentcloud.txt` dengan konten “Hello Tencent Cloud.” di drive C:, gunakan tag berikut:
```
<powershell>
"Hello Tencent Cloud." | File Keluar C:\tencentcloud.txt
</powershell>
```

<span id="Base64Script"></span>
#### Mengodekan skrip dengan Base64

1. Jalankan perintah berikut untuk membuat skrip PowerShell bernama "script_text.ps1".
```
vi script_text.ps1
```
2. Tekan **i** untuk beralih ke mode pengeditan, masukkan konten berikut, dan simpan.
```
<powershell>
"Hello Tencent Cloud." | File Keluar C:\tencentcloud.txt
</powershell>
```
3. Jalankan perintah berikut untuk mengodekan **script_text.ps1** dengan Base64.
```
base64 script_text.ps1
```
Informasi berikut ditampilkan:
```
PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAgQzpcdGVuY2VudGNsb3VkLnR4dAo8L3Bvd2Vyc2hlbGw+Cg==
```

### Meneruskan skrip

Kami menyediakan beberapa metode untuk meluncurkan sebuah instans. Berikut ini adalah metode yang paling banyak digunakan:
- [Menggunakan situs resmi atau konsol](#Consoletrans)
- [Menggunakan API](#APItrans)

<span id="Consoletrans"></span>
#### Menggunakan situs web resmi atau konsol

1. Gunakan [Membuat Instans](https://intl.cloud.tencent.com/document/product/213/4855) sebagai referensi dan buat instans CVM. Klik **Advanced Configuration** (Konfigurasi Lanjutan) di **4. Configure Security Group and CVM** (Konfigurasi Grup Keamanan dan CVM), seperti terlihat pada gambar berikut:
![](https://main.qcloudimg.com/raw/28baf2764488ecfaf5bbac791cec7ea3.png)
2. Di **Advanced Configuration** (Konfigurasi Lanjutan), masukkan konten skrip di kotak teks **Custom Data** (Data Kustom).
 - Skrip PowerShell: masukkan konten skrip yang Anda masukkan di [skrip PowerShell](#PowerShellScript) dalam bentuk aslinya.
 - Skrip yang dikodekan dengan Base64: pilih **The entry is Base64-encoded text** (Entri adalah teks yang dikodekan dengan Base64), dan masukkan konten skrip yang dikodekan yang Anda kodekan di [Mengodekan skrip dengan Base64](#Base64Script), seperti yang ditunjukkan pada gambar berikut:
 ![](https://main.qcloudimg.com/raw/0b6b594f174568ca7d3312821c0571ed.png)
4. Ikuti instruksi dan selesaikan pembuatan CVM.

<span id="APItrans"></span>
#### Menggunakan API

Jika Anda memilih untuk membuat instans CVM menggunakan Tencent Cloud API, Anda dapat menetapkan hasil pengodean yang ditampilkan di [Mengodekan skrip dengan Base64](#Base64Script) ke parameter UserData RunInstances.
Berikut ini adalah contoh permintaan pembuatan CVM dengan UserData:
```
https://cvm.tencentcloudapi.com/?Action=RunInstances
  &Version=2017-03-12
  &Placement.Zone=ap-guangzhou-2
  &ImageId=img-pmqg1cw7
  &UserData=PHBvd2Vyc2hlbGw+CiJIZWxsbyBUZW5jZW50IENsb3VkLiIgfCBPdXQtRmlsZSAuXHRlbmNlbnRjbG91ZC50eHQKPC9wb3dlcnNoZWxsPgo=
  &<Common request parameter>
```

### Memverifikasi konfigurasi data kustom

1. Login ke instans CVM.
2. Buka drive C:, dan periksa apakah sudah ada `tencentcloud.txt`.
Jika sudah ada, berarti konfigurasi berhasil, seperti yang ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/9f94ec922111734a489b9730d66168c3.png)


