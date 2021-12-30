[Aturan ACL](https://intl.cloud.tencent.com/document/product/215/31850) adalah lapisan keamanan opsional yang beroperasi pada tingkat subnet. Ini digunakan untuk mengontrol aliran data masuk dan keluar dari subnet, yang akurat untuk protokol dan granularitas port, untuk mencapai kontrol lalu lintas subnet yang baik. Anda dapat menghubungkan ACL jaringan yang sama ke subnet yang memerlukan tingkat kontrol lalu lintas jaringan yang sama.
Bagian ini menjelaskan cara mengikat, melepaskan, dan mengubah aturan ACL melalui konsol VPC.

## Petunjuk
1. Login ke [Konsol VPC](https://console.cloud.tencent.com/vpc).
2. Pilih **Subnet** (Subnet) di bilah sisi kiri untuk membuka halaman pengelolaan subnet.
3. Klik ID subnet untuk membuka halaman detailnya. Anda dapat melakukan pengikatan, pelepasan, atau perubahan ACL di halaman berikut.
    + Di kolom **Associate ACL** (Hubungkan ACL) di bawah tab **Basic Information** (Informasi Dasar)
    + Di bawah tab **ACL Rules** (Aturan ACL)
4. Lakukan operasi berikut berdasarkan kebutuhan bisnis. Tangkapan layar berikut mengambil operasi di **ACL Rules** (Aturan ACL) sebagai contoh.
  + Jika subnet saat ini tidak terikat dengan aturan ACL, Anda dapat mengeklik **Bind** (Ikat) untuk memilih aturan ACL yang sesuai, dan klik **OK** (Oke) untuk menyelesaikan pengikatan. Pengikatan akan langsung berlaku. Saat ini, hanya lalu lintas masuk dan keluar dari subnet yang aturannya **Allow** (Izinkan) yang dapat melewatinya.
 + Jika aturan ACL yang terikat ke subnet saat ini tidak memenuhi persyaratan aliran jaringan, Anda dapat mengeklik **Change** (Ubah) untuk mengubah aturan ACL, yang akan langsung berlaku.
 + Jika subnet saat ini terikat dengan aturan ACL, tetapi Anda tidak perlu lagi mengontrol lalu lintas masuk dan keluar subnet, Anda dapat mengeklik **Unbind** (Putuskan Ikatan) untuk memutuskan ikatan aturan ACL. Pemutusan ikatan akan langsung berlaku dan ini akan menyebabkan pencabutan pembatasan aturan ACL pada lalu lintas masuk dan keluar subnet.
    	 
