Anda dapat mengelola grup replikasi yang dibuat sesuai kebutuhan dalam kasus penggunaan Ops Anda yang sebenarnya. Khususnya, Anda dapat mengatur instans baca saja sebagai instans master, mengalihkan peran instans master dan baca saja, menghapus instans, atau menghapus grup replikasi.

## Prasyarat
- Anda telah [membuat grup replikasi global](https://intl.cloud.tencent.com/document/product/239/45603), dan grup tersebut dalam status **Running** (Berjalan).
- Anda telah [menambahkan instans ke grup replikasi](https://intl.cloud.tencent.com/document/product/239/45603), dan instans dalam status **Running** (Berjalan).

## Mengatur Instans Baca Saja sebagai Master Instans
Anda dapat mengatur instans baca saja dalam grup replikasi sebagai instans master untuk penulisan data. Perubahan ini hanya memperbarui konfigurasi instans tanpa menyebabkan migrasi data. Seluruh proses memakan waktu sekitar tiga menit.

Untuk petunjuk mendetail, lihat langkah-langkah berikut:
1. Di [daftar grup replikasi](https://console.cloud.tencent.com/redis/replication), klik <img src="https://qcloudimg.tencent-cloud.cn/raw/3a815073e7ccf4206decf7b522a40ccd.png" style="zoom: 67%;" /> sebelum nama grup replikasi target untuk menampilkan daftar instansnya.
2. Temukan instans baca saja target dan klik **Set to Master** (Atur ke Master) di kolom **Operation** (Operasi).
>!Anda dapat mengatur instans baca saja sebagai instans master hanya jika ada setidaknya dua replika instans baca saja dalam grup replikasi.
> 
![](https://qcloudimg.tencent-cloud.cn/raw/10f9f36c3f5e7c18ccd598673d3c9e74.png)
3. Baca perintah dengan cermat di jendela pop-up **Set to Master** (Atur ke Master) dan klik **OK** (OKE).
Dalam daftar instans grup replikasi, **instance status** (status instans) berubah menjadi **switching instance role** (mengalihkan peran instans), dan **instance role** (peran instans) akan berubah menjadi **master instance** (instans master) setelah peralihan.

## Mengatur Instans Master sebagai Instans Baca Saja
Anda juga dapat mengatur instans master yang ditambahkan ke grup replikasi sebagai instans baca saja seperti yang dijelaskan di bawah ini.
![](https://qcloudimg.tencent-cloud.cn/raw/7a29d5abcaf379062fb011e8bfb33f37.png)

## [Mengalihkan Peran Instans](id:qhsljs)
Anda dapat mengalihkan instans master hanya dalam kasus penggunaan pemulihan bencana; yaitu, hanya ada satu instans master dan satu instans baca saja dalam grup replikasi. Biasanya, grup replikasi akan tidak dapat diakses selama satu menit selama peralihan seperti yang ditunjukkan di bawah ini.
![](https://qcloudimg.tencent-cloud.cn/raw/cd56064d296acbed44024cb33829158d.png)
> !Saat data disinkronkan ke instans master baru (instans baca saja asli), data masih tersedia untuk akses baca.

Lihat langkah-langkah berikut untuk cara mengalihkan instans master:
1. Di [daftar grup replikasi](https://console.cloud.tencent.com/redis/replication), klik <img src="https://qcloudimg.tencent-cloud.cn/raw/3a815073e7ccf4206decf7b522a40ccd.png" style="zoom: 67%;" /> sebelum nama grup replikasi target untuk menampilkan daftar instansnya.
2. Temukan instans baca saja target dan klik **Switch with Master Instance** (Alihkan dengan Instans Master) di kolom **Operation** (Operasi).
![](https://qcloudimg.tencent-cloud.cn/raw/b20ca448e8061ff1d472e026ed0093d8.png)
3. Baca perintah dengan cermat di jendela pop-up **Switch with Master Instance** (Alihkan dengan Instans Master) dan klik **OK** (OKE).
4. Baik instans master dan baca saja dalam grup replikasi memasuki status **switching with master instance** (mengalihkan dengan instans master). Tunggu hingga peralihan selesai, lalu Anda dapat melihat bahwa instans master asli menjadi baca saja, sedangkan instans baca saja asli sekarang menjadi instans master.

## Menghapus Instans dari Grup Replikasi
Anda dapat menghapus instans dari grup replikasi. Instans yang dihapus akan berhenti menyinkronkan data dari instans lain dalam grup replikasi.

Lihat langkah-langkah berikut untuk cara menghapus instans dari grup replikasi:
1. Di [daftar grup replikasi](https://console.cloud.tencent.com/redis/replication), klik <img src="https://qcloudimg.tencent-cloud.cn/raw/3a815073e7ccf4206decf7b522a40ccd.png" style="zoom: 67%;" /> sebelum nama grup replikasi target untuk menampilkan daftar instansnya.
2. Temukan instans target dan klik **Remove from Replication Group** (Hapus dari Grup Replikasi) di kolom **Operation** (Operasi).
> !Anda tidak dapat menghapus sebuah instans jika instans tersebut adalah satu-satunya instans master dalam grup replikasi tempat instans baca saja ada.
3. Di jendela pop-up **Remove from Replication Group** (Hapus dari Grup Replikasi), konfirmasikan informasi instans.
Jika instans yang akan dihapus adalah instans master, Anda harus memilih  **removal mode** (mode penghapusan) dan klik **OK** (OKE).
   - **Hapus sekarang**: Dalam mode ini, sistem segera memutuskan sinkronisasi data dalam grup replikasi, tanpa menunggu node lain menyelesaikan sinkronisasi data dari instans master ini. Beberapa data mungkin hilang.
   - **Setelah sinkronisasi data selesai**: Dalam mode ini, sistem menetapkan instans master sebagai baca saja, menunggu node lain dalam grup replikasi untuk menyelesaikan sinkronisasi data dari instans tersebut, memutus replikasi antara instans tersebut dan semua node lain dalam grup replikasi, menghapusnya dari grup replikasi, membatalkan status baca saja instans tersebut, lalu mengaktifkan akses tulisnya.
4. Dalam daftar instans grup replikasi, **instance status** (status instans) berubah menjadi **remove instance** (hapus instans). Tunggu hingga penghapusan selesai.

## Menghapus Grup Replikasi
Anda harus menghapus semua instans dalam grup replikasi sebelum Anda dapat menghapus grup tersebut.

1. Di [daftar grup replikasi](https://console.cloud.tencent.com/redis/replication), pilih grup replikasi target dan klik **Delete Replication Group** (Hapus Grup Replikasi) di kolom **Operation** (Operasi).
![](https://qcloudimg.tencent-cloud.cn/raw/a3d9cc9c83d7fb18fba127720d00d417.png)
2. Di jendela pop-up **Delete Replication Group** (Hapus Grup Replication), konfirmasikan informasi grup replikasi dan klik **OK** (OKE).

