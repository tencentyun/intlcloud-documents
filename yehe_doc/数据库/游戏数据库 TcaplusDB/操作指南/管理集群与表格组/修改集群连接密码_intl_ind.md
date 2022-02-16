## Skenario Operasi
Dokumen ini menjelaskan cara mengubah kata sandi koneksi kluster di Konsol TcaplusDB dan memperbarui waktu kedaluwarsa kata sandi lama.

## Prasyarat
Anda telah membuat kluster dan grup tabel. Untuk informasi selengkapnya, silakan lihat [Membuat Kluster](https://intl.cloud.tencent.com/document/product/1016/32714) dan [Membuat Grup Tabel](https://intl.cloud.tencent.com/document/product/1016/32716).

## Petunjuk
### Mengubah kata sandi koneksi
1. Masuk ke halaman [Daftar Kluster](https://console.cloud.tencent.com/tcaplusdb/app), klik **Change Password** (Ubah Kata Sandi) di "Connection Password" (Kata Sandi Koneksi) kluster, masukkan kata sandi lama dan kata sandi baru, konfirmasi kata sandi baru di kotak dialog pop-up, dan klik **Confirm** (Konfirmasi).
>Untuk "Defer Change" (Menunda Perubahan), Anda harus memilih **Update password** (Perbarui kata sandi) dan waktu kedaluwarsa kata sandi lama.
>
![](https://main.qcloudimg.com/raw/7aab39aa33e2e461e0a2e87b07abeeb6.png)
2. Setelah permintaan berhasil diajukan, waktu kedaluwarsa kata sandi lama akan ditampilkan di halaman detail kluster, sebelum kata sandi lama akan tetap valid dan Anda tidak dapat mengajukan permintaan lain untuk memperbarui kata sandi.

### Memperbarui waktu kedaluwarsa kata sandi lama
>Sebelum kata sandi lama kedaluwarsa, Anda dapat memperbarui waktu kedaluwarsanya untuk mempersingkat atau memperpanjang periode sebelum menggantinya.

1. Masuk ke halaman [Daftar Kluster](https://console.cloud.tencent.com/tcaplusdb/app), klik **Change Password** (Ubah Kata Sandi) di "Connection Password" (Kata Sandi Koneksi) pada kluster, ubah waktu kedaluwarsa di kotak dialog pop-up, dan klik **Confirm** (Konfirmasi).
 - **Old Password** (Kata Sandi Lama): kata sandi lama yang akan kedaluwarsa, yaitu kata sandi lama yang Anda masukkan saat Anda mengubah kata sandi koneksi.
 - **New Password** (Kata Sandi Baru): kata sandi baru yang belum berlaku, yaitu kata sandi baru yang Anda masukkan saat Anda mengubah kata sandi koneksi.
 - **Defer Change** (Menunda Perubahan): pilih **Update old password expiration time** (Perbarui waktu kedaluwarsa kata sandi lama).
 - **Old Password Expiration Time** (Waktu Kedaluwarsa Kata Sandi Lama): pilih waktu kedaluwarsa yang baru.
![](https://main.qcloudimg.com/raw/f603e4184231af909e48129d6cce56d4.png)
2. Kembali ke halaman detail kluster dan Anda akan melihat bahwa waktu kedaluwarsa kata sandi lama telah diperbarui.
>Setelah waktu kedaluwarsa, kata sandi lama akan kedaluwarsa, dan Anda dapat mengajukan permintaan baru untuk memperbarui kata sandi.
