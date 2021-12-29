## 1.Dasar CBS
- [Ikhtisar](https://intl.cloud.tencent.com/document/product/362/2345)
- [Keunggulan Produk](https://intl.cloud.tencent.com/document/product/362/3039)
- [Jenis Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31636)
- [Kasus Penggunaan](https://intl.cloud.tencent.com/document/product/362/3065)
- [Batas Penggunaan](https://intl.cloud.tencent.com/document/product/362/32406)

## 2.Cara Penagihan CBS
Tencent Cloud CBS mendukung cara penagihan **monthly subscription** (langganan bulanan) dan **pay-as-you-go** (pembayaran sesuai pemakaian).Anda perlu memahami kedua cara penagihan tersebut untuk memilih solusi penagihan yang optimal.Untuk informasi selengkapnya, lihat [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/362/32415).

## 3.Snapshot
Snapshot adalah metode perlindungan data yang nyaman dan efisien.Sebaiknya Anda membuat snapshot untuk disk cloud sebelum melakukan perubahan bisnis besar.Snapshot dapat digunakan untuk memulihkan data dengan cepat jika perubahan bisnis yang dilakukan gagal.Untuk informasi selengkapnya, lihat [(Ikhtisar Snapshot](https://intl.cloud.tencent.com/document/product/362/31638).


## 4.Memulai
#### 4.1 Pendaftaran dan autentikasi
Sebelum menggunakan Tencent Cloud CBS, daftar untuk membuat [Akun Tencent Cloud](https://intl.cloud.tencent.com/register?s_url=https%3A%2F%2Fcloud.tencent.com%2F) dan selesaikan [verifikasi identitas](https://intl.cloud.tencent.com/document/product/378/3629).

#### 4.2 Membuat disk cloud
Setelah pendaftaran dan verifikasi identitas, Anda dapat memilih jenis disk cloud, kapasitas, cara penagihan, periode penyimpanan, perpanjangan otomatis, dan waktu kedaluwarsa, atau perlindungan kedaluwarsa atau tunggakan berdasarkan persyaratan zona ketersediaan tempat CVM Anda berada untuk membuat disk cloud.Untuk informasi selengkapnya, lihat [Membuat Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31647).

#### 4.3 Menggunakan disk cloud
Setelah membuat disk cloud, Anda perlu memasang secara terpisah disk cloud yang dibeli ke CVM di zona ketersediaan yang sama dan menginisialisasi disk cloud tersebut.Untuk informasi selengkapnya, baca dokumen berikut:
- [Memasang Disk Cloud](https://intl.cloud.tencent.com/document/product/362/39991)
- [Menginisialisasi Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31645)

#### 4.4 Membuat snapshot (opsional)
Setelah membuat disk cloud, Anda dapat menggunakan snapshot untuk mencadangkan data bisnis penting secara manual atau berkala untuk mencegah kehilangan atau kerusakan data akibat kesalahan pengoperasian, serangan, virus, atau hal lainnya.Untuk informasi selengkapnya, lihat [Membuat Snapshot](https://intl.cloud.tencent.com/document/product/362/5755) dan [Snapshot Terjadwal](https://intl.cloud.tencent.com/document/product/362/35238).



## 5.Ikhtisar Fitur Konsol

| Fitur | Referensi |
|---------|---------|
| Buat disk cloud menggunakan cara lain.| [Membuat Disk Cloud](https://intl.cloud.tencent.com/document/product/362/5744) |
| Pasang disk cloud ke CVM di zona ketersediaan yang sama dan atur pemasangan disk cloud otomatis.| [Memasang Disk Cloud](https://intl.cloud.tencent.com/document/product/362/32401) |
| Inisialisasi disk cloud berdasarkan kebutuhan yang sebenarnya.| [Skenario Inisialisasi](https://intl.cloud.tencent.com/document/product/362/31596) |
| Perluas disk cloud untuk menambah ruang penyimpanan.| [Skenario Perluasan Disk Cloud](https://intl.cloud.tencent.com/document/product/362/31600) |
| Lepas disk cloud dan pasang ke CVM lain.| [Melepas Disk Cloud](https://intl.cloud.tencent.com/document/product/362/32400) |
| Hentikan atau kembalikan disk cloud.| [Menghentikan disk cloud](https://intl.cloud.tencent.com/document/product/362/32399) |
| Buatlah snapshot disk cloud pada titik waktu tertentu untuk menyimpan data disk cloud pada waktu tersebut.| [Membuat Snapshot](https://intl.cloud.tencent.com/document/product/362/5755) |
| Gunakan kebijakan snapshot terjadwal untuk mencadangkan data secara fleksibel.| [Snapshot Terjadwal](https://intl.cloud.tencent.com/document/product/362/35238) |
| Hapus snapshot yang tidak diperlukan.| [Menghapus Snapshot](https://intl.cloud.tencent.com/document/product/362/5758) |
| Lakukan rollback (pemulihan) pada disk cloud menggunakan snapshot untuk memulihkan data ke waktu pembuatan snapshot.| [Mengembalikan Menggunakan Snapshot](https://intl.cloud.tencent.com/document/product/362/5756) |

## 6.Pertanyaan Umum
#### Penggunaan CBS
- [Apa saja skenario yang berlaku untuk berbagai jenis disk cloud?](https://intl.cloud.tencent.com/document/product/362/32409)
- [Bagaimana cara melihat detail disk cloud?](https://intl.cloud.tencent.com/document/product/362/32409#.E5.A6.82.E4.BD.95.E6.9F.A5.E7.9C.8B.E4.BA.91.E7.A1.AC.E7.9B.98.E8.AF.A6.E7.BB.86.E4.BF.A1.E6.81.AF.EF.BC.9F)
- [Bisakah satu disk cloud diakses oleh beberapa CVM?](https://intl.cloud.tencent.com/document/product/362/32409#.E6.98.AF.E5.90.A6.E6.94.AF.E6.8C.81.E5.A4.9A.E4.B8.AA.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8.E8.AE.BF.E9.97.AE.E5.90.8C.E4.B8.80.E5.9D.97.E4.BA.91.E7.A1.AC.E7.9B.98.EF.BC.9F)
- [Mengapa disk cloud yang saya buat secara terpisah dirilis bersama dengan instance saya?](https://intl.cloud.tencent.com/document/product/362/32409#.E4.B8.BA.E4.BB.80.E4.B9.88.E6.88.91.E5.8D.95.E7.8B.AC.E5.88.9B.E5.BB.BA.E7.9A.84.E4.BA.91.E7.A1.AC.E7.9B.98.E5.92.8C.E6.88.91.E7.9A.84.E5.AE.9E.E4.BE.8B.E4.B8.80.E8.B5.B7.E9.87.8A.E6.94.BE.E4.BA.86.EF.BC.9F)
- [Bisakah saya mengubah jenis disk cloud setelah pembelian?](https://intl.cloud.tencent.com/document/product/362/32409#.E5.9C.A8.E6.88.90.E5.8A.9F.E8.B4.AD.E4.B9.B0.E5.90.8E.EF.BC.8C.E6.98.AF.E5.90.A6.E6.94.AF.E6.8C.81.E6.9B.B4.E6.8D.A2.E4.BA.91.E7.A1.AC.E7.9B.98.E7.9A.84.E7.B1.BB.E5.9E.8B.EF.BC.9F)
- [Bisakah disk sistem saya dipartisi?](https://intl.cloud.tencent.com/document/product/362/32409#.E7.B3.BB.E7.BB.9F.E7.9B.98.E8.83.BD.E5.90.A6.E8.BF.9B.E8.A1.8C.E5.88.86.E5.8C.BA.E6.93.8D.E4.BD.9C.EF.BC.9F)


#### Pertanyaan Umum Snapshot
- [Apa perbedaan snapshot dan image?](https://intl.cloud.tencent.com/document/product/362/17820)
- [Mengapa saya tidak bisa menghapus snapshot?](https://intl.cloud.tencent.com/document/product/362/17820)
- [Apakah saya perlu mematikan CVM untuk melakukan roll back (pengembalian) menggunakan snapshot?](https://intl.cloud.tencent.com/document/product/362/17820)
- [Ketika saya menghentikan disk cloud, apakah snapshot terkaitnya akan ikut terhapus juga?](https://intl.cloud.tencent.com/document/product/362/17820)


## 7.Masukan dan Saran
Jika memiliki keraguan atau saran saat menggunakan produk dan layanan Tencent Cloud CBS, Anda dapat mengirimkan masukan Anda melalui saluran berikut.Staf yang berdedikasi akan menghubungi Anda untuk memecahkan masalah Anda.

- Jika Anda menemui masalah dokumentasi produk, seperti eror pada tautan, konten, atau API, Anda dapat mengeklik **Send Feedback** (Kirim Masukan) di bagian bawah dokumen untuk memilih konten yang bermasalah.
- Jika Anda mengalami masalah terkait produk, silakan [kirim tiket](https://console.cloud.tencent.com/workorder/category) untuk meminta bantuan.
