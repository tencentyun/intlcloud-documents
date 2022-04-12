### Bagaimana cara menerapkan IP publik jika tidak ditetapkan pada saat membeli CVM?
Jika IP publik tidak ditetapkan saat Anda membeli CVM, maka tidak ada cara untuk menerapkan ulang IP publik biasa untuk CVM ini. Namun, fungsi yang sama dapat dilakukan menggunakan [EIP](https://intl.cloud.tencent.com/document/product/213/5733). Untuk informasi selengkapnya tentang cara menggunakannya, lihat [Menerapkan untuk EIP](https://intl.cloud.tencent.com/document/product/213/16586).
- EIP adalah jenis IP publik yang ditetapkan ke alamat IP publik tertentu di wilayah tertentu. Tidak seperti IP publik biasa, EIP terikat ke akun Anda. Dengan kata lain, Anda dapat mengikat dan melepaskan ikatan EIP dengan CVM yang berbeda sesuai kebutuhan (hanya satu yang dapat diikat dalam sekali waktu).
- Karena sifat khusus dari EIP, jika Anda menerapkan EIP tetapi tidak mengikatnya ke instans, biaya sumber daya IP akan dikenakan. Untuk detail selengkapnya, lihat [Penagihan EIP](https://intl.cloud.tencent.com/document/product/213/17156).

### Bagaimana sebuah instans (CVM atau database) dapat mengakses jaringan publik tanpa alamat IP publik?
Instans tanpa IP publik dapat diterapkan untuk EIP (lihat pertanyaan sebelumnya) atau dapat mengakses jaringan publik melalui gateway NAT.
[Gateway NAT](https://intl.cloud.tencent.com/document/product/1015) dapat menyediakan fitur SNAT dan DNAT untuk instans CVM di VPC. Jika Anda memiliki beberapa instans dan ingin instans tersebut mengakses jaringan publik melalui IP publik yang sama, Anda dapat menggunakan gateway NAT.

Anda bisa mengubah IP publik CVM.
Ya.
- Jika instans CVM Anda menggunakan IP publik yang ditetapkan pada saat pembelian, silakan lihat [Mengubah Alamat IP Publik](https://intl.cloud.tencent.com/document/product/213/16642).
- Jika instans CVM Anda terikat ke EIP, Anda harus [melepas ikatan EIP](https://intl.intl.cloud.tencent.com/document/product/213/16586) terlebih dahulu, lalu [menerapkan untuk EIP lain](https://intl.intl.cloud.tencent.com/document/product/213/16586) atau mengikat EIP yang ada.
> ! Sebaiknya segera lepaskan EIP setelah dikonversi dari IP publik. Jika tidak, EIP yang tidak terikat dengan instans akan dikenakan [biaya sumber daya IP](https://intl.cloud.tencent.com/document/product/213/17156). 

### Apakah IP publik yang sebelumnya digunakan dapat dipulihkan? Apakah EIP tertentu dapat diterapkan?
Anda dapat memulihkan IP publik yang sebelumnya Anda gunakan dan saat ini tidak ditetapkan ke pengguna lain. IP publik yang dipulihkan semuanya adalah EIP. Untuk informasi selengkapnya, lihat [Mendapatkan alamat IP jaringan publik](https://intl.cloud.tencent.com/document/product/213/32719).

### Apakah penambahan kuota dapat dilakukan setelah jumlah EIP mencapai batas atas?
Karena sumber daya EIP terbatas, Anda hanya dapat menerapkan 20 akun per akun per wilayah, dan Anda tidak dapat meminta peningkatan kuota. Instans CVM tanpa IP publik dapat menggunakan gateway NAT dan metode lain untuk mengakses jaringan publik.

### Bagaimana cara CVM mengakses jaringan publik jika memiliki IP publik atau EIP dan subnetnya juga dikaitkan dengan gateway NAT?

Jika CVM memiliki IP atau EIP publik dan subnetnya juga dikaitkan dengan gateway NAT (artinya tabel rute menentukan bahwa hop selanjutnya untuk lalu lintas subnet ini untuk mengakses jaringan publik adalah gateway NAT), maka pengaturan default adalah untuk semua lalu lintas CVM ini guna mengakses jaringan publik melalui gateway NAT.

Jika Anda perlu mengubah prioritas agar lalu lintas dari instans CVM ke jaringan publik melewati IP publik, lihat [Menyesuaikan Prioritas Gateway NAT dan EIP](https://intl.cloud.tencent.com/document/product/1015/32734).

### Ketika instans CVM mengakses jaringan publik melalui gateway publik atau gateway NAT, apakah biaya jaringan akan dikenakan dua kali?

Tidak, biaya jaringan hanya akan dikenakan satu kali. Saat mengakses jaringan publik melalui gateway publik atau gateway NAT, hanya biaya jaringan gateway publik yang sesuai atau biaya jaringan gateway NAT yang akan dikenakan. 

