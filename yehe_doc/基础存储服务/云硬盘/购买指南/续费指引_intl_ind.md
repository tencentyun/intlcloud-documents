Berdasarkan siklus hidupnya, disk cloud dapat digunakan sebagai disk sistem atau disk data CVM.Pembaruan disk cloud yang tepat waktu dapat mencegah kehilangan data yang disebabkan oleh kedaluwarsa.Kami menyarankan Anda mengonfigurasi pengingat kedaluwarsa untuk data penting.


## Memperbarui disk data
- Hanya disk data CBS dengan cara penagihan berlangganan bulanan yang mendukung pembaruan.
- Sebelum disk data CBS kedaluwarsa, Anda dapat memperbaruinya untuk menghindari pelepasan disk dan kegagalan baca/tulis yang disebabkan oleh kedaluwarsa.
- Setelah disk data CBS kedaluwarsa dan sebelum disk data tersebut dihentikan (dalam 14 hari setelah kedaluwarsa), Anda dapat memulihkannya.Jika Anda tidak memperbarui disk tepat waktu, disk akan dihentikan dan dapat menyebabkan kehilangan data.

### Memperbarui melalui API
Anda dapat menggunakan API RenewDisk untuk memperbarui disk cloud elastis.
