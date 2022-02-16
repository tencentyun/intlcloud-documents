## Ikhtisar
Perintah ini digunakan untuk mengkueri Time to Live (TTL) dalam milidetik dari sebuah catatan. Setelah catatan dikonfigurasi dengan TTL, Anda dapat menggunakan `getttl` untuk mengkueri TTL kuncinya, yaitu, berapa lama sampai kunci dihapus karena kedaluwarsa. Perintah ini dapat menanyakan TTL hanya untuk satu catatan.

## Sintaksis
```
getttl dari [table] dengan key1 = 1 dan key2 = "abc";
```

## Parameter

| Parameter             | Diperlukan | Batas Penggunaan                     | Deskripsi                            |
| ---------------- | -------- | ---------------------------- | ------------------------------- |
| tabel            | Ya       | Tidak ada                           | Nama tabel                            |
| kunci dalam klausul WHERE | Ya      | Tabel TDR: semua nilai kunci diperlukan | Tentukan nilai kunci. Beberapa nilai dipisahkan dengan `and`. |

## Kesalahan
Untuk informasi selengkapnya, silakan lihat [Kode Kesalahan](https://intl.cloud.tencent.com/document/product/1016/38791).

## Pesan Pengembalian

| Situasi                                 | Pesan Pengembalian                                                     |
| ---------------------------------------- | ------------------------------------------------------------ |
| Kunci tidak ada atau telah kedaluwarsa.                     | Catatan tidak ada atau telah kedaluwarsa\.                       |
| Kuncinya ada tetapi TTL-nya tidak ditentukan. | Catatan ada dan tidak ada waktu kedaluwarsa yang ditetapkan \(permanent\)\.  |
| Gagal mengkueri TTL.                                 | Gagal mendapatkan waktu untuk aktif\. Kode kesalahannya adalah \[error code\] dan pesan kesalahannya adalah \[Error message\]\. |
| Mengkueri TTL berhasil.                                 | Waktu untuk aktif adalah \[TTL\] milidetik\.                   |


## Sampel
Mengkueri TTL catatan:
```
tcaplus> getttl dari email dengan key1 = 1 dan key2 = "abc";
Waktu untuk aktif adalah 2000 milidetik.
```
