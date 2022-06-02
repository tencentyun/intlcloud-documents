Tencent Cloud akan memberi tahu alamat panggilan balik tentang keberhasilan pengiriman, kegagalan pengiriman, email terpental, email terbuka, klik tautan, berhenti berlangganan, dan peristiwa lainnya. Format protokol push peristiwa adalah sebagai berikut:
## Contoh Permintaan
```json
{
  "event": "delivered",
  "email": "example@example.com",
  "bulkId": "qcloud-ses-4F001945B2D9BXXXXXX",
  "timestamp": 1587953211,
  "reason": "the reason when email failed to delivered",
  "bounceType": ""
}
```

Bidang | Jenis | Deskripsi
--|--|--
event | string | Jenis peristiwa. Untuk detailnya, lihat [Jenis Peristiwa](#Event_Type).
email | string | Alamat email penerima
link | string | URL dalam email yang diklik oleh penerima. Bidang ini hanya berlaku jika nilai `event` adalah `click`.
bulkId | string | `MessageId` dikembalikan oleh `SendEmail` API
timestamp | int | Stempel waktu saat peristiwa dibuat
reason | string | Alasan mengapa email gagal terkirim
bounceType | string | Jenis penolakan ketika email ditolak oleh penyedia layanan email (ESP) penerima. Nilai yang valid: soft, hard. Bidang ini hanya berlaku jika nilai `event` adalah `bounce`.

## Jenis Peristiwa[](id:Event_Type)
Nilai | Deskripsi
--|--
processed | Mengirimkan. Keadaan ini merupakan keadaan peralihan dan tidak dapat dipanggil kembali.
deferred | Pengiriman email telah ditunda oleh ESP penerima dan sedang dicoba ulang.
delivered | Pengiriman berhasil. ESP penerima menerima email.
dropped | Email tidak dapat dikirim dan dibatalkan karena beberapa alasan.
open | Penerima membuka email.
click | Penerima mengeklik URL di email.
bounce | ESP penerima menolak email (biasanya karena alamat email salah).
spamreport | Penerima melaporkan email.
unsubscribe | Penerima mengeklik tombol berhenti berlangganan. URL berhenti berlangganan harus berisi kata kunci "berhenti berlangganan".
