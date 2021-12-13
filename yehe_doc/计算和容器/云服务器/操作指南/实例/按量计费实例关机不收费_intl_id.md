## Ikhtisar
Jika Anda mengaktifkan "Tanpa Biaya saat Pematian" saat menonaktifkan instans bayar sesuai pemakaian, penagihan sumber daya CPU dan memori instans ini akan berhenti. Namun, disk Cloud (disk sistem dan disk data), bandwidth jaringan publik, citra, dan komponen utama lainnya dari instans CVM dikenakan biaya.
>! Saat fitur ini diaktifkan, sumber daya CPU dan memori instans **will not be retained** (tidak akan dipertahankan), dan alamat IP publik **will be automatically released** (akan dirilis secara otomatis) setelah dinonaktifkan. Untuk informasi selengkapnya tentang fitur, batas penggunaannya, dan dampaknya, lihat [Tanpa Biaya Saat Pematian untuk Instans Bayar Sesuai Pemakaian](https://intl.cloud.tencent.com/document/product/213/19918).

## Petunjuk
### Mematikan instans melalui konsol
1. Login ke [konsol CVM](https://console.cloud.tencent.com/cvm).
2. Pilih metode operasi yang sesuai berdasarkan kebutuhan Anda yang sebenarnya.
 - Mematikan satu instans:
    1. Pilih instans yang ingin dimatikan, lalu klik **More** (Lainnya) > **Instance Status** (Status Instans) > **Shut down** (Matikan) di bawah kolom **Operation** (Operasi) di sebelah kanan.
    2. Centang **CVM No Charge when Shut down** (CVM Tanpa Biaya saat Pematian), lalu klik **OK** (OKE).
    Jika instans tidak mendukung fitur ini, **"No Charge when Shut Down" is not supported** (("CVM Tanpa Biaya saat Mematikan" tidak didukung)) akan ditampilkan dalam daftar instans.
 - Mematikan beberapa instans:
    1. Pilih semua instans yang ingin Anda matikan, lalu klik **Shut down** (Matikan) di bagian atas daftar untuk mematikan instans dalam batch.
    Alasan diberikan untuk instans yang tidak dapat dionaktifkan.
	 2. Centang **CVM No Charge when Shut down** (CVM Tanpa Biaya saat Pematian), lalu klik **OK** (OKE).
		Jika instans tidak mendukung fitur ini, **"No Charge when Shut Down" is not supported** (("CVM Tanpa Biaya saat Mematikan" tidak didukung)) akan ditampilkan dalam daftar instans.

### Mematikan instans melalui API
Anda dapat menggunakan `StopInstances` API untuk mematikan instans. Untuk detailnya, harap lihat [StopInstances](https://intl.cloud.tencent.com/document/product/213/33235). Untuk mengaktifkan fitur ini melalui API, tambahkan parameter berikut:

| Nama Parameter | Wajib | Jenis | Deskripsi |
| ----------- | ---- | ------ | ------------------------------------------------------------ |
| Mode Berhenti | Tidak | String |Fitur "Tanpa Biaya saat Pematian" hanya tersedia untuk instans bayar sesuai pemakaian.<br>**Valid values:** (Nilai yang valid:)<br>KEEP_CHARGING: instans dikenakan biaya setelah pematian<br>STOP_CHARGING: tanpa biaya saat pematian<br>**Default value:** (Nilai default:)<br>KEEP_CHARGING |



