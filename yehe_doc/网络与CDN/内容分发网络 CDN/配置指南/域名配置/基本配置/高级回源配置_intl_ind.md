

Tencent Cloud Content Delivery Network menawarkan konfigurasi tarik-asal yang disempurnakan untuk meneruskan permintaan tarik-asal berdasarkan jalur (yaitu, menentukan jenis file, folder, file jalur lengkap, atau beranda untuk tarik-asal) dan wilayah IP klien.

>! Tarik-asal berdasarkan wilayah IP klien berada dalam versi beta, silakan nantikan peluncuran resminya.

## Panduan Konfigurasi

Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn), pilih **Domain Management** (Pengelolaan Domain) di bilah samping kiri, klik **Manage** (Kelola) di sebelah kanan nama domain untuk masuk ke halaman konfigurasinya, dan buka tab **Basic Configuration** (Konfigurasi Dasar) untuk menemukan bagian **Advanced Origin-pull Configuration** (Konfigurasi Tarik-Asal Lanjutan).

![](https://main.qcloudimg.com/raw/17e0385a7cea2cbdd0ae012cae8b2555.png)

### Menambahkan aturan

Anda dapat mengeklik **Add Rule** (Tambahkan Aturan) untuk menambahkan aturan sesuai kebutuhan.
![](https://main.qcloudimg.com/raw/ef2ae0e51a0cb032d493f89b8029b316.png)

**Batasan**

- Setiap nama domain dapat dikonfigurasi hingga 50 aturan.
- Alamat tarik-asal dari satu aturan dapat berupa IP, nama domain, dan port (rentang: 0 - 65535; port dapat dihilangkan). Jika "HTTPS" atau "Follow Protocol" (Ikuti Protokol) dipilih sebagai protokol tarik-asal, port harus diisi dengan 443 atau dibiarkan kosong.
- Tindakan selengkapnya: Anda dapat menyesuaikan prioritas aturan dan mengedit atau menghapus beberapa aturan dalam batch.

>?
>- Dalam daftar aturan, aturan yang lebih rendah memiliki prioritas yang lebih tinggi. Perhatikan bahwa jika Anda mengatur ulang aturan dalam daftar, hanya prioritas aturan dari jenis yang sama yang terpengaruh.
>- Jika permintaan cocok dengan kedua jenis aturan, aturan akan dijalankan dalam urutan aturan berbasis jalur dan kemudian aturan berbasis wilayah IP klien.
Misalnya, saat ada dua aturan tarik-asal: "meneruskan semua permintaan dari provinsi Jiangsu ke `1.1.1.1`" dan "meneruskan permintaan yang mengakses `/test` ke `2.2.2.2`", jika permintaan dari Jiangsu ingin mengakses direktori `/test`, permintaan akan diteruskan ke `2.2.2.2`.
