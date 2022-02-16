## Ikhtisar
Perintah ini digunakan untuk mengatur time to live (TTL) dalam milidetik untuk sebuah catatan. Nilai yang ditetapkan akan dikurangi dengan waktu yang telah berlalu. Ketika nilai TTL catatan sama dengan 0, TcaplusDB akan menghapusnya. Perintah ini hanya berlaku pada satu catatan.

## Sintaksis
```
setttl [tabel] ttl=[TTL] dengan key1 = 1 dan key2 = "abc";
```

## Parameter

| Parameter             | Diperlukan | Batas                                                   | Deskripsi                            |
| ---------------- | -------- | ------------------------------------------------------------ |------------------------------- |
| tabel            | Ya       | Tidak                                                       | Nama tabel                            |
| TTL              | Ya       | Nilai tidak boleh melebihi setengah dari nilai maksimum `uint64\_t`. Dengan kata lain, nilai TTL maksimum adalah ULONG\_MAX/2. Nilai yang melebihi batas ini akan diatur ke nilai maksimum.    | Waktu untuk aktif dalam milidetik |
| Masukkan klausul WHERE | Ya       | Semua nilai kunci diperlukan untuk tabel TDR.      | Nilai kunci perlu dideklarasikan. Beberapa nilai kunci digabungkan dengan `and`.  |

## Kesalahan
Untuk informasi selengkapnya, lihat [Kode Kesalahan](https://intl.cloud.tencent.com/document/product/1016/38791).


## Pesan Pengembalian

| Situasi             | Pesan Pengembalian                                                   |
| -------------------- | ------------------------------------------------------------ |
| Catatan tidak ada atau telah kedaluwarsa. | Catatan tidak ada atau telah kedaluwarsa\.                       |
| Gagal mengatur waktu aktif.            | Gagal mengatur waktu aktif\. Kode kesalahannya adalah \[error code\] dan pesan kesalahannya adalah \[Error message\]\. |
| Atur waktu agar berhasil aktif.            | Atur waktu agar berhasil aktif\.                              |


## Sampel
Atur TTL ke 2.000 milidetik:
```
tcaplus> setttl mails ttl=2000 dengan key1 = 1 dan key2 = "abc";
Atur waktu agar berhasil aktif.
```
