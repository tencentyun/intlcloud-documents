Cloud Connect Network (CCN) menjembatani VPC Tencent Cloud dan antara VPC dan IDC lokal. Ini memberi Anda interkoneksi jaringan pribadi multipoint. Untuk memanfaatkan fitur CCN ini, Anda harus terlebih dahulu menambahkan VPC ke CCN. Dokumen ini menjelaskan cara menghubungkan VPC dengan atau memutuskan koneksinya dari CCN.

## Menghubungkan dengan CCN
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih wilayah VPC di bagian atas halaman **VPC**.
3. Klik ID VPC untuk mengakses halaman **Basic Information** (Informasi Dasar).
4. Klik **Associate Now** (Hubungkan Sekarang) di bagian **Associate with CCN** (Hubungkan dengan CCN) untuk membuka kotak dialog **Associate with CCN** (Hubungkan dengan CCN).

5. Konfigurasikan parameter sebagai berikut.

	+ **Account** (Akun): akun pemilik instans CCN. Instans VPC dan CCN dapat berada di bawah akun yang sama atau berbeda. Jika Anda memilih **Other accounts** (Akun lain), masukkan **Account ID** (ID Akun). Pemilik akun harus menerima permohonan CCN dalam waktu 7 hari, jika tidak, permohonan akan kedaluwarsa. Pemilik CCN menanggung biaya interkoneksi jaringan yang dihasilkan oleh instans yang terhubung ke CCN.
	+ **CCN ID** (ID CCN): pilih ID CCN dari daftar pilihan untuk **My Account** (Akun Saya) atau masukkan ID CCN untuk **Other accounts** (Akun lain). 
6. Klik **OK** (Oke). Maka statusnya akan menjadi **Connected** (Terhubung) seperti ditampilkan gambar di bawah ini.

		
## Pemutusan koneksi dari CCN
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih wilayah VPC di bagian atas halaman **VPC**.
3. Temukan VPC yang akan diputuskan koneksinya dari CCN, dan klik ID VPC untuk mengakses halaman **Basic Information** (Informasi Dasar).
4. Klik **Disassociate** (Putuskan koneksi) di bagian **Associate with CCN** (Hubungkan dengan CCN).

5. Periksa kembali dan konfirmasikan risiko operasi dan klik **Disassociate** (Putuskan koneksi).


## Operasi yang Relevan
[Interkoneksi Instans Jaringan dalam Satu Akun](https://intl.cloud.tencent.com/document/product/1003/31986)
[Akun Lintas Interkoneksi Instans Jaringan](https://intl.cloud.tencent.com/document/product/1003/31987)
