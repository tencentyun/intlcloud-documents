Instans Virtual Private Cloud (VPC) Tencent Cloud adalah ruang jaringan yang terisolasi secara logis yang ditentukan pengguna di Tencent Cloud. Dalam hal ini, pengguna dapat menyesuaikan rentang IP, alamat IP, dan kebijakan perutean. Oleh karena itu, Tencent Cloud menyarankan Anda menggunakan instans VPC untuk bisnis Anda.

Untuk membantu Anda menggunakan instans VPC Tencent Cloud dengan lebih baik, Tencent Cloud memberikan rekomendasi perencanaan jaringan berikut.

### Menentukan jumlah instans VPC

- Fitur:
	- Instans VPC bersifat spesifik wilayah. Secara default, CVM di wilayah yang berbeda tidak dapat berkomunikasi satu sama lain. Jika komunikasi lintas wilayah diperlukan, buat [koneksi peering](https://intl.cloud.tencent.com/document/product/553).
	- Secara default, instans VPC yang berbeda di wilayah yang sama tidak dapat saling berkomunikasi. Jika komunikasi lintas-VPC diperlukan, buat [koneksi peering](https://intl.cloud.tencent.com/document/product/553).
	- Secara default, zona ketersediaan yang berbeda dalam instans VPC yang sama dapat saling berkomunikasi.
- Rekomendasi:
	- Jika bisnis Anda memerlukan deployment sistem lintas wilayah, beberapa instans VPC diperlukan. Dalam kasus ini, Anda dapat membuat instans VPC yang dekat dengan wilayah tempat pelanggan Anda berada guna mengurangi latensi akses dan meningkatkan kecepatan akses.
	- Jika Anda telah mend-deploy beberapa bisnis di wilayah saat ini dan ingin menerapkan isolasi jaringan di antara bisnis yang berbeda, Anda dapat membuat instans VPC untuk setiap bisnis di wilayah saat ini.
	- Jika Anda tidak memerlukan deployment bisnis lintas wilayah atau isolasi jaringan di antara bisnis, Anda dapat menggunakan satu instans VPC.

### Menentukan pembagian subnet
- Fitur:
	- Subnet adalah blok alamat IP dalam instans VPC. Semua sumber daya cloud dalam instans VPC harus di-deploy di subnet.
	- Dalam instans VPC yang sama, rentang IP subnet tidak boleh tumpang tindih.
	- Tencent Cloud secara otomatis menetapkan alamat IP pribadi awal dari rentang IP VPC. Blok CIDR Tencent Cloud VPC dapat berupa salah satu dari rentang IP VPC berikut. Untuk alamat IP dalam rentang ini, nilai mask-nya berkisar dari 16 hingga 28, dan mask sebenarnya ditentukan oleh jaringan pribadi tempat instans tersebut berada.
	 - **10.0**.0.0-**10.255**.255.255
	 - **172.16**.0.0-**172.31**.255.255
	 - **192.168**.0.0-**192.168**.255.255
	- Setelah instans VPC dibuat, rentang IP-nya tidak dapat diubah.
- Rekomendasi:
	- Jika hanya subnet VPC yang perlu dibagi dan komunikasi dengan jaringan dasar atau IDC tidak terlibat, pilih salah satu rentang IP sebelumnya untuk membuat subnet.
	- Jika komunikasi dengan jaringan dasar diperlukan, buat instans VPC dengan rentang IP 10.[0-47].0.0/16 beserta subsetnya sesuai kebutuhan.
	- Jika VPN diperlukan, rentang IP lokal (dari instans VPC) dan rentang pasangan IP (dari IDC Anda) tidak boleh tumpang tindih. Oleh karena itu, jangan gunakan rentang pasangan IP saat membuat subnet.
	- Selama pembagian subnet, Anda juga perlu mempertimbangkan jumlah alamat IP yang tersedia dalam rentang IP.
	- Sebaiknya subnet dibagi berdasarkan modul bisnis untuk bisnis dalam instans VPC yang sama. Misalnya, subnet A digunakan untuk lapisan web, subnet B digunakan untuk lapisan logika, dan subnet C digunakan untuk lapisan database. Ini memfasilitasi kontrol akses dan pemfilteran dengan menggunakan jaringan ACL.

### Menentukan kebijakan rute

- Fitur:
	- Tabel rute terdiri dari serangkaian aturan perutean yang mengontrol arus lalu lintas subnet dalam instans VPC.
	- Setiap subnet harus dikaitkan dengan hanya satu tabel rute.
	- Sebuah tabel rute tunggal dapat dikaitkan dengan beberapa subnet.
	- Saat instans VPC dibuat, sistem secara otomatis membuat tabel rute default untuk instans, yang menentukan bahwa instans VPC dapat saling berkomunikasi melalui jaringan pribadi.
- Rekomendasi:
	- Jika Anda tidak perlu mengontrol arus lalu lintas subnet dan instans VPC saling terhubung melalui jaringan pribadi secara default, Anda dapat menggunakan tabel rute default tanpa perlu mengonfigurasi kebijakan perutean khusus.
	- Jika Anda perlu mengontrol arus lalu lintas subnet, lihat [Ikhtisar](https://intl.cloud.tencent.com/document/product/215/31810) di situs web resmi.


Untuk informasi selengkapnya tentang instans VPC, lihat [VPC](https://intl.cloud.tencent.com/document/product/215).



