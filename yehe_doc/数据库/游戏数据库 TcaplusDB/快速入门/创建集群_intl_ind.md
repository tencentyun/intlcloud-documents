## Ikhtisar
Dokumen ini menjelaskan cara membuat kluster TcaplusDB melalui konsol.

## Prasyarat
- Anda perlu [mendaftar](https://intl.cloud.tencent.com/document/product/378/17985) akun Tencent Cloud dan menyelesaikan [verifikasi identitas](https://intl.cloud.tencent.com/document/product/378/3629).

## Petunjuk
1. Masuk ke [TencentDB untuk konsol TcaplusDB](https://console.cloud.tencent.com/tcaplusdb/app), pilih **Cluster List** (Daftar Kluster) di bilah sisi kiri, dan klik **Create Cluster** (Buat Kluster).
2. Pada halaman pembelian yang ditampilkan, tentukan konfigurasi berikut, dan klik **Buy Now** (Beli Sekarang).
 - **Network** (Jaringan): pilih VPC dan subnet. Anda dapat memilih satu VPC dan satu subnet hanya saat membuat kluster yang tidak dapat dimodifikasi setelah dibuat.
 - **Connection Protocol** (Protokol Koneksi): pilih protokol koneksi (protokol deskripsi data).
 - **Cluster Name** (Nama Kluster): atur nama kluster dan ini harus unik berdasarkan akun dan dapat berisi 1-32 karakter. Anda dapat mengganti nama kluster kapan saja.
 - **Access Password** (Kata Sandi Akses): atur kata sandi akses kluster dan ini harus memenuhi persyaratan berikut:
	 - Panjang 8–64 karakter. Kata sandi sebaiknya 12 karakter atau lebih.
	 - Tidak boleh diawali dengan garis miring (/).
	 - Setidaknya mengandung tiga jenis:
	  - Huruf kecil (a-z)
	  - Huruf besar (A-Z)
	  - Angka (0-9)
	  - Simbol khusus `\~!@#$%^&*_-+=\|(){}[]:;'<>,.?/`.
 - **Table Group Name** (Nama Grup Tabel) dan **Table Group ID** (ID Grup Tabel): buat grup tabel default untuk kluster dan beri nama. ID grup tabel dapat dibuat atau disesuaikan secara otomatis.
![](https://qcloudimg.tencent-cloud.cn/raw/eebfcf5a907d248b8352b54865ccf235.png)
3. Kembali ke daftar kluster untuk melihat kluster dan grup tabel yang dibuat. Setiap kluster akan diberi ID kluster yang unik.
![](https://qcloudimg.tencent-cloud.cn/raw/0706ef01fd5983fdcfb7dcb67ab9e018.png)

