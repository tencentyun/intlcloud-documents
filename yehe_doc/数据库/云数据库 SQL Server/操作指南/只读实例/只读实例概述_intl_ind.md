
## Ikhtisar
Dalam skenario di mana ada banyak permintaan baca tetapi hanya sedikit permintaan tulis, satu instans mungkin tidak dapat menangani beban permintaan baca, yang bahkan dapat memengaruhi bisnis. Untuk menerapkan penskalaan otomatis kemampuan baca dan mengurangi tekanan pada TencentDB for SQL Server, Anda dapat membuat satu atau beberapa instans baca saja dan menggunakannya untuk mempertahankan jumlah pembacaan database yang tinggi.

Alamat pemisahan baca/tulis terpadu (yaitu, permintaan baca dan tulis dipisahkan secara otomatis) tidak didukung saat ini. Instans Baca Saja perlu diakses dengan IP dan port terpisah.

#### Konsep
- Grup Baca Saja: terdiri dari satu atau beberapa instans baca saja yang mengaktifkan penyeimbangan beban. Jika ada beberapa instans baca saja dalam satu grup baca saja, volume permintaan baca dapat didistribusikan secara merata di antara instans. grup baca saja menyediakan IP dan port untuk akses ke database.
- Instans Baca Saja: instans node tunggal (tanpa replika) yang mendukung permintaan baca. Instans tidak bisa berdiri secara independen; sehingga harus dalam grup baca saja.

#### Arsitektur
Perubahan pada instans utama (database sumber) disinkronkan ke semua instans baca saja. Mengingat arsitektur node tunggal (tanpa replika) dari instans baca saja, upaya berulang untuk memulihkan instans baca saja yang gagal akan dilakukan. Dengan demikian, sebaiknya pilih grup baca saja daripada instans baca saja untuk ketersediaan yang lebih tinggi.

Arsitektur dan teknologi backend instans baca saja sedikit berbeda berdasarkan edisi TencentDB for SQL Server:
- Pada edisi di bawah 2017 Enterprise, metode publikasikan/langganan digunakan untuk membuat instans baca saja.
![](https://qcloudimg.tencent-cloud.cn/raw/8da3f1fd5e18cd5ab42f9c2d7731ebda.png)
>!Dalam mode ini, tabel tanpa kunci primer di instans utama tidak dapat disinkronkan. Anda dapat menggunakan kode berikut untuk mengkueri apakah ada tabel seperti itu:
```
menggunakan dbname
pilih nama dari sys.sysobjects dengan xtype='U' dan id tidak ada (pilih parent_obj dari sys.sysobjects dengan xtype='PK')
```
Jika Anda perlu membuat instans baca saja untuk tabel tanpa kunci primer, sebaiknya gunakan Edisi Kluster Perusahaan 2017.
- Pada Edisi Kluster Perusahaan 2017 dan yang lebih tinggi, metode Always-On digunakan untuk membuat instans baca saja untuk memastikan efisiensi dan stabilitas sinkronisasi data.
![](https://qcloudimg.tencent-cloud.cn/raw/c3cee7a40aad567b1bb56811f88d6785.png)


## Keunggulan
#### Mode grup Baca Saja
Anda dapat terhubung ke VIP grup baca saja untuk membaca instans baca saja di dalamnya, yang dapat mengurangi biaya pemeliharaan. Anda juga dapat menambahkan jumlah instans baca saja dalam grup baca saja terpadu untuk terus memperluas kapasitas pemrosesan sistem sembari memastikan ketersediaan tinggi instans baca-saja, tanpa perlu membuat perubahan apa pun pada aplikasi.

#### Penskalaan lintas-AZ/wilayah
TencentDB for SQL Server mendukung penambahan instans baca saja di seluruh AZ dan wilayah, memberikan solusi satu atap dengan latensi rendah, efisiensi tinggi, dan stabil untuk akses bisnis di sekitar.

#### Penghapusan otomatis
Modul manajemen kluster secara otomatis memeriksa instans baca saja. Saat menemukan bahwa instans baca saja sedang tidak dapat digunakan atau penundaan melebihi ambang batas, ia berhenti mengalokasikan permintaan baca ke instans dan mengalokasikannya di antara instans sehat yang tersisa. Ini memastikan bahwa saat satu instans baca saja gagal, akses normal ke aplikasi tidak akan terpengaruh. Saat instans yang gagal diperbaiki, ini akan secara otomatis ditambahkan kembali ke sistem distribusi permintaan.


## Batasan Fitur
- Maksimal 3 instans baca saja dapat dibuat untuk instans utama.
- Saat ini, instans baca saja tidak didukung untuk Edisi Standar.
- Saat ini, instans baca saja tidak dapat ditambahkan ke instans di zona keuangan.
- Instans Baca Saja tidak mendukung pencadangan dan pengembalian.
- Data tidak dapat dimigrasikan ke instans baca saja.
- Instans Baca Saja tidak mendukung pembuatan/penghapusan database. Jika diperlukan, silakan operasikan pada instans utama.
- Instans Baca Saja tidak mendukung pembuatan/penghapusan/otorisasi akun dan perubahan nama/kata sandi akun. Jika diperlukan, silakan operasikan pada instans utama.
