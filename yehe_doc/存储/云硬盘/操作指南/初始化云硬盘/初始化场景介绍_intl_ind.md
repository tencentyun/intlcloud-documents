Disk cloud yang dibuat melalui konsol dipasang secara manual ke CVM Anda dan digunakan sebagai disk data dalam status Online secara default.Untuk menggunakan disk, Anda harus menginisialisasinya terlebih dahulu, termasuk memformat, mempartisi, dan membuat sistem file.Metode inisialisasi berbeda berdasarkan skenario penggunaan aktual seperti yang ditunjukkan di bawah ini:
- Jika seluruh disk disajikan sebagai satu partisi terpisah (yaitu, tidak ada beberapa disk logis seperti disk D/vdb1 dan disk E/vdb2), kami sangat menyarankan Anda untuk tidak menggunakan partisi, dan langsung membuat sistem file pada perangkat kosong.
- Jika seluruh disk perlu disajikan sebagai beberapa partisi logis (yaitu, ada beberapa disk logis), Anda harus mempartisi disk terlebih dahulu, kemudian membuat sistem file pada partisi.

Gaya partisi disk yang umum adalah Main Boot Record (MBR) dan Guid Partition Table (GPT).Jika format partisi disk diubah setelah disk digunakan, data asli pada disk akan dihapus.Oleh karena itu, pilihlah gaya partisi yang sesuai dengan kebutuhan aktualnya.
Dasar-dasar dari dua gaya partisi tersebut ditunjukkan pada tabel berikut:

| Gaya partisi | Kapasitas disk maksimum yang didukung | Jumlah partisi yang didukung | Alat partisi |
|---------|---------|---------|---------|
|MBR | 2 TB |<li>4 partisi utama</li><li>3 partisi utama dan 1 partisi tambahan</li>|Sistem operasi Windows:Manajemen disk</br>Sistem operasi Linux:<ul><li>alat fdisk</li><li>alat parted</li></ul> |
|GPT | 18EB</br>Saat ini, disk cloud mendukung kapasitas maksimum 32 TB | Tidak ada batasan jumlah partisi | Sistem operasi Windows:Manajemen disk</br>Sistem operasi Linux: alat parted|

Pilih panduan operasi yang sesuai berdasarkan kapasitas disk dan sistem operasi CVM:
- Untuk kapasitas disk kurang dari 2 TB:
- [Menginisialisasi disk cloud (Windows)](https://intl.cloud.tencent.com/document/product/362/31597#Steps)
- [Menginisialisasi disk cloud (Linux)](https://intl.cloud.tencent.com/document/product/362/31597#Steps)
- Untuk kapasitas disk yang lebih besar dari atau sama dengan 2 TB:
- [Menginisialisasi disk cloud (Windows)](https://intl.cloud.tencent.com/document/product/362/31598#Steps)
- [Menginisialisasi disk cloud (Linux)](https://intl.cloud.tencent.com/document/product/362/31598#Steps)









