## Skenario Operasi
Anda dapat menggunakan fitur pencarian nama domain untuk menemukan nama domain tertentu. Anda dapat memfilter nama domain dengan beberapa kriteria seperti nama domain, server asal, tag, dan proyek serta beberapa kata kunci.
> Sebuah tag disediakan oleh Tencent Cloud untuk mengidentifikasi sumber daya di cloud. Untuk informasi selengkapnya tentang tag dan cara mengelolanya, lihat [Tag](https://intl.cloud.tencent.com/document/product/651).

## Petunjuk
1. Masuk ke [Konsol CDN](https://console.cloud.tencent.com/cdn) dan klik **Domain Management** (Pengelolaan Domain) di bilah samping kiri untuk masuk ke halaman pengelolaan.
2. Klik kotak pencarian nama domain untuk mengaktifkan fitur pencarian, pilih satu atau beberapa atribut sumber daya seperti nama domain, server asal, tag, atau proyek, dan masukkan nilai untuk memfilter nama domain.
![](https://main.qcloudimg.com/raw/5f77724408026bd05f2d1ac14b9f8b86.png)
3. Jika Anda memiliki pertanyaan tentang atribut sumber daya input atau format input, klik ikon **i** untuk [bantuan dengan pencarian](#bantuan).
![](https://main.qcloudimg.com/raw/b633c3602cc79891cd9ad2e0c11323f9.png)

>
>+ Anda hanya dapat melakukan pencarian dalam server asal master, bukan server slave.
>+ Gunakan titik koma (;) untuk memisahkan alamat IP server asal saat melakukan pencarian di beberapa server asal.
>+ Hanya pencarian kata kunci tunggal yang didukung untuk nama domain dan server asal.

## Deskripsi Pencarian
+ Cari berdasarkan nama domain: Masukkan nama domain lengkap atau sebagian untuk pencarian. Pencarian fuzzy didukung.
![](https://main.qcloudimg.com/raw/95ff6e4da21cfa031a625146bf912b4b.png)
+ Cari berdasarkan server asal: Masukkan server asal lengkap atau sebagian untuk pencarian. Pencarian fuzzy didukung.
+ Cari berdasarkan tag: Masukkan tag lengkap, dan daftar nama domain yang berisi tag yang dimasukkan akan dikembalikan. Pencarian fuzzy tidak didukung.
+ Cari berdasarkan proyek: Anda dapat memilih beberapa proyek sebagai filter.
![Project](https://main.qcloudimg.com/raw/bdcaa7725595005fd1b49c3953559437.png)
- Filter berdasarkan beberapa kriteria: Anda dapat memilih satu atau beberapa kriteria seperti tag, nama domain, server asal, dan proyek untuk pemfilteran. Gunakan tombol enter untuk memisahkan beberapa kriteria.
- Filter berdasarkan beberapa kata kunci: Anda dapat memasukkan beberapa kata kunci untuk setiap kriteria filter. Gunakan bilah vertikal (|) untuk memisahkan beberapa kata kunci.

<span id=help></span>
## Bantuan dengan pencarian
<style>
table th:first-of-type {
    width: 110px;
}
table th:nth-of-type(2) {  
width: 240px;
}
</style>

| Jenis              | Format Input                                             | Contoh                    | Contoh Kotak Pencarian                                                  | Deskripsi                                                        |
| ----------------- | --------------------------------------------------- |----------------------- | ----------------------------------------------------------- | ------------------------------------------------------------ |
|   Kata kunci tunggal      | **Kata Kunci Tunggal**                                           | www.test.com             |  ![Kata kunci tunggal](https://main.qcloudimg.com/raw/af1f1771fd42f0a38df5c7a0bc9bc861.png)| Memfilter nama domain yang memuat `www.test.com`                           |
| Atribut nama domain tunggal        | **Atribut**:**kata kunci**                                  | Origin server:1.1.1.1            | ![Atribut nama domain tunggal](https://main.qcloudimg.com/raw/95eab4659fde0526a6ff7b82b4dae03b.png) | Memfilter nama domain yang memuat server asal 1.1.1.1                                  |
| Atribut beberapa nama domain       | **Atribut**:**kata kunci** **pengembalian pembawa**<br>**Atribut**:**kata kunci** | Domain name:test<br>Origin server:1.1.1.1 | ![Atribut beberapa nama domain](https://main.qcloudimg.com/raw/1e199e5b7a5268ee3e0b458b7db1fa76.png) | Memfilter nama domain untuk nama domain yang memuat "test" dan server asal yang memuat "1.1.1.1"              |
| Atribut nama domain tunggal dengan beberapa kata kunci | **Atribut**:**kata kunci**\|**kata kunci**                      | Project:test1\|test2   | ![Atribut nama domain tunggal dengan beberapa kata kunci](https://main.qcloudimg.com/raw/22a61295630849332aac815db4a6a039.png) | Memfilter nama domain untuk nama domain yang memuat "test1" atau "test2" dari proyek yang dipilih. Atribut nama domain dan server asal saat ini tidak mendukung pencarian beberapa kata kunci |
| Karakter yang disalin           | (Karakter yang ditempel)                                       | test abc                 | ![Salin](https://main.qcloudimg.com/raw/823aeda4c1e1f43dc2fa3cec34b8c29f.png) | Memfilter nama domain yang memuat "test" atau "abc"                              |

>CDN tidak dapat melakukan pencarian global jika tidak ada atribut yang dimasukkan. Oleh karena itu, atribut **nama domain** ditambahkan untuk pencarian secara default. Dengan kata lain, ketika Anda memasukkan satu kata kunci, konten di kotak pencarian akan menjadi `domain name:www.test.com`; ketika Anda menyalin karakter, konten di kotak pencarian akan menjadi `domain name:test|abc`.

