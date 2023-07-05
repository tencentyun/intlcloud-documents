
## Ikhtisar

Migrasi Layanan adalah platform yang dikembangkan oleh Tencent Cloud untuk membantu perusahaan memigrasikan sistem operasi, aplikasi, dan data aplikasi dari server sumber ke Cloud Virtual Machine (CVM) atau Cloud Block Storage (CBS). Migrasi ini membantu memenuhi kebutuhan perusahaan akan cloudifikasi, migrasi lintas cloud, migrasi lintas akun atau lintas wilayah, dan deployment cloud hibrida.

Migrasi layanan mencakup migrasi offline dan migrasi online. Migrasi offline meliputi:
- [Migrasi instans offline](#cvmStep) memungkinkan Anda memigrasi citra disk sistem ke CVM tertentu.
- [Migrasi data offline](#csmStep) memungkinkan Anda memigrasikan citra disk data ke CBS tertentu.

## Prasyarat

Migrasi offline memerlukan Cloud Object Storage (COS). Pastikan wilayah Anda didukung oleh COS.
Untuk informasi selengkapnya tentang wilayah yang didukung oleh COS, lihat [Wilayah dan Titik Akhir Akses](https://intl.cloud.tencent.com/document/product/436/6224).

## Persiapan

>! 
> - Saat ini, migrasi layanan Tencent Cloud mendukung citra dalam format qcow2, vhd, vmdk, dan mentah. Sebaiknya gunakan format citra terkompresi untuk mempersingkat waktu transmisi dan migrasi.
> - Wilayah COS tempat citra diunggah harus sama dengan tempat CVM yang ingin Anda migrasikan berada.
> - Selama migrasi offline, ukuran file citra yang diunggah tidak boleh lebih besar dari kapasitas disk yang ingin Anda migrasikan. Jika ukuran file citra adalah 50 GB, disk sistem harus setidaknya 50 GB.
> - Migrasi offline tidak mendukung snapshot (nama file mirip dengan \*-00000\*.vmdk).

 - Buat citra untuk server yang perlu dimigrasikan seperti yang diinstruksikan dalam dokumentasi pembuatan citra.
    - Untuk Windows, lihat [Menyiapkan Citra Windows](https://intl.cloud.tencent.com/document/product/213/17815).
    - Untuk Linux, lihat [Menyiapkan Citra Linux](https://intl.cloud.tencent.com/document/product/213/17814).
 - Unggah file citra yang dibuat ke COS.  
    - Karena file citra berukuran besar, unggah menggunakan browser mungkin gagal. Sebaiknya gunakan alat COSCMD untuk mengunggah citra. Untuk informasi selengkapnya, lihat [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).  
    - Jika citra yang diekspor dari platform cloud lain adalah paket terkompresi (seperti file .tar.gz), Anda dapat mengunggahnya langsung ke COS.
 - Dapatkan alamat COS dari citra yang diunggah.
Di [konsol COS](https://console.cloud.tencent.com/cos5/bucket), cari file citra yang baru saja Anda unggah dan lihat informasinya untuk mendapatkan tautan file.
 - Siapkan CVM atau CBS yang akan dimigrasikan.
[Klik di sini untuk membeli CVM >>](https://buy.cloud.tencent.com/cvm?tab=custom&step=1&regionId=8).
[Klik di sini untuk melihat petunjuk pembelian CBS >>](https://intl.cloud.tencent.com/document/product/362/32414).


## Petunjuk

<span id="cvmStep"></span>
### Migrasi instans offline

1. Login ke konsol CVM, lalu klik **[Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** ([Migrasi Layanan]) di bilah sisi kiri.
2. Klik **Create an instans migration task** (Buat tugas migrasi instans).
3. Selesaikan langkah-langkah persiapan seperti yang diminta, dan klik **Next** (Selanjutnya).
4. Pilih wilayah, masukkan informasi konfigurasi seperti nama tugas, tautan COS, dan instans CVM yang akan dimigrasikan. Kemudian, klik **Complete** (Selesai) untuk membuat tugas migrasi.
Selama migrasi, Anda dapat keluar atau menutup halaman [Migrasi Layanan](https://console.cloud.tencent.com/cvm/csm/index?rid=4). Anda juga dapat kembali ke halaman ini kapan saja untuk memeriksa kemajuan tugas. 
>!  
> - File COS harus dikonfigurasi dengan izin baca/tulis pribadi. Untuk informasi selengkapnya, lihat [Mengatur Izin Akses Objek](https://intl.cloud.tencent.com/document/product/436/13327).
> - Kapasitas disk sistem dari instans yang ingin Anda migrasikan tidak boleh kurang dari ukuran file citra yang diunggah. Jika tidak, tugas akan gagal.
> 

<span id="csmStep"></span>
### Migrasi data offline

1. Login ke konsol CVM, lalu klik **[Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** ([Migrasi Layanan]) di bilah sisi kiri.
2. Klik **Create a data migration task** (Buat tugas migrasi data).
3. Selesaikan langkah-langkah persiapan seperti yang diminta, dan klik **Next** (Selanjutnya).
4. Pilih wilayah, masukkan informasi konfigurasi seperti nama tugas, tautan COS, dan disk cloud yang akan dimigrasikan. Kemudian, klik **Complete** (Selesai) untuk membuat tugas migrasi.
Selama migrasi, Anda dapat keluar atau menutup halaman [Migrasi Layanan](https://console.cloud.tencent.com/cvm/csm/index?rid=4). Anda juga dapat kembali ke halaman ini kapan saja untuk memeriksa kemajuan tugas. 
>! Kapasitas disk CBS yang ingin Anda migrasikan tidak boleh kurang dari ukuran file citra yang diunggah. Jika tidak, tugas akan gagal.
>

## Pertanyaan Umum

Untuk informasi selengkapnya, lihat [Tentang Migrasi Layanan](https://intl.cloud.tencent.com/document/product/213/32395).






