Network Access Control List (ACL) adalah lapisan keamanan opsional yang membatasi lalu lintas ke dan dari subnet yang akurat ke protokol dan port.

## Ikhtisar
Anda dapat menghubungkan ACL jaringan dengan beberapa subnet untuk mempertahankan lalu lintas yang sama dan mengontrol arus masuk dan keluarnya secara tepat dengan menetapkan aturan masuk dan keluar.
Misalnya, saat menghosting aplikasi web multi-lapisan di instans Tencent Cloud VPC dan membuat subnet yang berbeda untuk layanan lapisan web, lapisan logis, dan lapisan data, Anda dapat menggunakan ACL jaringan untuk memastikan bahwa lapisan web dan subnet lapisan data tidak dapat mengakses satu sama lain, tetapi hanya subnet lapisan logis yang dapat mengakses subnet lapisan web dan lapisan data.
![](https://main.qcloudimg.com/raw/f8490b4c94db7cd50f2cbe29524d237d.jpg)


## Aturan ACL
Saat aturan ACL jaringan ditambahkan atau dihapus, perubahan akan diterapkan ke subnet terhubung secara otomatis.
Anda dapat mengonfigurasi aturan ACL jaringan masuk dan keluar. Setiap aturan terdiri dari:
+ IP Sumber/IP tujuan: masukkan IP sumber untuk aturan masuk atau IP tujuan untuk aturan keluar. Format yang didukung:
  + IP tunggal: seperti “192.168.0.1” atau “FF05::B5”
  + Blok CIDR: seperti “192.168.1.0/24” atau “FF05:B5::/60”
  + Semua alamat IPv4: “0.0.0.0/0”
- Jenis protokol: menunjukkan jenis protokol yang diizinkan atau ditolak oleh aturan ACL, misalnya, TCP dan UDP.
- Port: menunjukkan port sumber atau tujuan lalu lintas. Format yang didukung:
  + Port tunggal: seperti "22" atau "80"
  + Rentang port: seperti "1-65535" atau "100-20000"
  + Semua port: Semua
- Kebijakan: menunjukkan apakah akan mengizinkan atau menolak permintaan akses.

### Aturan default
Setelah dibuat, setiap ACL jaringan memiliki dua aturan default yang tidak dapat diubah atau dihapus, dengan prioritas terendah.
- Aturan masuk default
<table>
<thead>
<tr>
<th>Jenis Protokol</th>
<th>Port</th>
<th>Sumber IP</th>
<th>Kebijakan</th>
<th>Deskripsi</th>
</tr>
</thead>
<tbody><tr>
<td>Semua</td>
<td>Semua</td>
<td>0.0.0.0/0</td>
<td>Tolak</td>
<td>Menolak semua lalu lintas masuk.</td>
</tr>
</tbody></table>

- Aturan keluar default
<table>
<thead>
<tr>
<th>Jenis Protokol</th>
<th>Port</th>
<th>IP tujuan</th>
<th>Kebijakan</th>
<th>Deskripsi</th>
</tr>
</thead>
<tbody><tr>
<td>Semua</td>
<td>Semua</td>
<td>0.0.0.0/0</td>
<td>Tolak</td>
<td>Menolak semua lalu lintas keluar.</td>
</tr>
</tbody></table>

### Prioritas aturan
- Aturan jaringan ACL diprioritaskan dari atas ke bawah. Aturan di bagian atas daftar memiliki prioritas tertinggi dan akan berlaku lebih dulu, sedangkan aturan di bagian bawah memiliki prioritas terendah dan akan berlaku terakhir.
- Jika ada konflik aturan, aturan dengan prioritas lebih tinggi akan berlaku secara default.
- Ketika lalu lintas masuk atau keluar dari subnet yang terikat ke jaringan ACL, aturan ACL jaringan akan dicocokkan secara berurutan dari atas ke bawah. Jika aturan berhasil dicocokkan dan berlaku, aturan berikutnya tidak akan cocok.

#### Contoh aplikasi
Untuk mengizinkan semua alamat IP sumber mengakses semua port CVM di subnet yang terhubung ke ACL jaringan dan menolak alamat IP sumber HTTP `192.168.200.11/24` untuk mengakses port 80, tambahkan dua aturan ACL jaringan berikut untuk lalu lintas masuk:

| Jenis Protokol | Port | IP Sumber | Kebijakan | Deskripsi |
| --- | --- | --- | --- |---|
| HTTP | 80 | 192.168.200.11/24 | Tolak | Menolak alamat IP layanan HTTP ini untuk mengakses port 80. |
| Semua | Semua | 0.0.0.0/0 | Izinkan | Mengizinkan semua alamat IP sumber mengakses semua port. |


## Grup Keamanan vs. ACL Jaringan
<table>
<thead>
<tr>
<th width="12%">Item</th>
<th width="45%">Grup Keamanan</th>
<th width="43%">Jaringan ACL</th>
</tr>
</thead>
<tbody><tr>
<td>Pelambatan lalu lintas</td>
<td>Pelambatan lalu lintas di tingkat instans, seperti CVM dan database</td>
<td>Pelambatan lalu lintas di tingkat subnet</td>
</tr>
<tr>
<td>Aturan</td>
<td>Aturan izinkan dan tolak</td>
<td>Aturan izinkan dan tolak</td>
</tr>
<tr>
<td>Stateful atau stateless</td>
<td>Stateful: lalu lintas yang dikembalikan secara otomatis diizinkan tanpa tunduk pada aturan apa pun.</td>
<td>Stateless: lalu lintas yang dikembalikan harus secara eksplisit diizinkan oleh aturan.</td>
</tr>
<tr>
<td>Waktu efektif</td>
<td>Aturan diterapkan ke instans, seperti CVM atau TencentDB,kecuali Anda menentukan grup keamanan saat membuat instans atau menghubungkan grup keamanan ke instans setelah dibuat.</td>
<td>Aturan ACL diterapkan secara otomatis ke semua instans, seperti instans CVM dan TencentDB di subnet terhubung.</td>
</tr>
<tr>
<td>Prioritas aturan</td>
<td>Jika terjadi konflik aturan, aturan dengan prioritas lebih tinggi akan berlaku secara default.</td>
<td>Jika terjadi konflik aturan, aturan dengan prioritas lebih tinggi akan berlaku secara default.</td>
</tr>
</tbody></table>
