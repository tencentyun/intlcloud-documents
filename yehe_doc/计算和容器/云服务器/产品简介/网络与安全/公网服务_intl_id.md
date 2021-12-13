Untuk meng-host layanan publik pada instans CVM Anda, yang melibatkan transmisi data melalui Internet, Anda memerlukan alamat IP publik. Tencent Cloud menyediakan akses Internet melalui jaringan terhubung berkecepatan tinggi dari Tencent Cloud IDC. Jaringan BGP multi-jalur domestik mencakup lebih dari 20 operator jaringan dan jalur keluar jaringan publik dapat menerapkan peralihan lintas wilayah dalam hitungan detik. Hal ini memastikan pengguna Anda dapat menikmati jaringan berkecepatan tinggi dan aman, apa pun jaringan yang mereka gunakan.

## Alamat IP publik
 - **Ikhtisar**: alamat IP publik adalah alamat non-cadangan di Internet. CVM dengan alamat IP publik dapat mengakses komputer lain di Internet dan diakses oleh komputer lain.
 - **Mendapatkan alamat IP publik**: atur bandwidth Anda ke lebih dari 0 Mbps saat membuat instans CVM. Sistem secara otomatis memilih alamat IP publik dari kumpulan alamat IP publik dan menetapkannya ke instans Anda. Alamat ini nantinya dapat diubah. Untuk mengetahui detailnya, lihat [Mengubah IP Publik Instans](https://intl.cloud.tencent.com/document/product/213/16642).
 - **Mengonfigurasi instans CVM Anda**: Anda dapat login ke instans CVM Anda dari jaringan publik untuk mengonfigurasinya. Untuk informasi selengkapnya, lihat [Login ke Instans Linux](https://intl.cloud.tencent.com/document/product/213/5436) dan [Login ke Instans Windows](https://intl.cloud.tencent.com/document/product/213/5435). 
 - **Menerjemahkan alamat IP publik**: Anda dapat memetakan alamat IP publik Anda ke [alamat IP pribadi](https://intl.cloud.tencent.com/document/product/213/5225) instans CVM Anda menggunakan Terjemahan Alamat Jaringan (NAT). 
 - **Mengambil informasi alamat IP publik**: semua antarmuka jaringan publik Tencent Cloud dikelola oleh Tencent Gateway (TGW), artinya semua antarmuka jaringan publik dari semua instans CVM dikelola oleh TGW. Proses ini tidak terlihat oleh instans CVM. Oleh karena itu, ketika Anda menjalankan perintah `ifconfig` pada instans CVM Linux atau `ipconfig` pada instans CVM Windows, Anda akan mendapatkan informasi [alamat IP pribadi](https://intl.cloud.tencent.com/document/product/213/5225). Untuk informasi mengenai alamat IP publik Anda, login ke [konsol CVM](https://console.cloud.tencent.com/cvm) Anda dan periksa halaman detail instans.
 - **Penagihan**: menggunakan alamat IP publik untuk menawarkan layanan dapat dikenakan biaya. Untuk mengetahui detailnya, lihat [Metode Penagihan Jaringan Publik](https://intl.cloud.tencent.com/document/product/213/10578).

## Rilis Alamat IP Publik
Anda tidak dapat secara aktif mengaitkan atau melepaskan alamat IP publik yang telah dikaitkan dengan instans.
Dalam kasus berikut, alamat IP publik yang terkait dengan instans dilepaskan atau ditetapkan ulang:
- **Saat Anda menghentikan instans**. Tencent Cloud akan merilis alamat IP publik saat Anda menghentikan instans CVM sesuai permintaan.
- Saat Anda mengaitkan atau memutuskan pengaitan [IP Publik Elastis](https://intl.cloud.tencent.com/document/product/213/5733) dengan sebuah instans. Saat mengaitkan EIP dengan instans Anda, alamat IP publik yang sudah ada akan dilepaskan kembali ke dalam kumpulan IP publik. Saat memutuskan pengaitan EIP dari instans Anda, Tencent Cloud akan memberikan alamat IP publik baru ke instans Anda. Anda tidak akan dapat menggunakan alamat IP publik lama Anda.

Jika Anda memerlukan alamat IP publik statis, gunakan [IP Publik Elastis (EIP)](https://intl.cloud.tencent.com/document/product/213/5733).

## Panduan Operasi
Untuk mengetahui petunjuk mendetail tentang cara mendapatkan dan mengubah alamat IP publik Anda, lihat:
- [Mendapatkan Alamat IP Publik Instans](https://intl.cloud.tencent.com/document/product/213/17940)
- [Mengubah Alamat IP Publik](https://intl.cloud.tencent.com/document/product/213/16642)
