## Ikhtisar Fitur
- Replika data online secara real-time
Snapshot adalah salinan disk cloud yang dapat digunakan secara maksimal.Saat terjadi masalah pada disk cloud yang snapshotnya telah dibuat, status sebelum masalah terjadi dapat dipulihkan dengan cepat menggunakan snapshot.Kami menyarankan Anda membuat snapshot untuk disk cloud terkait sebelum membuat perubahan besar pada bisnis Anda sehingga data dapat dipulihkan dengan cepat jika terjadi kegagalan perubahan bisnis.
- Pencadangan terus-menerus pada tonggak pencapaian penting
Snapshot dapat digunakan sebagai cadangan data bisnis yang terus-menerus untuk menjaga status tonggak pencapaian data bisnis.
- Deployment bisnis yang cepat
Anda dapat menggunakan snapshot bisnis Anda untuk mengklona beberapa disk cloud dengan cepat sehingga mencapai deployment server yang cepat.

## Skenario
Merupakan layanan perlindungan data yang nyaman dan efisien, snapshot direkomendasikan untuk skenario bisnis berikut:
- Pencadangan data harian
Anda dapat menggunakan snapshot untuk secara teratur mencadangkan data bisnis penting untuk mengatasi kehilangan data yang disebabkan oleh kesalahan operasi, serangan, virus, dll.
- Pemulihan data yang cepat
Sebelum melakukan operasi besar seperti beralih sistem operasi, meningkatkan aplikasi, atau memigrasikan data bisnis, Anda dapat membuat satu atau beberapa snapshot.Jika terjadi masalah saat membuat perubahan ini, Anda dapat memulihkan data bisnis menggunakan snapshot yang telah Anda buat.
- Penerapan beberapa replika data produksi
Anda dapat menyediakan data produksi aktual hampir secara waktu nyata untuk penerapan seperti penambangan data, kueri laporan, dan pengujian pengembangan dengan membuat snapshot data produksi.
- Deployment lingkungan yang cepat
Anda dapat membuat snapshot dari CVM dan menggunakan snapshot tersebut untuk membuat image khusus.Anda dapat menggunakan image ini untuk membuat satu atau beberapa instance CVM dengan cepat, men-deploy beberapa CVM dengan lingkungan yang sama dalam satu batch untuk menghemat waktu yang dihabiskan untuk konfigurasi duplikat.

## Penagihan
Untuk informasi penagihan mendetail tentang layanan snapshot, silakan lihat [Ikhtisar penagihan snapshot](https://intl.cloud.tencent.com/document/product/362/32415) dan [Ikhtisar Penagihan](https://intl.cloud.tencent.com/document/product/362/2413).

## Batas Kuota
Untuk detail tentang batas kuota snapshot, lihat [Batas Layanan](https://intl.cloud.tencent.com/document/product/362/5145).

## Jenis Snapshot
- Snapshot Manual
Anda dapat membuat snapshot untuk data disk cloud secara manual pada titik waktu tertentu.Snapshot ini dapat digunakan untuk membuat lebih banyak disk cloud dengan data yang identik, atau untuk memulihkan disk cloud ke status saat ini nanti.Untuk informasi selengkapnya, lihat [Membuat Snapshot](https://intl.cloud.tencent.com/document/product/362/5755).
- Snapshot Terjadwal
Untuk bisnis yang terus diperbarui, Anda dapat menggunakan snapshot terjadwal untuk membuat cadangan data berkelanjutan.Untuk mencapai pencadangan berkelanjutan data disk cloud selama periode tertentu, Anda hanya perlu mengonfigurasi kebijakan pencadangan dan mengaitkannya dengan disk cloud, yang secara signifikan meningkatkan keamanan data.Untuk informasi selengkapnya, lihat [Snapshot Terjadwal](https://intl.cloud.tencent.com/document/product/362/31622).

> Selama pembuatan snapshot, data aplikasi yang disimpan dalam memori mungkin tidak disimpan secara terus-menerus, menyebabkan snapshot tidak dapat menangkap data disk cloud terbaru dan paling lengkap.Lihat [Catatan]) untuk memastikan konsistensi data snapshot.


## Tinjauan Kasus
#### Kasus 1:Kegagalan pembuatan snapshot secara manual sebelum operasi berisiko tinggi, yaitu dapat menyebabkan kehilangan data
**Detail**:Pelanggan A tidak pernah membuat snapshot untuk disk cloud.Pada Mei 2019, seorang operator melakukan uji fio pada disk cloud.Sistem file rusak dan data tidak dapat dipulihkan.
**Analisis**:Jika pelanggan A telah membuat snapshot untuk disk cloud sebelum pengujian, pelanggan tersebut dapat mengaktifkan pengembalian snapshot setelah terjadi kerusakan data untuk segera memulihkan bisnis.

#### Kasus 2:Kegagalan pembuatan snapshot terjadwal untuk disk data penting dapat menyebabkan kehilangan data
**Detail**:Pelanggan B membuat snapshot untuk beberapa disk cloud, tetapi tidak untuk disk cloud yang baru dibeli setelah Januari 2019 karena masalah biaya.Pada Juni 2019, disk cloud yang tidak dilindungi oleh snapshot mengalami kehilangan data yang tidak dapat dipulihkan karena penghapusan data file lapisan sistem secara tidak sengaja.
**Analisis**:Jika pelanggan B telah membuat snapshot terjadwal untuk disk cloud ini, pelanggan tersebut dapat memulihkan data ke status pada titik waktu snapshot sebelumnya sehingga meminimalkan kerugian setelah penghapusan data yang tidak disengaja.Setelah insiden tersebut, pelanggan B telah membuat snapshot untuk disk cloud tersebut guna meningkatkan perlindungan data.

#### Kasus 3:Mengembalikan data dengan snapshot terjadwal untuk memulihkan bisnis setelah terjadi kesalahan pengoperasian
**Detail:** Pelanggan C membuat snapshot untuk semua disk cloud.Pada Mei 2019, pengecualian startup terjadi karena kesalahan pengoperasian.
**Analisis**:Pelanggan C segera memulihkan data menggunakan snapshot terjadwal yang diambil dua hari lalu, dan bisnis tidak terpengaruh.


Dalam kasus di atas, kesalahan pengoperasian menyebabkan kehilangan data.Sebagai perbandingan, kami menemukan bahwa:
- Dalam situasi ketika **snapshot belum dibuat**, pemulihan data sulit dilakukan ketika pengecualian server atau disk cloud terjadi sehingga menyebabkan kerugian besar.
ka- Dalam situasi ketika **snapshot telah dibuat**, data dapat dipulihkan saat pengecualian server atau disk cloud terjadi sehingga meminimalkan kerugian.

Kami menyarankan Anda secara teratur membuat snapshot untuk bisnis berdasarkan jenisnya, meningkatkan keamanan data, dan mencapai pemulihan bencana dengan biaya rendah dan efisiensi tinggi.

## Lainnya
Untuk pertanyaan lainnya, lihat [Pertanyaan Umum Snapshot](https://intl.cloud.tencent.com/document/product/362/17820).







