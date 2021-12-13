## Ikhtisar
Anda dapat menggunakan cira kustom untuk membuat instans CVM dari sistem operasi, aplikasi, dan data yang sama untuk meningkatkan efisiensi. Dokumen ini memandu Anda melalui cara membuat instans menggunakan citra kustom.


## Prasyarat
Anda harus memiliki citra kustom di bawah akun Anda dan di wilayah tempat Anda ingin membuat instans.
Jika tidak ada citra kustom, lihat solusi berikut:
<table>
	<tr><th>Status Citra</th><th>Solusi</th></tr>
	<tr><td>Citra di komputer lokal atau platform lain</td><td>Impor citra disk sistem di komputer lokal atau platform lain ke citra kustom di CVM. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/4945">Ikhtisar</a>.</td></tr>
	<tr><td>Ada instans templat tetapi tidak ada citra kustom</td><td>Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/4942">Membuat Citra Kustom</a>.</td></tr>
	<tr><td>Citra kustom di wilayah lain</td><td>Salin citra kustom ke wilayah target tempat Anda ingin membuat instans. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/4943">Menyalin Citra</a>.</td></tr>
	<tr><td>Citra kustom di bawah akun lain</td><td>Bagikan citra kustom dengan akun tempat Anda ingin membuat instans. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/4944">Membagikan Citra Kustom</a>.</td></tr>
</table>

## Petunjuk

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/instance/index?rid=1).
2. Klik **Images** (Citra) di bilah sisi kiri untuk mengakses halaman **Image** (Citra).
3. Pilih wilayah di bagian atas halaman **Image** (Citra).
4. Pilih tab berdasarkan sumber citra untuk melihat daftar citranya.
 - **Public Image** (Citra Publik): buka halaman citra publik.
 - **Custom Image** (Citra Kustom): buka halaman citra kustom.
 - **Shared Image** (Citra Bersama): buka halaman citra bersama.
5. Di bawah kolom **Operation** (Operasi) dari citra yang ingin Anda gunakan, klik **Create Instance** (Buat Instans).
![](https://main.qcloudimg.com/raw/4c5806f49da53595d31ad07662bf363a.png)
6. Di jendela pop-up, klik **OK** (OKE).
7. Konfigurasikan dan buat instans seperti yang diminta oleh halaman.
Kolom **Region** (Wilayah) dan **Image** (Citra) otomatis akan terisi. Selesaikan konfigurasi instans lainnya sesuai kebutuhan. Untuk informasi selengkapnya, lihat [Membuat Instans melalui Halaman Pembelian CVM](https://intl.cloud.tencent.com/document/product/213/4855).
> Jika Anda menggunakan citra kustom yang berisi satu atau beberapa snapshot disk data, sistem operasi akan secara otomatis membuat jumlah Cloud Block Storage (CBS) yang sama sebagai snapshot dan kapasitas yang sama dengan setiap snapshot. Anda dapat memperluas, tetapi tidak dapat mengurangi, kapasitas CBS.
>

## Dokumentasi Terkait

Anda juga dapat membuat citra kustom menggunakan RunInstances API. Untuk informasi selengkapnya, lihat [RunInstances](https://intl.cloud.tencent.com/document/product/213/33237)
