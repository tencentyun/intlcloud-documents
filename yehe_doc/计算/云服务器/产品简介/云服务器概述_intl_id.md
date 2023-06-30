## Ikhtisar CVM

Tencent Cloud Virtual Machine (CVM) adalah layanan komputasi cloud yang dapat diskalakan yang membebaskan Anda dari estimasi penggunaan sumber daya dan investasi di muka. Dengan Tencent Cloud CVM, Anda dapat memulai CVM dan men-deploy aplikasi secepatnya.
Anda dapat menyesuaikan semua sumber daya instans CVM, termasuk CPU, memori, disk, jaringan, dan kebijakan keamanan. Anda juga dapat dengan mudah menyesuaikan sumber daya dalam menanggapi setiap perubahan permintaan.

## Menggunakan instans CVM

Anda dapat mengonfigurasi dan mengelola instans CVM dengan cara berikut:
- **Konsol**: UI berbasis web untuk mengonfigurasi dan mengelola instans CVM.
- **API**: Tencent Cloud juga menyediakan API untuk mengonfigurasi dan mengelola instans CVM. Untuk informasi selengkapnya, lihat [Kategori API](https://intl.cloud.tencent.com/document/api/213/15689).
- **SDK**: Anda dapat menggunakan [SDK](https://intl.cloud.tencent.com/document/product/494) atau [Tencent Cloud CLI](https://intl.cloud.tencent.com/document/product/1013) untuk memanggil CVM API.

## Konsep Utama

Sebelum menggunakan Tencent Cloud CVM, Anda harus mempelajari konsep berikut:
<table>
<tr>
<th width="12%">Konsep</th><th>Deskripsi</th>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/4939">Instans</a></td>
<td>Sumber daya komputasi virtual berisi komponen komputasi dasar seperti CPU, memori, OS, jaringan, dan disk. Tencent Cloud menyediakan berbagai konfigurasi CPU, MEM, penyimpanan, dan kapasitas jaringan untuk instans CVM. Untuk informasi selengkapnya, lihat <a href="https://intl.cloud.tencent.com/document/product/213/11518">Jenis Instans</a>.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/4940">Citra</a></td>
<td>Templat yang telah dikonfigurasi sebelumnya berisi sistem operasi dan aplikasi yang menjalankan instans CVM. Tencent Cloud CVM menyediakan citra yang telah dikonfigurasi sebelumnya untuk Windows, Linux, dll.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/4953">Cloud Block Storage</a></td>
<td>Perangkat penyimpanan blok terdistribusi dan persisten yang disediakan oleh Tencent Cloud yang dapat berfungsi sebagai disk sistem atau disk data instans yang dapat diperluas.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/215/535">Virtual Private Cloud</a></td>
<td>Ruang jaringan virtual yang terisolasi secara logis di Tencent Cloud.</td>
</tr>
<tr>
<td>Alamat IP</td>
<td>Tencent Cloud menyediakan alamat <a href="https://intl.cloud.tencent.com/doc/product/213/5225">IP Pribadi</a> dan <a href="https://intl.cloud.tencent.com/document/product/213/5224">IP Publik</a>. Alamat IP pribadi berfungsi untuk interkoneksi instans CVM dalam LAN yang sama, sedangkan alamat IP publik berfungsi untuk layanan yang dapat diakses oleh publik.</td>
</tr>
<tr>
<td>IP Elastis</td>
<td>Alamat IP jaringan publik statis dirancang khusus untuk jaringan dinamis guna memenuhi permintaan pemecahan masalah yang cepat.</td>
</tr>
<tr>
<td><a href="https://intl.cloud.tencent.com/document/product/213/12452">Grup keamanan</a></td>
<td>Firewall virtual yang menampilkan pemfilteran paket data stateful. Firewall ini digunakan untuk mengonfigurasi kontrol akses jaringan CVM. Grup keamanan adalah ukuran penting untuk keamanan dan isolasi jaringan.</td>
</tr>
</table>

## Membeli dan Menyesuaikan Instans CVM

Jika Anda memiliki kebutuhan khusus yang tidak dapat dipenuhi oleh spesifikasi CVM standar kami, gunakan panduan berikut untuk mempelajari cara mendapatkan konfigurasi kustom:
- [Menyesuaikan Konfigurasi CVM Windows](https://intl.cloud.tencent.com/document/product/213/10516)
- [Menyesuaikan Konfigurasi CVM Linux](https://intl.cloud.tencent.com/document/product/213/10517)

## Harga CVM

CVM mendukung metode bayar sesuai pemakaian. Untuk informasi selengkapnya, lihat [Harga Instans CVM](https://intl.cloud.tencent.com/document/product/213/2176).
Untuk informasi harga pada instans CVM dan sumber daya lainnya, lihat [Harga Produk](https://buy.cloud.tencent.com/price/cvm/overview).

## Produk Terkait

- Penskalaan Otomatis memungkinkan Anda menskalakan kluster server menggunakan kriteria yang telah ditentukan sebelumnya seperti waktu atau beban. Untuk informasi selengkapnya, lihat [dokumentasi Penskalaan Otomatis](https://intl.cloud.tencent.com/document/product/377).
- Cloud Load Balancer memungkinkan Anda mendistribusikan traffic klien secara otomatis di antara beberapa instans CVM. Untuk informasi selengkapnya, lihat [dokumentasi Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214).
- Tencent Kubernetes Engine memungkinkan Anda mengelola siklus proses aplikasi dalam CVM. Untuk informasi selengkapnya, lihat [dokumentasi Tencent Kubernetes Engine](https://intl.cloud.tencent.com/document/product/457).
- Cloud Monitor melacak instans CVM Anda dan disk sistemnya. Untuk informasi selengkapnya, lihat [dokumentasi Basic Cloud Monitor](https://intl.cloud.tencent.com/document/product/248).
- Anda dapat menggunakan database relasional di cloud atau menggunakan TencentDB. Untuk informasi selengkapnya, lihat [dokumentasi TencentDB for MySQL](https://intl.cloud.tencent.com/document/product/236).


