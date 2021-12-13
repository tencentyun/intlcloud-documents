TencentOS Server (juga dikenal sebagai Tencent Linux, TS, atau Tlinux) adalah sistem operasi Linux Tencent yang dirancang untuk skenario cloud. Dengan fitur khusus dan performa yang dioptimalkan, TencentOS Server menyediakan lingkungan operasi berperforma tinggi, aman, dan andal untuk aplikasi di instans Cloud Virtual Machine (CVM). TencentOS Server tidak dikenai biaya alias gratis, dan aplikasi yang dikembangkan di CentOS dan distribusi lainnya bisa langsung dijalankan di TencentOS Server. Selain itu, Tencent Cloud selalu memberi Anda pembaruan, pemeliharaan, dan dukungan teknis.

## Kasus Penggunaan

TencentOS Server bisa digunakan dalam skenario berikut:

- TencentOS Server cocok untuk instans dari sebagian besar tipe CVM.
- Saat meluncurkan instans, TencentOS Server digunakan untuk mentransfer operasi terkait ke cloud-init melalui data pengguna (bidang data pengguna) untuk mendukung konfigurasi dinamis.

## TencentOS Server 2.4 Pendahuluan

### Lingkungan mode pengguna

Paket perangkat lunak mode pengguna kompatibel dengan CentOS 7 terbaru, yang bisa digunakan langsung di TencentOS Server 2.4.

### Layanan sistem dan konfigurasi pengoptimalan

#### Layanan sistem

- `tlinux-irqaffinity`: layanan afinitas IRQ di TencentOS Server.
- `tlinux-bootlocal`: layanan bootlocal di TencentOS Server. Ini akan dimulakan setelah eksekusi otomatis skrip `/etc/rc.d/boot.local` saat startup.

#### Alat sistem

`tencent-tools`: perintah tos (t) yang digunakan untuk manajemen sistem. Parameter yang didukung adalah sebagai berikut:

```bash
tos versi 2.2
Penggunaan:
	tos TencentOS Server System Management Toolset
	tos -u|-U| update [rpm_name]Memperbarui sistem 
	tos -i|-I| install rpm_name	menginstal rpms
	tos -s|-S| showMenampilkan versi sistem
	tos -c|-C| check [rpm_name]Memeriksa rpms yang dimodifikasi
	tos -f yum | fix yumMemperbaiki masalah yum
	tos -f dns | fix dnsMemperbaiki masalah DNS
	tos -a|-A | analyzeMenganalisis performa sistem 
	tos set dns			Mengatur DNS
	tos set irqSet irqaffinity, memulai ulang layanan irqaffinity
	tos -cu| check-updateMemeriksa pembaruan paket yang tersedia
	tos -b|-B| backup [ reboot ]Mencadangkan sistem secara online, atau me-reboot untuk mencadangkan 
	tos -r|-R| recover|reinstallMemulihkan atau Menginstal ulang sistem
	tos -h|-H| helpMenampilkan penggunaan ini
	tos -v|-V| versionMenampilkan versi skrip
```

#### Konfigurasi sistem

- **pam**: menetapkan kebijakan kata sandi yang kuat.
- **memodifikasi `/etc/bashrc`**: mengoptimalkan tampilan bash.
- **`/etc/hosts`**: menambahkan TENCENT64 dan TENCENT64.site.
- **`/root/.bashrc`**: mengoptimalkan konfigurasi.

#### Kernel TencentOS Server 2.4

TencentOS Server 2.4 menggunakan kernel 4.14 jangka panjang dari komunitas kernel. Untuk informasi selengkapnya, lihat [TencentOS-kernel](https://github.com/Tencent/TencentOS-kernel).


## Mendapatkan TencentOS Server

Anda bisa mendapatkan dan menggunakan TencentOS Server menggunakan metode berikut ini:

- Saat membuat instans CVM, pilih **Public Image** dan versi TencentOS Server yang sesuai.
  Untuk informasi selengkapnya, lihat [Membuat Instans melalui Halaman Pembelian CVM](https://intl.cloud.tencent.com/document/product/213/4855).
- Untuk instans CVM yang sudah ada, Anda perlu menginstal ulang sistem operasi ke TencentOS Server.
  Untuk informasi selengkapnya, lihat [Menginstal Ulang Sistem](https://intl.cloud.tencent.com/document/product/213/4933).

## Catatan Rilis

| Waktu Rilis      | Tag Gambar                                                    | Deskripsi                                                  |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 17 September 2019 | TencentOS Server 2.4, sebelumnya dikenal sebagai Tencent linux rilis 2.4 (Final) | ID Gambar: img-hdt9xxkt<br>Versi kernel: 4.14.105<br>Wilayah: semua wilayah |


## Dukungan Teknis

Tencent Cloud menyediakan dukungan teknis berikut untuk TencentOS Server:

- Tencent Cloud menyediakan pembaruan keamanan di repositori YUM. Anda bisa menjalankan perintah `yum update` untuk memperbarui TencentOS Server ke versi terbaru.
- TencentOS Server adalah citra sistem operasi yang dirancang untuk skenario cloud. Ini didasarkan pada kernel versi 4.14.105, yang telah lama didukung oleh komunitas kernel. Jika perlu, Tencent Cloud akan memberikan bantuan teknis untuk membantu Anda memecahkan masalah yang Anda hadapi saat menggunakan TencentOS Server.
