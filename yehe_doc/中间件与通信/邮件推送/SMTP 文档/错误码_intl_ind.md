## Parameter Masukan
| Bidang | Deskripsi | Keterangan |
| ------------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Bcc | Alamat salinan karbon buta | Saat ini tidak didukung |
| Cc | Salin alamat | Saat ini tidak didukung |
| Pengkodean-Transfer-Konten | Metode pengkodean transfer konten | Saat ini tidak digunakan. Anda dapat membiarkannya kosong. Konten kecuali lampiran tidak perlu dienkripsi |
| Jenis-Konten | Jenis konten | Saat ini, Anda hanya dapat meneruskan `text/plain; charset=UTF-8,text/html; charset=UTF-8 multipart/mixed`, `multipart/related`, atau `multipart/alternative`; jika tidak, kesalahan akan dilaporkan |
| Tanggal | Tanggal dan waktu | Saat ini tidak digunakan |
| Dikirim-Ke | Alamat penerima | Saat ini tidak digunakan |
| Dari | Alamat pengirim | Diperlukan |
| ID Pesan | ID Pesan | Saat ini tidak digunakan |
| Versi MIME | Versi MIME | Saat ini tidak digunakan. Biarkan kosong atau teruskan dengan 1.0; jika tidak, kesalahan akan dilaporkan |
| Diterima | Jalur transfer | Saat ini tidak digunakan |
| Balas-Ke | Alamat balasan | Saat ini tidak digunakan |
| Jalur Kembali | Alamat balasan ke | Saat ini tidak digunakan |
| Subjek | Subjek | Diperlukan |
| Untuk | Alamat penerima | Diperlukan |

### Parameter lampiran (saat mengirim lampiran)
| Bidang | Deskripsi | Keterangan |
| ------------------------- | --------- | ------------------------------ |
| Jenis-Konten | Jenis konten | Kami sarankan Anda meneruskan `application/octet-stream` untuk file |
| Pengkodean-Transfer-Konten | Metode pengkodean transfer konten | Saat ini, hanya Base64 yang didukung, dan kesalahan akan dilaporkan jika Anda memasukkan nilai lain |
| Disposisi-Konten | Metode disposisi konten | Saat ini, Anda hanya dapat meneruskan `attachment`, dan lampiran tidak dapat dikirim jika Anda memasukkan nilai lain |
| ID-Konten | ID Konten | Saat ini tidak didukung |
| Konten-Lokasi | Lokasi konten (jalur) | Saat ini tidak didukung |
| Basis Konten | Lokasi basis konten | Saat ini tidak didukung |

>?Persyaratan verifikasi parameter input umumnya sama dengan [SendEmail](https://intl.cloud.tencent.com/document/product/1084/39408), termasuk pembatasan jumlah penerima, ukuran badan email, format lampiran, dan ukuran lampiran.

#### Parameter Respons
API SMTP tidak memiliki parameter respons dan hanya mendukung pengembalian informasi `err`. Jika `nil` dikembalikan, berarti panggilan API berhasil, tetapi pengiriman email yang sebenarnya mungkin belum tentu berhasil. Untuk mendapatkan status pengiriman, lihat [GetSendEmailStatus](https://intl.cloud.tencent.com/document/product/1084 /39502).

## Kode Kesalahan
### Kesalahan sistem
1. Ada 2.000 karakter atau lebih dalam satu baris di badan email.
`554 5.0.0 Error: transaction failed, blame it on the weather: smtp: too longer line in input stream` atau log lainnya yang memuat frasa `too longer`.
`write tcp *.*.*.*:60575->*.*.*.*:25: write: broken pipe`

2. Lampiran terlalu besar.
Jika lampiran berukuran sekitar 9 MB, EOF akan dikembalikan. Kamisarankan Anda menjaga ukuran lampiran total di bawah 8 MB dan menjaga ukuran pesan total di bawah 10 MB. Jika tidak, konten akan terpotong, dan kesalahan pengecualian lainnya seperti kegagalan decoding Base64 akan dilaporkan.
				
### Kesalahan bisnis
Format kesalahan bisnis adalah sebagai berikut:
`
554 5.0.0 Error: transaction failed, blame it on the weather: ##SES-response-json: {"Response":{"RequestId":"bee4e9fb-8127-48cc-b606-bbb1e801596b","QcloudError":{"Error":{"Code":"FailedOperation.MissingEmailContent. Operasi gagal. Isi email tidak ada (`TemplateData` dan `Simple` tidak boleh kosong).
`
 Setelah `##SES-response-json:` adalah bentuk `json` dari struktur yang dikembalikan oleh API pengirim. Bidang dijelaskan sebagai berikut:

| Bidang | Jenis | Deskripsi |
| ----------- | ------ | ----- |
| RequestId | string | ID Permintaan | 
| QcloudError | stuct | Struktur kesalahan | 

QcloudError:

| Bidang | Jenis | Deskripsi | 
| ----------- | ------ | ----- | 
| Kode | string | Kode kesalahan | 
| Pesan | string | Pesan kesalahan | 



Deskripsi kesalahan bisnis umum:

| Kode Kesalahan | Deskripsi Kesalahan | Keterangan |
| ---------------------------------- | ------------------------------------------------------------------ | ------------------------------------- |
| FailedOperation | msg.From is null | Pengirim kosong |
| FailedOperation | msg.Subject is null | Subjek kosong |
| FailedOperation | msg.Body is null | Isi pesan kosong |
| FailedOperation | Pengkodean-Transfer-Konten harus dalam... | Periksa parameter `Content-Transfer-Encoding` terhadap deskripsi parameter masukan |
| FailedOperation | Jenis Konten harus dalam... | Periksa parameter `Content-Type` pada header berdasarkan deskripsi parameter masukan |
| FailedOperation | Mime-Version harus dalam... | Periksa parameter `Mime-Version` pada header berdasarkan deskripsi parameter masukan |
| FailedOperation | Email terlalu besar. Hapus beberapa konten... | Badan email selain lampiran tidak boleh lebih dari 1 MB |
| FailedOperation | Konten lampiran salah. Pastikan konten base64 adalah... | Konten lampiran harus dikodekan dengan Base64 |
| FailedOperation | Email terlalu besar. Pastikan tidak melebihi... | Ukuran satu lampiran melebihi 5 MB, atau ukuran total semua lampiran melebihi 10 MB (yang dapat disesuaikan) |
| RequestLimitExceeded.SmtpRateLimit | batas frekuensi pengiriman smtp... | Batas laju panggilan SMTP tercapai |

### Kesalahan bisnis lainnya
Anda dapat merujuk ke deskripsi kode kesalahan di [SendEmail](https://intl.cloud.tencent.com/document/product/1084/39408).
