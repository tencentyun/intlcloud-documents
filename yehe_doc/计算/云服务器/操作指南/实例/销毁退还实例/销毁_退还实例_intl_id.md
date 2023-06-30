Artikel ini menjelaskan cara menghentikan dan melepas instans Cloud Virtual Machine (CVM). Untuk informasi selengkapnya tentang kedaluwarsa, lihat [Pemberitahuan Kedaluwarsa](https://intl.cloud.tencent.com/document/product/213/2181).

## Ikhtisar

Jika Anda tidak lagi membutuhkan instans, Anda dapat menghentikannya. Instans yang dihentikan akan dipindahkan ke Keranjang Sampah. Anda dapat memperbarui, memulihkan, atau melepaskan instans di Keranjang Sampah.

>! Jika akun Anda lewat jatuh tempo, Anda perlu menambahkan dana sebelum memulihkan instans bayar sesuai pemakaian.
>

Anda dapat menggunakan metode berikut untuk menghentikan dan melepaskan instans bayar sesuai pemakaian:
 - **Manual termination:** (Penghentian manual:) jika akun Anda bereputasi baik, Anda dapat menghentikan instans bayar sesuai pemakaian secara manual. Instans bayar sesuai pemakaian dilepaskan setelah tetap berada di keranjang sampah selama lebih dari 2 jam.
 - **Scheduled termination:** (Penghentian terjadwal:) Anda dapat menjadwalkan waktu (hingga detik) untuk secara otomatis menghentikan instans bayar sesuai pemakaian. Anda dapat memilih waktu mendatang untuk menghentikan sumber daya. Instans yang dihentikan menggunakan penghentian terjadwal akan melewati keranjang sampah dan segera dilepaskan. Anda dapat [membatalkan penghentian terjadwal](https://intl.cloud.tencent.com/document/product/213/4930) kapan saja sebelum waktu yang dijadwalkan.
 - **Automatic termination upon expiration or when account is overdue** (Penghentian otomatis setelah kedaluwarsa atau saat akun lewat jatuh tempo): instans bayar sesuai pemakaian dengan saldo di bawah 0 akan otomatis dilepaskan setelah 2 jam dan 15 hari. Selama 2 jam pertama, penagihan berlanjut dan Anda masih dapat menggunakan instans. Namun, selama 15 hari ke depan, instans akan ditutup, dan penagihan akan dihentikan. Instans bayar sesuai pemakaian tidak dapat dipindahkan ke keranjang sampah setelah akun Anda lewat jatuh tempo. Sebagai gantinya, Anda perlu memeriksa instans di daftar instans CVM. Anda dapat terus menggunakan instans jika Anda [memperpanjangnya](https://intl.cloud.tencent.com/document/product/213/6143) dalam waktu yang ditentukan.

| | Penghentian manual (tidak melewati jatuh tempo) | Penghentian terjadwal (tidak melewati jatuh tempo) | Penghentian otomatis setelah kedaluwarsa atau saat akun lewat jatuh tempo |
|---------|---------|---------|---------|
| Instans bayar sesuai pemakaian | Setelah penghentian, instans bayar sesuai pemakaian akan dilepas setelah disimpan di keranjang sampah selama maksimal 2 jam. |Instans yang penghentian waktunya diatur akan segera dilepas sesuai jadwal, bukan masuk ke keranjang sampah. | Saat akun Anda melewati jatuh tempo, selama 2 jam pertama, penagihan berlanjut dan Anda masih dapat menggunakan instans. Namun, selama 15 hari ke depan, instans akan ditutup, dan penagihan akan dihentikan. Instans bayar sesuai pemakaian tidak dipindahkan ke keranjang sampah setelah akun Anda lewat jatuh tempo. Jika instans tidak diperpanjang dalam periode ini, instans akan dilepas.|



## Dampak
Apa yang terjadi pada data, EIP, dan biaya instans setelah dihentikan:
- **Billing** (Penagihan): setelah instans dihentikan atau dilepaskan, tidak ada biaya lagi yang akan dikenakan.
- **Instance Data:** (Data instans:) disk lokal dan disk cloud non-elastis yang dipasang ke instans semuanya dilepaskan, dan data pada disk ini hilang. Cadangkan data terlebih dahulu. Disk cloud elastis mengikuti siklus prosesnya sendiri.
- **EIP:** (EIP:) EIP (termasuk alamat IP pada ENI sekunder) dari instans yang dihentikan akan dipertahankan, dan alamat IP yang tidak aktif dapat dikenakan biaya. Jika Anda tidak membutuhkannya lagi, lepaskannya sesegera mungkin.



## Mengakhiri dan Melepas Instans Bayar Sesuai Pemakaian

Untuk instans bayar sesuai pemakaian, Anda dapat memilih penghentian segera atau penghentian terjadwal.

### Mengakhiri instans menggunakan Konsol

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/).
2. Pilih salah satu metode berikut:
    - **Terminate a single instance** (Hentikan satu instans): temukan instans yang diinginkan dalam daftar dan klik **More** (Lainnya) -> **Instance Status** (Status Instans) -> **Terminate/Return** (Hentikan/Tampilkan) di sisi kanan.
    - **Terminate instances in batches** (Hentikan instans secara massal): pilih semua instans yang diinginkan dan klik **More** (Lainnya) -> **Terminate/Return** (Hentikan/Tampilkan) di bagian atas antarmuka. Untuk kasus yang tidak dapat dihentikan, alasannya akan ditampilkan.
3. Di jendela pop-up, pilih **Immediate Termination** (Penghentian Segera) atau **Scheduled Termination** (Penghentian Terjadwal).
 	 - **Immediate Termination** (Penghentian Segera): Anda dapat memilih untuk segera melepaskan sumber daya atau dalam 2 jam. Jika Anda memilih untuk segera melepaskan sumber daya, data instans akan dihapus dan tidak dapat dipulihkan.
 	 - **Scheduled Termination** (Penghentian Terjadwal): jika Anda memilih penghentian terjadwal, Anda perlu menentukan waktu penghentian. Instans dihentikan dan dilepas pada saat itu dan data tidak dapat dipulihkan.
4. Klik **Next** (Selanjutnya) untuk mengonfirmasi sumber daya yang akan dihentikan atau dipertahankan.
5. Klik **Start Termination** (Mulai Penghentian).

### Membatalkan penghentian terjadwal

1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/).
2. Dalam daftar instans, temukan instans yang diinginkan dan **Scheduled Termination** (Penghentian Terjadwal) yang sesuai di kolom **Instance Billing Plan** (Paket Penagihan Instans). Arahkan kursor Anda ke <img src="https://main.qcloudimg.com/raw/2b612d7419315e76aaa9a7f3a7c9a447.png" style="margin: 0;"></img> untuk menampilkan kotak dialog penghentian terjadwal, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/2a57f29e939d794df1a25f41b0a4880a.png)
3. Klik **Cancel** (Batal). Sebuah kotak dialog ditampilkan meminta Anda untuk mengonfirmasi pembatalan.
4. Di kotak dialog, konfirmasikan informasi instans yang ingin Anda batalkan penghentian waktunya, lalu klik **OK** (OKE). Pembatalan berlaku segera, seperti yang ditunjukkan di bawah ini:
![](https://main.qcloudimg.com/raw/4ee8b052dad3f348f726ba74956d95c5.png)

## Menghentikan Instans Menggunakan Tencent Cloud API

Lihat [TerminateInstances API](https://intl.cloud.tencent.com/document/product/213/33234) untuk informasi selengkapnya.
