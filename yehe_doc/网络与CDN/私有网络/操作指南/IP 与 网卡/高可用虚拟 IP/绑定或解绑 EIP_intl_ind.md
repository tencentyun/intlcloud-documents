Mirip dengan IP pribadi, pengikatan HAVIP juga dapat dikonfigurasi di konsol. Pengikatan HAVIP mengacu pada operasi EIP. Anda dapat melewati bagian ini jika tidak diperlukan koneksi jaringan publik.

## Pengikatan EIP
1. Login ke [konsol VPC](https://console.cloud.tencent.com/vpc/) dan pilih **IP and Interface** (IP dan Antarmuka) > **HAVIP** di bilah sisi kiri. 
2. Pilih wilayah target pada halaman pengelolaan HAVIP.
3. Pilih HAVIP yang akan diikat ke EIP, dan klik **Bind** (Ikatkan) di kolom **Operation** (Operasi).
4. Pada kotak dialog pop-up, pilih EIP yang akan diikatkan.
    >!
    >> + Satu HAVIP hanya dapat diikatkan ke satu EIP. Jika tidak ada EIP yang tersedia, Anda harus terlebih dahulu membuat EIP di konsol.
    >+ Jika HAVIP tidak dibatasi dengan instans CVM, EIP terkait akan berstatus tidak aktif dan akan dikenakan biaya waktu jeda. Harap konfigurasi HAVIP dengan benar dan ikat ke instans dengan mengacu pada kasus berikut: 
    > + [Membangun Kluster Utama/Sekunder Ketersediaan Tinggi dengan Menggunakan HAVIP + Keepalived](https://intl.cloud.tencent.com/document/product/215/31877) di Praktik Terbaik
    > + [Membuat Database Ketersediaan Tinggi dengan Menggunakan HAVIP + Windows Server Failover Cluster](https://intl.cloud.tencent.com/document/product/215/31878) di Praktik Terbaik 
5. Klik **OK** (OKE).

## Memutuskan Ikatan EIP
1. Login ke [konsol VPC](https://console.cloud.tencent.com/vpc/) dan pilih **IP and Interface** (IP dan Antarmuka) > **HAVIP** di bilah sisi kiri. 
2. Pilih wilayah target pada halaman pengelolaan HAVIP.
3. Pilih HAVIP dari tempat ikatan EIP akan dilepas, dan klik **Unbind** (Memutuskan Ikatan) di kolom **Operation** (Operasi).
4. Pada jendela pop-up, baca catatan, dan klik **OK** (OKE) untuk memutuskan ikatan EIP.
   >!
   >> Bisnis jaringan publik Anda mungkin terpengaruh setelah memutuskan ikatan EIP. Harap bersiap sejak awal.
   >> Setelah ikatan diputuskan, EIP akan menjeda dan membebankan biaya waktu jeda. Anda dapat langsung merilis EIP yang tidak digunakan untuk menghindari biaya.
   >
