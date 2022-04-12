## Ikhtisar
TencentDB for MySQL memungkinkan Anda membuat satu atau beberapa instans baca saja, yang cocok untuk pemisahan baca/tulis dan skenario aplikasi satu-sumber-banyak-replika dan dapat meningkatkan kapasitas beban baca database Anda secara signifikan.
Alamat pemisahan baca/tulis terpadu (yaitu, permintaan baca dan tulis dipisahkan secara otomatis) tidak didukung saat ini. Instans Baca Saja perlu diakses dengan IP dan port terpisah.
>?
>- Untuk harga instans baca saja, lihat [Harga Produk](https://buy.Intl.cloud.tencent.com/price/cdb).
- Instans baca saja mendukung konfigurasi alamat jaringan pribadi pada halaman detail Instans, dan mendukung modifikasi kustom IP dan port pribadi.

#### Konsep
- Grup Baca Saja: terdiri dari satu atau beberapa instans baca saja yang mengaktifkan penyeimbangan beban. Jika ada beberapa instans baca saja dalam satu grup baca saja, volume permintaan baca dapat didistribusikan secara merata di antara instans. grup baca saja menyediakan IP dan port untuk akses ke database.
- Instans Baca Saja: instans node tunggal (tanpa replika) yang mendukung permintaan baca. Instans tidak bisa berdiri secara independen; sehingga harus dalam grup baca saja.

#### Arsitektur
Fitur sinkronisasi binlog replika sumber MySQL diadopsi untuk instans baca saja, yang dapat menyinkronkan perubahan dalam instans sumber (database sumber) ke semua instans baca saja. Mengingat arsitektur node tunggal (tanpa replika) dari instans baca saja, upaya berulang untuk memulihkan instans baca saja yang gagal akan dilakukan. Dengan demikian, sebaiknya pilih grup RO daripada instans baca saja untuk ketersediaan yang lebih tinggi.
![](https://main.qcloudimg.com/raw/bf2ef3ecfc232f6e69a99ead319a5cb2.png)

## Batasan Fitur
- Instans baca saja hanya dapat dibeli untuk **two-node or three-node source instances on MySQL 5.6 or above with the InnoDB engine at a specification of 1 GB memory and 50 GB disk capacity or above** (instans sumber dua node atau tiga node pada MySQL versi 5.6 atau yang lebih tinggi dengan mesin InnoDB dengan spesifikasi memori 1 GB dan kapasitas disk 50 GB atau yang lebih tinggi). Jika instans sumber Anda di bawah spesifikasi ini, tingkatkan terlebih dahulu.
- Spesifikasi minimum instans baca saja adalah memori 1 GB dan kapasitas disk 50 GB dan harus lebih besar dari atau sama dengan ukuran penyimpanan instans sumber yang dibeli.
- Instans sumber dapat membuat hingga 5 instans baca saja.
- Fitur pencadangan dan pengembalian tidak didukung.
- Data tidak dapat dimigrasikan ke instans baca saja.
- Pembuatan/penghapusan database tidak didukung dan begitu juga dengan phpMyAdmin (PMA).
- Operasi termasuk pembuatan/penghapusan/otorisasi akun dan nama akun/modifikasi kata sandi tidak didukung.

## Catatan
- Tidak perlu memelihara akun atau database untuk instans baca saja, yang disinkronkan dengan instans sumber.
- Jika versi MySQL adalah 5.6 tetapi GTID tidak diaktifkan, Anda harus mengaktifkan GTID di konsol terlebih dahulu sebelum membuat instans baca saja.
Operasi memerlukan waktu lama, dan instans akan terputus selama beberapa detik. Sebaiknya lakukan proses ini selama jam tidak sibuk dan tambahkan mekanisme koneksi ulang dalam program yang mengakses database.
- Instans baca saja hanya mendukung mesin InnoDB.
- Inkonsistensi data antara beberapa instans baca saja dapat terjadi karena penundaan sinkronisasi data antara instans baca saja dan instans sumber. Anda dapat memeriksa penundaan di konsol.
- Spesifikasi instans baca saja bisa berbeda dari instans sumber, yang memudahkan Anda untuk meningkatkan instans baca saja sesuai dengan bebannya. Sebaiknya Anda menyimpan spesifikasi yang sama dari instans baca saja dalam satu grup RO.

## Petunjuk
1. Login ke [konsol TencentDB for MySQL](https://console.cloud.tencent.com/cdb/). Dalam daftar instans, klik ID instans atau **Manage** (Kelola) di kolom **Operation** (Operasi) untuk mengakses halaman detail instans.
2. Klik **Add Read-Only Instans** (Tambahkan Instans Baca Saja) di bagian **Instance Architecture Diagram** (Diagram Arsitektur Instans) pada tab **Instance Details** (Detail Instans) atau klik **Create** (Buat) pada tab **Read-Only Instance** (Instans Baca Saja).
3. Pada halaman pembelian yang ditampilkan, tentukan konfigurasi instans baca saja berikut, konfirmasikan bahwa semuanya sudah benar, dan klik **Buy Now** (Beli Sekarang).
 - **Specify RO Group** (Tentukan Grup RO): Anda dapat menggunakan grup RO yang ditetapkan secara otomatis oleh alokasi sistem, membuatnya, atau memilih grup yang sudah ada.
    - **Assigned by system** (Ditetapkan oleh sistem): jika beberapa instans dibeli sekaligus, masing-masing akan ditetapkan ke grup RO independen, dan bobotnya akan ditetapkan secara otomatis oleh sistem secara default.
    - **Create RO group** (Buat grup RO): membuat grup RO. Jika beberapa instans dibeli sekaligus, semuanya akan ditetapkan ke grup RO baru ini, dan bobotnya akan dialokasikan oleh sistem secara otomatis secara default.
    - **Existing RO group** (Grup RO yang sudah ada): menentukan grup RO yang ada. Jika beberapa instans baca saja
    dibeli sekaligus, semuanya akan ditetapkan ke grup RO.
    Bobot mereka akan dialokasikan sebagaimana dikonfigurasi dalam grup RO. Jika penetapan oleh sistem diatur untuk grup RO, instans akan ditambahkan ke grup secara otomatis sesuai dengan spesifikasi yang dibeli. Jika diatur ke alokasi kustom, bobotnya akan menjadi nol secara default.
		Karena IP pribadi yang sama dibagikan dalam grup RO, jika VPC digunakan, setelan grup keamanan yang sama akan dibagikan. Jika grup RO ditentukan, tidak mungkin untuk menyesuaikan grup keamanan apa pun saat instans dibeli.
 - Hapus Instans RO Tertunda: opsi ini menunjukkan apakah akan mengaktifkan kebijakan penghapusan. Jika instans baca saja dihapus saat penundaannya melebihi ambang batas, instans tersebut akan menjadi tidak aktif, bobotnya akan diatur ke 0 secara otomatis, dan pemberitahuan peringatan akan dikirim (untuk informasi selengkapnya tentang cara mengonfigurasi alarm penghapusan instans baca saja dan penerima, lihat [Fitur Alarm](https://intl.cloud.tencent.com/document/product/236/8457). Instans akan dimasukkan kembali ke grup RO saat penundaannya berada di bawah ambang batas. Terlepas dari apakah opsi ini diaktifkan, instans baca saja yang dihapus karena kegagalan instans akan bergabung kembali dengan grup RO saat diperbaiki.
![](https://main.qcloudimg.com/raw/5c002d37fdeb72a5396a394133672338.png)
4. Setelah selesai melakukan pembelian, Anda akan dialihkan ke daftar instans. Setelah status instans baca saja ditampilkan sebagai **Running** (Berjalan), instans tersebut dapat digunakan secara normal.

## Pertanyaan Umum
#### Apa aturan untuk menghapus instans baca saja?
Setelah **Remove Delayed RO Instances** (Hapus Instans RO Tertunda) diaktifkan, grup RO akan menentukan aturan penghapusan berdasarkan ambang batas penundaan dan nilai "Instans RO Terkecil". Jika penundaan instans baca saja mencapai ambang batas, instans tersebut akan dihapus dan dibuat tidak aktif, dengan bobotnya diatur ke 0 dan alarm dikirim ke pengguna. Ketika berada di bawah ambang batas, penundaannya akan dikembalikan ke grup RO.
- Ambang Batas Penundaan: ini menetapkan ambang batas penundaan untuk instans baca saja. Jika ambang batas terlampaui, instans akan dihapus dari grup baca saja.
- Instans RO Terkecil: ini adalah jumlah minimum instans yang harus dipertahankan dalam grup baca saja. Ketika ada lebih sedikit instans dalam grup baca saja, meski melebihi ambang batas penundaan, instans tidak akan dihapus.

#### Jika instans baca saja dihentikan atau dikembalikan, bagaimana instans sumber akan terpengaruh?
Penghentian dan pengembalian instans baca saja tidak berdampak pada instans sumber.
