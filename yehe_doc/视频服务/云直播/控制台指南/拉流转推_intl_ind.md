Konsol CSS Tencent Cloud menyediakan fitur relai. Jika Anda tidak dapat menggunakan sumber streaming langsung untuk melakukan push atau Anda ingin menggunakan video sesuai permintaan untuk streaming langsung, Anda dapat menggunakan fitur relai untuk melakukan pull pada konten dengan cepat dari sumber streaming langsung yang ada atau video dan kemudian melakukan push ke URL tujuan, tanpa perlu melakukan push langsung.
![](https://main.qcloudimg.com/raw/8f0b044ce2104efdc1ed835287b9b683.png)

## Prasyarat
- Anda telah mengaktifkan [CSS](https://intl.cloud.tencent.com/product/css) dan login ke konsol CSS.
- Anda telah menambahkan [nama domain push](https://intl.cloud.tencent.com/document/product/267/35970) di konsol.

## Batas
- Anda dapat membuat hingga **20** tugas relai.
- Biaya fitur relai dikenakan berdasarkan **durasi tugas relai**. Informasi lebih lanjut dapat dilihat di [Relay (Relai)](https://intl.cloud.tencent.com/document/product/267/41059).
- Relai hanya melakukan pull dan push pada konten. **Pastikan bahwa konten telah diberi izin dan mematuhi undang-undang dan peraturan untuk distribusi. Jika konten melanggar hak terkait atau melanggar peraturan, CSS akan menangguhkan fitur terkait dan berhak mengambil tindakan hukum**.

[](id:create)
## Membuat Tugas
1. Buka **CSS Toolkit** > **[Relay](https://console.cloud.tencent.com/live/tools/relay)** (Toolkit CSS > Relai), lalu klik **Create Task** (Buat Tugas).
![](https://qcloudimg.tencent-cloud.cn/raw/f41c7a329a9fed7a901bca252a973f35.png)
2. Masukkan informasi dasar tugas:
![](https://qcloudimg.tencent-cloud.cn/raw/d10fb06aba921e27791441a112039586.png)
<table>
<tr><th width="15%">Item Konfigurasi</th><th>Deskripsi</th>
<tr>
<td>Task Description (Deskripsi Tugas)</td>
<td>Berikan deskripsi tugas.</td>
</tr><tr>
<td>Execution Time (Waktu Eksekusi)</td>
<td>Waktu eksekusi default adalah dari <code>waktu saat ini</code> hingga <code>24 jam kemudian</code>. Anda dapat memilih rentang waktu tidak lebih dari 7 hari, dan waktu mulai tidak boleh lebih dari 1 tahun dari waktu saat ini. <br>Misalnya, waktu saat ini adalah 24-3-2021 11:50:01. <ul style="margin:0"><li/>Anda dapat memilih rentang waktu antara 24-3-2021 11:50:01 dan 30-3-2022 11:50:01.<li/>Waktu berakhir tidak boleh lebih dari 30-3-2022 11:50:01.</ul></td
</tr><tr>
<td>Event Callback Notification (Pemberitahuan Panggilan Balik Peristiwa)</td>
<td>Masukkan URL panggilan balik untuk menerima pemberitahuan peristiwa tugas relai. </td>
</tr></table>
3. Berikan informasi sumber konten.
      - Wilayah: Acak (Tiongkok Daratan), wilayah Tiongkok Utara (Beijing), Tiongkok Timur (Shanghai), Tiongkok Selatan (Guangzhou), Asia Tenggara (Singapura), Asia Tenggara (Bangkok), Asia Timur Laut (Seoul), Asia Selatan (Mumbai), Hong Kong
      - Jika Anda memilih **Random (Chinese mainland)** (Acak (Tiongkok Daratan)), sistem akan menetapkan wilayah yang terdekat.
4. Untuk **Content Type** (Jenis Konten), Anda dapat memilih **Live streaming** (Streaming langsung) atau **Custom video path** (Jalur video kustom).
   - **Live streaming** (Streaming langsung):
     - Masukkan URL streaming langsung (**hanya satu** yang diizinkan).
   ![](https://qcloudimg.tencent-cloud.cn/raw/6795d964f41e63fa90f0c09e3ddcf060.png)
     - Jika Anda memilih **Enable backup** (Aktifkan cadangan), saat sistem gagal melakukan pull pada konten dari sumber utama, sistem akan secara otomatis beralih ke sumber cadangan. Setelah sumber utama pulih, Anda harus beralih kembali secara manual. Sumber cadangan hanya mendukung loop dari satu video.
   - **Custom video path** (Jalur video kustom):
      - Anda dapat memasukkan **beberapa** (maksimum 30) URL sumber.
      - Pilih **Repeat** (Ulangi) untuk mengulang pemutaran ulang secara tidak terbatas atau **Specified** (Ditentukan) untuk menentukan jumlah (1‒100 kali) pemutaran konten.
      ![](https://qcloudimg.tencent-cloud.cn/raw/154e880ea3f2a60eef9031c7cba11510.png)
>? 
>- Sistem akan menghentikan tugas relai saat jumlah pemutaran ulang mencapai nilai yang ditentukan atau saat tugas mencapai waktu berakhirnya.
>- Setelah memodifikasi tugas:
     - Jika Anda hanya mengubah jumlah pemutaran ulang, setelah nilai baru diterapkan, perhitungan akan dimulai dari 2.
	  - Jika Anda mengubah URL sumber dan jumlah pemutaran ulang, setelah konfigurasi baru diterapkan (segera atau setelah pemutaran ulang saat ini berakhir), perhitungan akan dimulai dari 1.
	  - Jika Anda mengubah URL tujuan, jumlah pemutaran ulang akan diatur ulang.
5. Masukkan URL tujuan untuk menerima konten.
   1. Klik **Address Generator** (Pembuat Alamat) untuk membuka halaman pembuatan URL.
   ![](https://qcloudimg.tencent-cloud.cn/raw/9724d77727e21ba1798485d03d6e3246.png)
   2. Pilih nama domain push yang sudah ada, masukkan `Appname`, `StreamName`, dan waktu kedaluwarsa, lalu klik **Confirm** (Konfirmasi) untuk membuat URL push, yang akan diisi secara otomatis sebagai **Destination Address** (Alamat Tujuan).
   ![](https://qcloudimg.tencent-cloud.cn/raw/b1b6f0b832bacb15b281d71fc653afb0.png)
> !Pastikan waktu kedaluwarsa URL lebih akhir dari waktu berakhirnya tugas. Jika Anda mengubah tujuan setelah tugas dimulai, tugas akan berhenti dan dimulai ulang.
6. Klik **Save** (Simpan).


## Mengelola Tugas
[](id:view)
### Melihat detail tugas
Di [task list (daftar tugas)](https://console.cloud.tencent.com/live/tools/relay), temukan tugas Anda, lalu klik description/ID (deskripsi/ID) untuk melihat detail tugas di jendela pop-up.
![](https://qcloudimg.tencent-cloud.cn/raw/c2bad33a6a735a218fa79b98f3738275.png)

>? Anda dapat mengeklik tombol di bagian bawah jendela pop-up untuk mengedit tugas, mengubah input, memulai ulang tugas, atau menonaktifkan tugas.

### Melihat status tugas
Di [task list (daftar tugas)](https://console.cloud.tencent.com/live/tools/relay), temukan tugas Anda, lalu klik description/ID (deskripsi/ID) untuk melihat status eksekusi di jendela pop-up.

![](https://qcloudimg.tencent-cloud.cn/raw/cd498cb1fd678e39b0942383c278e82b.png)

<table>
<thead><tr><th>Status Tugas</th><th>Nilai Kolom</th><th>Deskripsi</th></tr></thead>
<tbody><tr>
<td>Not started (Belum dimulai)</td>
<td>Inactive (Tidak aktif)</td>
<td>Tugas belum dimulai.</td>
</tr><tr>
<td rowspan=2>Valid</td>
<td>Active (Aktif)</td>
<td>Tugas telah dimulai dan dijalankan seperti yang diharapkan.</td>
</tr><tr>
<td>Inactive (Tidak aktif)</td>
<td>Tugas telah dimulai, tetapi tidak dijalankan seperti yang diharapkan.</td>
</tr><tr>
<td>Disabled (Dinonaktifkan)</td>
<td>Inactive (Tidak aktif)</td>
<td>Tugas dinonaktifkan.</td>
</tr><tr>
<td>Expired (Kedaluwarsa)</td>
<td>Inactive (Tidak aktif)</td>
<td>Tugas telah kedaluwarsa.</td>
</tr>
</tbody></table>



[](id:change)
### Memodifikasi tugas
1. Di [task list (daftar tugas)](https://console.cloud.tencent.com/live/tools/relay), temukan tugas yang ingin Anda modifikasi, lalu klik **Edit**.
![](https://qcloudimg.tencent-cloud.cn/raw/a0a83bf06f9b5ae9743b68b19e4c40cd.png)
2. Modifikasi informasi tugas, lalu klik **Save** (Simpan).
 - Anda tidak dapat mengubah wilayah atau jenis konten.
 - Saat mengubah waktu berakhirnya tugas, pastikan URL tujuan valid hingga tugas berakhir. Memodifikasi URL tujuan akan menyebabkan tugas terhenti dan dimulai ulang.
![](https://qcloudimg.tencent-cloud.cn/raw/d950a8029e1944e9029445dd8e428933.png)
3. Di jendela pop-up, periksa informasi sebelum dan sesudah perubahan:
   - Misalnya, Anda memodifikasi **start time, end time, and playback count** (waktu mulai, waktu berakhir, dan jumlah pemutaran ulang) tugas. Anda akan melihat informasi berikut di jendela pop-up:
![](https://qcloudimg.tencent-cloud.cn/raw/4cadcabeef99828ab4be144040cbfd19.png)
   - Jika URL sumber untuk **Custom video path** (Jalur video kustom) diubah, Anda harus memilih untuk menerapkan perubahan **After the current video ends** (Setelah video saat ini berakhir) (default) atau **Now** (Sekarang). Setelah perubahan diterapkan, relai akan dimulai ulang dari URL sumber pertama.
![](https://qcloudimg.tencent-cloud.cn/raw/9591b91b7e5e307860c9ea2244b4e14e.png)
    - Jika **Destination Address** (Alamat Tujuan) diubah, sistem akan mengingatkan Anda bahwa setelah Anda mengeklik **Confirm** (Konfirmasi), tugas relai saat ini akan **berhenti dan dimulai ulang**.
![](https://qcloudimg.tencent-cloud.cn/raw/0a7e04f65ae8bbdd9cb7ef3bc0ece656.png)
4. Setelah pemeriksaan selesai, klik **Confirm** (Konfirmasi).

[](id:copy)

### Menyalin tugas
1. Di [task list (daftar tugas)](https://console.cloud.tencent.com/live/tools/relay), temukan tugas relai yang ingin Anda salin, lalu klik **Copy** (Salin). Anda akan diarahkan ke halaman pembuatan tugas.
![](https://qcloudimg.tencent-cloud.cn/raw/28a0a3542ab9ab838d26dfc565f321d1.png)
2. Informasi tugas yang disalin akan diisi secara otomatis. Anda dapat [memodifikasinya](#create) sesuai dengan kebutuhan.
3. Klik **Save** (Simpan) untuk membuat tugas relai baru.



[](id:reboot)
### Memulai ulang tugas
Memulai ulang tugas **tidak akan mengubah status tugas**. Tugas yang sedang berlangsung akan **dimulai ulang dari awal**. Lakukan hal berikut untuk memulai ulang tugas:

1. Di [task list (daftar tugas)](https://console.cloud.tencent.com/live/tools/relay), temukan tugas relai yang ingin Anda mulai ulang, lalu klik **Restart** (Mulai ulang).
2. Di jendela pop-up, klik **Restart** (Mulai Ulang).
![](https://qcloudimg.tencent-cloud.cn/raw/d1b03e226297e44cbb7504d57c54af4f.png)

[](id:disable)
### Menonaktifkan tugas
Jika Anda menonaktifkan tugas, **tugas akan berhenti**. Anda dapat mengeklik [Enable (Aktifkan)](#enable) untuk memulai kembali tugas. Lakukan hal berikut untuk menonaktifkan tugas:

1. Di [task list (daftar tugas)](https://console.cloud.tencent.com/live/tools/relay), temukan tugas relai yang ingin Anda nonaktifkan, lalu klik **Disable** (Nonaktifkan).
2. Di jendela pop-up, klik **Disable** (Nonaktifkan).
![](https://qcloudimg.tencent-cloud.cn/raw/c3acfb89f425b50ba53a8d63075091d8.png)


[](id:enable)
### Mengaktifkan tugas
Jika Anda mengaktifkan tugas, **tugas akan dimulai dari awal**. Lakukan hal berikut untuk mengaktifkan tugas:

1. Di [task list (daftar tugas)](https://console.cloud.tencent.com/live/tools/relay), temukan tugas relai yang ingin Anda aktifkan, lalu klik **Enable** (Aktifkan).
2. Di jendela pop-up, klik **OK** (OKE).
![](https://qcloudimg.tencent-cloud.cn/raw/77417a9c8406fe9d763c4d3960d98b21.png)

[](id:delete)
### Menghapus tugas
Tugas yang dihapus **tidak dapat dipulihkan**. Lakukan hal berikut untuk menghapus tugas:

1. Di [task list (daftar tugas)](https://console.cloud.tencent.com/live/tools/relay), temukan tugas relai yang ingin Anda hapus, lalu klik **Delete** (Hapus).
2. Di jendela pop-up, klik **Delete** (Hapus).
![](https://qcloudimg.tencent-cloud.cn/raw/44a15ad52bfc81f62c0aa907cdc7eb5c.png)

[](id:batch)
### Pengoperasian dalam batch
Anda dapat menghapus, menonaktifkan, dan mengaktifkan **hingga 10 tugas relai** sekaligus.
1. Di [task list (daftar tugas)](https://console.cloud.tencent.com/live/tools/relay), pilih tugas relai yang ingin Anda hapus, nonaktifkan, atau aktifkan.
2. Klik **Batch Operation** (Pengoperasian dalam Batch), lalu pilih **Delete** (Hapus), **Disable** (Nonaktifkan), atau **Enable** (Aktifkan).
![](https://qcloudimg.tencent-cloud.cn/raw/7401eade6f5e04b9eadf71e04211f6e0.png)
3. Di jendela pop-up, konfirmasi informasi, lalu klik **Delete** (Hapus), **Disable** (Nonaktifkan), atau **Enable** (Aktifkan).
![](https://qcloudimg.tencent-cloud.cn/raw/5874636c548a4733281cd33eaca35abe.png)

   
## Menghapus Otomatis Tugas yang Kedaluwarsa

Tugas kedaluwarsa setelah waktu berakhir tugas. Jika memiliki terlalu banyak tugas relai, Anda mungkin tidak dapat membuat tugas relai baru. Untuk menghindarinya, Anda dapat mengaktifkan penghapusan otomatis agar sistem menghapus tugas kedaluwarsa secara otomatis pada waktu yang ditentukan. Tugas yang dihapus tidak dapat dipulihkan.

1. Buka **CSS Toolkit** > **[Relay](https://console.cloud.tencent.com/live/tools/relay)** (Toolkit CSS > Relai), lalu klik **Set** (Atur) di area **Expired** (Kedaluwarsa).
2. Klik ![](https://qcloudimg.tencent-cloud.cn/raw/7ed257d05a4283dc233ef406520187b4.png) untuk mengaktifkan penghapusan otomatis.
3. Tentukan periode (1‒24 jam) penyimpanan tugas kedaluwarsa sebelum tugas tersebut dihapus.
![](https://qcloudimg.tencent-cloud.cn/raw/4d579b1d0776ea22b5d994e3b7357ea3.png)



