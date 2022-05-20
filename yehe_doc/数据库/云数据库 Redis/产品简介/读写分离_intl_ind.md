
TencentDB for Redis mendukung pemisahan baca-tulis untuk skenario bisnis dengan lebih banyak pembacaan tetapi lebih sedikit penulisan, yang dapat mengatasi permintaan baca yang berkonsentrasi pada data yang sering dibaca dengan baik. Mendukung hingga mode 1-master 5-replika untuk menawarkan performa baca 5x.

## Cara Kerjanya
#### Edisi Memori
- **Prinsip pemisahan baca/tulis**: TencentDB for Redis v4.0 dan yang lebih baru dalam arsitektur standar atau arsitektur kluster menerapkan pemisahan baca/tulis otomatis pada lapisan Proksi.
- **Bobot pemisahan baca-tulis**: setelah pemisahan baca/tulis diaktifkan, Proksi akan mengaktifkan akses dengan mengarahkan permintaan tulis ke node master saja dan mendistribusikan permintaan baca secara merata pada node replika.
![](https://main.qcloudimg.com/raw/ebdf223270b8bfbc250036470e96e3a7.png)

#### Edisi CKV
- **Prinsip pemisahan baca/tulis**: Edisi CKV secara inheren mendukung arsitektur pemisahan baca/tulis. Semua permintaan didistribusikan ke node dalam kluster melalui gateway CLB, dan setiap node memiliki informasi perutean slot global. Setelah pemisahan baca/tulis diaktifkan untuk sebuah node, jika kunci baca ditekan, data akan dibaca secara langsung dan dikembalikan; jika tidak, permintaan akan diteruskan ke node yang terkait, sesuai informasi peruteannya, yang akan membaca data dan mengembalikannya ke node ini untuk pengembalian akhir ke klien.
- **Bobot pemisahan baca/tulis**: permintaan dalam Edisi CKV didistribusikan oleh CLB, jadi bobot baca dan tulis didistribusikan secara merata sesuai dengan empat kali lipat koneksi TCP (IP sumber, port sumber, IP tujuan, dan port tujuan).
![](https://main.qcloudimg.com/raw/3003faec1d3e55e4f3915532707a203d.png)
