## Skenario Operasi 
Dokumen ini menjelaskan cara membuat cadangan tabel di Konsol TcaplusDB.

## Prasyarat
Anda telah membuat tabel. Untuk informasi selengkapnya, silakan lihat [Membuat Tabel](https://intl.cloud.tencent.com/document/product/1016/32715).

## Petunjuk
### Pencadangan otomatis
TcaplusDB secara otomatis mencadangkan tabel pada pukul 01.00 (waktu Beijing) setiap hari, dan data cadangan akan disimpan selama 7 hari, setelah itu akan dihapus secara otomatis.

### Pencadangan manual
Jika Anda ingin mencadangkan tabel secara manual, Anda dapat melakukannya di konsol.
**Method 1:** (Metode 1:)
1. Masuk ke halaman [Daftar Tabel](https://console.cloud.tencent.com/tcaplusdb/table), pilih tabel target dan klik **More** (Lainnya) > **Back up** (Cadangkan) di kolom "Operasi", atau pilih beberapa tabel dan klik **Batch Backup** (Cadangkan Massal) di atas.
2. Di kotak dialog cadangan pop-up, masukkan komentar dan klik **Confirm** (Konfirmasi) untuk mencadangkan tabel yang dipilih.

**Method 2:** (Metode 2:)
Masuk ke halaman [Daftar Tabel](https://console.cloud.tencent.com/tcaplusdb/table), klik ID tabel untuk masuk ke halaman detail tabel, dan klik **Manual Backup** (Cadangkan Manual) di sudut kanan atas untuk membuat cadangan tabel.

