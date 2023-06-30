## Ikhtisar
Port 53 adalah port terbuka Domain Name Server (DNS). Ini utamanya digunakan untuk resolusi nama domain. DNS bertindak sebagai penerjemah antara nama domain dan alamat IP, jadi pengguna hanya perlu mengingat nama domain untuk mengakses situs web dengan cepat.

“Classified Catalogue of Telecommunications Businesses” (Katalog Klasifikasi Bisnis Telekomunikasi) (Edisi 2015) telah menggolongkan layanan resolusi nama domain internet repetitif sebagai layanan telekomunikasi (Nomor kode: B26-1). Untuk mengelola layanan nama domain repetitif, dapatkan izin layanan telekomunikasi.

## Kebijakan dan peraturan terkait

**1. Layanan resolusi domain internet tidak diizinkan tanpa izin usaha.**
Jika Anda atau perusahaan Anda terlibat dalam bisnis ini, Anda harus mengajukan “Code and Protocol Conversion License” (Lisensi Konversi Kode dan Protokol). Untuk detail spesifik, hubungi administrasi telekomunikasi setempat Anda.
**“Tindakan Administratif Perizinan Penyelenggaraan Usaha Telekomunikasi” Pasal 46:** Barang siapa melanggar ketentuan Ayat 1 Pasal 16 dan Ayat 1 Pasal 28, yaitu dengan sewenang-wenang menyelenggarakan layanan telekomunikasi atau menyelenggarakan layanan telekomunikasi di luar ruang lingkup yang diizinkan, akan dikenakan hukuman sesuai dengan Pasal 69 “Peraturan Telekomunikasi Republik Rakyat Tiongkok”. Untuk pelanggaran serius, perintah akan diberikan untuk menangguhkan bisnis untuk rektifikasi yang akan disertakan dalam daftar penyedia layanan telekomunikasi yang tidak dapat dipercaya.
**“Peraturan Nama Domain Internet” Kementerian Industri dan Teknologi Informasi, Pasal 36:** Untuk menyediakan layanan resolusi nama domain, pelaku usaha harus mematuhi undang-undang, peraturan, dan standar yang relevan, dan memiliki kapasitas perlindungan keamanan teknis, layanan, jaringan, dan informasi yang relevan. Pelaku usaha harus menerapkan tindakan perlindungan jaringan dan keamanan informasi, mencatat dan menyimpan log resolusi nama domain, log O&M, dan mengubah catatan sesuai dengan hukum, untuk memastikan kualitas layanan resolusi serta keamanan sistem resolusi. Apabila layanan telekomunikasi dilibatkan, pelaku usaha akan memperoleh izin penyelenggaraan telekomunikasi sesuai hukum.
**2. Tencent Cloud tidak akan menyediakan layanan, seperti akses atau penagihan, untuk individu atau entitas yang belum memperoleh izin usaha atau pengajuan ICP untuk layanan informasi internet nonkomersial di Tiongkok Daratan.**
**“Tindakan Administratif untuk Perizinan Penyelenggaraan Usaha Telekomunikasi” Pasal 24, pelaku usaha telekomunikasi nilai tambah yang menyediakan layanan akses harus memenuhi peraturan berikut:** (Tiga) Penyediaan layanan, seperti akses atau penagihan, untuk entitas atau individu yang belum memperoleh izin usaha atau pengajuan ICP untuk layanan informasi internet nonkomersial di Tiongkok Daratan sesuai dengan hukum tidak diizinkan.
Jika Anda atau perusahaan Anda tidak terlibat dalam **layanan resolusi nama domain Internet**, Anda sebaiknya menyesuaikan kebijakan grup keamanan server Anda, dan menonaktifkan port 53 melalui aturan masuk.

## Menonaktifkan port 53 melalui aturan masuk

1. Login ke [Konsol Tencent Cloud CVM](https://console.cloud.tencent.com/cvm/index).
2. Pada halaman manajemen instans, pilih instans tempat port 53 akan dinonaktifkan, dan klik **ID/Name** (ID/Nama). Hal ini ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/186bd6ec5c69b12b3ea9645ff1dbb22b.png)
3. Pada halaman detail instans, pilih tab **Security Groups** (Grup Keamanan), untuk masuk ke halaman manajemen grup keamanan untuk instans ini. Hal ini ditunjukkan pada gambar berikut:
![](https://main.qcloudimg.com/raw/7eb1b0b56520701fc8d28a14cfecd7f1.png)
4. Pada bidang**Bound to security group** (Ikat ke grup keamanan), pilih **Security Group ID/Name** (ID/Nama Grup Keamanan) dari aturan masuk yang akan dimodifikasi.
5. Pada halaman **Security Group Rule** (Aturan Grup Keamanan), pilih tab **Inbound Rule** (Aturan Masuk). Klik **Add a Rule** (Tambah Aturan). Ini ditunjukkan pada gambar berikut.
![](https://main.qcloudimg.com/raw/f1f7f9ce6d3e259e06542bf19d797022.png)
6. Di jendela **Add Inbound Rule** (Tambah Aturan Masuk) yang muncul, masukkan informasi berikut. Hal ini ditunjukkan pada gambar berikut:
![Add inbound rules-disable port 53](https://main.qcloudimg.com/raw/f3890575ef22f31f67c0c6902f6df55a.png)
 - Jenis: Pilih "Custom" (Kustom).
 - Sumber: Masukkan "0.0.0.0/0".
 -Port protokol: Masukkan "UDP:53".
 - Kebijakan: Pilih “Reject” (Tolak).
7. Klik **Complete** (Selesai) untuk menonaktifkan port 53.

## Pertanyaan Umum

### Apa itu layanan resolusi nama domain internet?
**Internet Domain Name Resolution** (Resolusi Nama Domain Internet) adalah sambungan antara nama domain Internet dan alamat IP yang sesuai.
**Internet domain name resolution service** (Layanan resolusi nama domain Internet) membangun server resolusi nama domain dan perangkat lunak terkait di Internet untuk menerjemahkan nama domain Internet ke alamat IP yang sesuai. Ada dua jenis layanan resolusi nama domain: layanan resolusi otoritatif dan repetitif.
- Resolusi otoritatif: Layanan ini menyediakan resolusi nama domain untuk nama domain root, nama domain tingkat atas, dan nama domain tingkat lainnya.
- Resolusi repetitif: Layanan ini merupakan sambungan antara nama domain dan alamat IP dengan mengkueri cache lokal atau sistem layanan resolusi otoritatif.

Layanan resolusi nama domain internet di sini secara khusus mengacu pada layanan resolusi repetitif. Untuk informasi selengkapnya, lihat “Classification Catalog of Telecommunications Services” (Katalog Klasifikasi Bisnis Telekomunikasi) (Edisi 2015): B26-1 Layanan resolusi nama domain internet.

 
### Bagaimana pengaruh menonaktifkan port 53 melalui aturan masuk terhadap server saya?
Jika tidak terlibat dalam layanan resolusi nama domain internet, menonaktifkan port 53 melalui aturan masuk tidak memengaruhi server atau bisnis Anda.

### Dapatkah individu terlibat dalam layanan resolusi nama domain?
Penyelenggara layanan telekomunikasi harus telah memiliki usaha resmi sesuai hukum. Individu tidak dapat terlibat dalam jenis layanan ini. Anda harus mendapatkan “Lisensi Konversi Kode dan Protokol” sebelum menjalankan bisnis layanan resolusi nama domain internet. Untuk informasi selengkapnya tentang mendapatkan lisensi, Anda dapat menghubungi kantor administrasi telekomunikasi setempat.

### Apa dampak dari menjalankan layanan resolusi nama domain internet tanpa izin?
Menurut “Peraturan Telekomunikasi Republik Rakyat Tiongkok” Pasal 69: (Satu) Barang siapa melanggar Pasal 7 Ayat 3 atau melakukan perbuatan yang tecantum dalam Pasal 58 Angka 1, yaitu menjalankan usaha telekomunikasi tanpa izin atau beroperasi di luar ruang lingkup yang diizinkan, akan dikenakan rektifikasi oleh Kementerian Industri dan Teknologi Informasi, badan pengatur telekomunikasi provinsi, daerah otonom, atau kota madya, termasuk penyitaan pendapatan ilegal dan denda antara 3 hingga 5 kali pendapatan ilegal. Jika tidak ada pendapatan ilegal atau pendapatan ilegal tidak melebihi 50.000 RMB, denda antara 100.000 RMB dan 1.000.000 RMB. Untuk pelanggaran serius, perintah akan diberikan untuk menangguhkan bisnis untuk rektifikasi.
