Selain [membuat citra kustom](https://intl.cloud.tencent.com/document/product/213/4942), Tencent Cloud memungkinkan Anda mengimpor citra. Anda dapat mengimpor file citra dari disk sistem di server lokal atau lainnya ke dalam citra kustom CVM. Anda dapat menggunakan citra yang diimpor untuk membuat CVM atau menginstal ulang sistem operasi untuk CVM yang ada.

<span id="Preparations"></span>
## Persiapan

Siapkan file citra yang memenuhi persyaratan impor.
- **Requirements for Linux images:** (Persyaratan untuk citra Linux:)
<table>
<tr><th style="width:16%">Atribut Citra</th><th>Persyaratan</th></tr>
<tr><td>OS</td><td><ul><li>CentOS, Ubuntu, Debian, CoreOS, OpenSUSE, dan SUSE</li><li>OS 32-bit dan 64-bit didukung.</li></ul></td></tr>
<tr><td>Format citra</td><td><ul><li>RAW, VHD, QCOW2, dan VMDK</li><li>Jalankan <code>qemu-img info imageName | grep 'file format'</code> untuk memeriksa format citra.</li></ul></td></tr>
<tr><td>Jenis sistem file</td><td>Partisi GPT tidak didukung.</td></tr>
<tr><td>Ukuran citra</td><td><ul><li>Ukuran citra sebenarnya tidak boleh melebihi 50 GB. Jalankan <code>qemu-img info imageName | grep 'disk size'</code> untuk memeriksa ukuran citra.</li><li>Ukuran citra tidak boleh melebihi 500 GB. Jalankan <code>qemu-img info imageName | grep 'virtual size'</code> untuk memeriksa ukuran citra.</li></ul><b>Catatan: </b>ukuran citra dalam format QCOW2 digunakan saat pemeriksaan selama impor.</td></tr>
<tr><td>Jaringan</td><td><ul><li>Secara default, Tencent Cloud menyediakan antarmuka jaringan <code>eth0</code> untuk instans.</li><li>Anda dapat menggunakan metadata layanan untuk mengkueri konfigurasi jaringan instans. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/4934">Metadata Instans</a>.</li></ul></td></tr>
<tr><td>Driver</td><td><ul><li>Driver virtio dari modul virtualisasi KVM harus diinstal untuk satu citra. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/9929">Memeriksa Driver Virtio di Linux</a>.</li><li>Sebaiknya menginstal cloud-init untuk citra tersebut. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/12587">Menginstal Cloud-Init di Linux</a>. </li><li>Jika cloud-init tidak dapat diinstal, konfigurasikan instans dengan melihat <a href="https://intl.cloud.tencent.com/document/product/213/12849">Mengimpor Citra Secara Paksa</a>.</li></ul></td></tr>
<tr><td>Kernel</td><td>Kernel native lebih disarankan untuk citra. Modifikasi apa pun pada kernel dapat menyebabkan kegagalan impor.</td></tr>
<tr><td>Wilayah</td><td>Mengimpor citra dari COS di wilayah lain tidak tersedia untuk Shanghai Finance dan Shenzhen Finance.</td></tr>
</table>
- **Requirements for Windows images:** (Persyaratan untuk citra Windows:)
<table>
<tr><th style="width:16%">Atribut Citra</th><th>Persyaratan</th></tr>
<tr><td>OS</td><td><ul><li>Versi terkait Windows Server 2008, Windows Server 2012, dan Windows Server 2016</li><li>OS 32-bit dan 64-bit didukung.</li></ul></td></tr>
<tr><td>Format citra</td><td><ul><li>RAW, VHD, QCOW2, dan VMDK</li><li>Jalankan <code>qemu-img info imageName | grep 'file format'</code> untuk memeriksa format citra.</li></ul></td></tr>
<tr><td>Jenis sistem file</td><td><ul><li>Hanya NTFS dengan partisi MBR yang didukung.</li><li>Partisi GPT tidak didukung.</li><li>Logical Volume Manager (LVM) tidak didukung.</li></ul></td></tr>
<tr><td>Ukuran citra</td><td><ul><li>Ukuran citra sebenarnya tidak boleh melebihi 50 GB. Jalankan <code>qemu-img info imageName | grep 'disk size'</code> untuk memeriksa ukuran citra.</li><li>Ukuran citra tidak boleh melebihi 500 GB. Jalankan <code>qemu-img info imageName | grep 'virtual size'</code> untuk memeriksa ukuran citra.</li></ul><b>Catatan: </b>ukuran citra dalam format QCOW2 digunakan saat pemeriksaan selama impor.</td></tr>
<tr><td>Jaringan</td><td><ul><li>Secara default, Tencent Cloud menyediakan antarmuka jaringan <code>koneksi area lokal</code> untuk instans. </li><li>Anda dapat menggunakan layanan metadata untuk mengkueri konfigurasi jaringan instans. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/4934">Metadata Instans</a>.</li></ul></td></tr>
<tr><td>Driver</td><td>Driver Virtio dari modul virtualisasi KVM harus diinstal untuk satu citra. Sistem Windows tidak dilengkapi dengan driver Virtio secara default, jadi harap menginstal driver Windows Virtio terlebih dahulu sebelum mengekspor citra lokal. Pilih alamat pengunduhan berdasarkan lingkungan jaringan:<ul><li>Alamat pengunduhan Internet:<code>http://mirrors.tencent.com/install/windows/virtio_64_1.0.9.exe</code></li><li>Alamat pengunduhan jaringan pribadi:<code>http://mirrors.tencentyun.com/install/windows/virtio_64_1.0.9.exe</code></li></ul></td></tr>
<tr><td>Wilayah</td><td>Mengimpor citra dari COS di wilayah lain tidak tersedia untuk Shanghai Finance dan Shenzhen Finance.</td></tr>
<tr><td>Lainnya</td><td>Citra Windows yang diimpor <b>tidak mendukung </b><a href="https://intl.cloud.tencent.com/document/product/213/2757">aktivasi sistem Windows</a>.</td></tr>
</table>

## Petunjuk

 1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm/).
 2. Di bilah sisi kiri, klik **[Images](https://console.cloud.tencent.com/cvm/image)** (Citra).
 3. Pilih **Custom Image** (Citra Kustom), lalu klik **Import Image** (Impor Citra).
 4. [Aktifkan Cloud Object Storage](https://console.cloud.tencent.com/cos4/index), lalu [buat bucket](/doc/product/436/6232). Unggah file citra ke bucket dan dapatkan [URL file citra](/doc/product/436/6260).
 5. Klik **Next** (Selanjutnya).
 6. Selesaikan konfigurasi, alu klik **Import** (Impor).
 >! Pastikan URL file COS yang dimasukkan sudah benar.
 >
Anda akan diberi tahu tentang hasil impor melalui konsol [Pusat Pesan](https://console.cloud.tencent.com/message).

## Impor yang Gagal

Jika pengimporan gagal, pecahkan masalah dengan cara sebagai berikut:

### Catatan

Pastikan Anda telah berlangganan pemberitahuan layanan produk melalui [Langganan Pesan](https://console.cloud.tencent.com/messageCenter/messageConfig). Tindakan ini memastikan Anda dapat menerima pesan internal, pesan SMS, dan email tentang penyebab kegagalan.
>! Jika Anda tidak berlangganan pemberitahuan layanan produk, Anda tidak akan menerima pesan internal tentang apakah impor berhasil.

### Pemecahan Masalah

Untuk informasi selengkapnya tentang pesan kesalahan dan deskripsi, lihat [Kode Kesalahan](#errorcode).

#### InvalidUrl: URL COS tidak valid

Kesalahan InvalidUrl menunjukkan bahwa telah memasukkan URL COS yang salah. Kemungkinan penyebabnya adalah:
* URL citra yang Anda masukkan bukan URL citra [Cloud Object Storage](https://console.cloud.tencent.com/cos4/index).
* Izin URL COS bukan untuk pembacaan publik dan penulisan pribadi.
* Izin akses file COS dibaca secara pribadi, tetapi tanda tangannya telah kedaluwarsa.
>! URL COS dengan tanda tangan hanya dapat diakses satu kali.
>
* URL COS dari wilayah lain telah dimasukkan.
>! Layanan impor citra mengakses server COS di wilayah lokal melalui jaringan pribadi.
>
* File citra pengguna telah dihapus.
* URL COS dengan tanda tangan telah digunakan.
Jika Anda menerima pesan kesalahan tentang URL COS yang tidak valid, pecahkan masalah berdasarkan alasan di atas.

#### InvalidFormatSize: format atau ukuran tidak valid

Kesalahan InvalidFormatSize menunjukkan bahwa format atau ukuran citra yang akan diimpor tidak memenuhi persyaratan Tencent Cloud berikut:
* Format file citra yang didukung adalah `qcow2`,` vhd`, `vmdk`, dan`raw`.
* Ukuran file citra yang akan diimpor tidak boleh melebihi 50 GB (berdasarkan ukuran dalam format qcow2).
* Ukuran disk sistem tempat citra diimpor tidak boleh melebihi 500 GB.

Jika Anda menerima pesan kesalahan bahwa format atau ukuran citra tidak valid:
- Ubah file citra menjadi format yang sesuai menurut [Pembuatan Citra Linux](https://intl.cloud.tencent.com/document/product/213/17814), kurangi konten citra untuk memenuhi persyaratan ukuran, lalu impor ulang.
- Anda juga dapat menggunakan fitur [migrasi instans offline](https://intl.cloud.tencent.com/document/product/213/19233) untuk memigrasikan instans. Fitur ini mendukung migrasi file citra hingga 500 GB.

#### VirtioNotInstall: Driver Virtio tidak diinstal

Kesalahan VirtioNotInstall menunjukkan bahwa citra yang akan diimpor tidak menginstal driver Virtio. Tencent Cloud menggunakan teknologi virtualisasi KVM dan mengharuskan pengguna untuk menginstal driver Virtio pada citra yang akan diimpor. Kecuali untuk beberapa OS Linux yang disesuaikan, sebagian besar OS Linux telah menginstal driver Virtio. Di OS Windows, pengguna perlu menginstal driver Virtio secara manual:
- Untuk impor citra Linux, harap lihat [Memeriksa Driver Virtio di Linux](https://intl.cloud.tencent.com/document/product/213/9929).
- Untuk impor citra Windows, lihat [Pembuatan Citra Windows](https://intl.cloud.tencent.com/document/product/213/17815) untuk menginstal driver Virtio.

#### CloudInitNotInstalled: program cloud-init tidak diinstal

Kesalahan CloudInitNotInstalled menunjukkan bahwa citra yang akan diimpor tidak menginstal cloud-init. Tencent Cloud menggunakan perangkat lunak cloud-init sumber terbuka untuk menginisialisasi CVM. Jika cloud-init tidak diinstal, inisialisasi CVM akan gagal.
* Untuk impor citra Linux, lihat [Menginstal Cloud-Init di Linux](https://intl.cloud.tencent.com/document/product/213/12587).
* Untuk impor citra Windows, lihat [Menginstal Cloudbase-Init di Windows](https://intl.cloud.tencent.com/document/product/213/32364).
* Setelah cloud-init atau cloudbase-init diinstal, ganti file konfigurasi berdasarkan dokumen yang sesuai sehingga CVM dapat menarik data dari sumber data yang benar saat startup.

#### PartitionNotPresent: informasi partisi tidak ditemukan

Kesalahan PartitionNotPresent menunjukkan bahwa citra yang diimpor tidak lengkap. Periksa apakah partisi boot disertakan saat citra dibuat.

#### RootPartitionNotFound: partisi root tidak ditemukan

Kesalahan RootPartitionNotFound menunjukkan bahwa partisi root tidak dapat dideteksi pada citra yang akan diimpor. Periksa file citra. Kemungkinan penyebabnya adalah:
* Paket penginstalan telah diunggah.
* Citra disk data telah diunggah.
* Citra partisi boot telah diunggah.
* File yang salah diunggah.

#### InternalError: kesalahan yang tidak diketahui

Kesalahan InternalError menunjukkan bahwa sebab kesalahan belum dicatat. Hubungi layanan pelanggan, kemudian tenaga teknis kami akan membantu Anda mengatasi masalah tersebut.

<a id="errorcode"></a>
## Kode Kesalahan
 
| Kode Kesalahan | Alasan | Solusi yang Direkomendasikan |
|-----|-----|-----|
| InvalidUrl | Tautan COS tidak valid. | Periksa apakah URL COS sama dengan URL citra yang diimpor. |
| InvalidFormatSize | Format atau ukuran tidak memenuhi persyaratan. | Citra harus memenuhi persyaratan `image format` dan `image size` di [Persiapan](#PreparationsforImport). |
| VirtioNotInstall | Driver Virtio tidak diinstal. | Instal driver Virtio pada citra dengan merujuk ke bagian `Driver` di [Persiapan](#PreparationsforImport). |
| PartitionNotPresent | Informasi partisi tidak ditemukan. | Citra rusak mungkin karena metode pembuatan citra yang salah. |
| CloudInitNotInstalled | Perangkat lunak cloud-init tidak diinstal. | Instal cloud-init di citra Linux dengan merujuk ke bagian `Driver` di [Persiapan](#PreparationsforImport). |
| RootPartitionNotFound | Partisi root tidak ditemukan. | Citra rusak mungkin karena metode pembuatan citra yang salah. |
| InternalError | kesalahan lainnya. | Hubungi layanan pelanggan kami. |

