Untuk instans TencentDB for Redis multi-AZ yang di-deploy dalam arsitektur standar/klaster, Anda dapat mempromosikan node replika/grup node ke node master/grup node secara manual. Anda dapat men-deploy node master dalam grup AZ/node tertentu.

## Promosi dalam Arsitektur Standar

Instans multi-AZ yang di-deploy dalam arsitektur standar hanya dapat memiliki satu node master. Anda dapat mempromosikan node replika menjadi node master, dan node master lama akan secara otomatis didemosi ke node replika secara bersamaan.

Proses promosinya adalah sebagai berikut

1. Promosikan node replika menjadi node master. (Jika node sudah menjadi node master, lewati langkah ini.)
2. Promosikan AZ menjadi AZ master.

## Petunjuk

1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans dalam daftar instans, dan masuk ke halaman manajemen instans.
2. Pada halaman **Node Management** (Manajemen Node), klik **Promote to Master Node/AZ** (Promosikan ke Node/AZ Master) di daftar node.
   ![](https://main.qcloudimg.com/raw/0ae356733962b9bde8a3b415a5ad9b8c.png)
3. Di kotak dialog pop-up, konfirmasikan bahwa semuanya sudah benar dan klik **OK** (OKE).
   ![](https://main.qcloudimg.com/raw/7519780d59c9ac4ced2f201499c599a8.png)

## Promosi dalam Arsitektur Klaster

Sebuah instans dalam arsitektur klaster memiliki beberapa replika per shard. Node master berada di grup node master, sedangkan node replika berada di grup node replika. Setiap grup memiliki nama. Ini membuat manajemen node menjadi lebih mudah.

Untuk instans multi-AZ yang di-deploy dalam arsitektur klaster, Anda dapat mempromosikan grup node replika menjadi grup node master. Jika node master dari beberapa shard dialihkan dari grup node ke yang lain, Anda dapat mempromosikan grup node tersebut sehingga semua nodenya akan menjadi node master.

Proses promosinya adalah sebagai berikut

1. Promosikan semua node dalam grup node menjadi node master. (Jika semua node sudah menjadi master node, lewati langkah ini.)
2. Promosikan grup node menjadi grup node master. Jika kegagalan tingkat server terjadi setelah promosi selesai, beberapa node dalam grup node akan didemosi ke node replika dan dipromosikan kembali menjadi node master.
3. Promosikan AZ menjadi AZ master.

### Cara kerjanya

- TencentDB for Redis dalam arsitektur standar/klaster menjalankan perintah `cluster failover` untuk mempromosikan node replika/grup node menjadi node master/grup node.
- Mempromosikan node akan memicu peralihan master-replika. Selama peralihan, akses database akan terpengaruh selama beberapa detik hingga 3 menit, dan perintah pemblokiran (termasuk BLPOP, BRPOP, BRPOPLPUSH, dan SUBSCRIBE) dapat mengalami kegagalan satu kali atau lebih sebelum dapat dijalankan dengan sukses.
- Jika promosi gagal, Anda dapat mencoba lagi.
- Setelah mempromosikan node replika menjadi  node master, akses Anda mungkin dirutekan ke beberapa AZ, sehingga meningkatkan latensi respons layanan dan menurunkan [QPS](https://intl.cloud.tencent.com/document/product/239/31950#qps.2F.E5.B9.B6.E5.8F.91).

## Petunjuk

1. Login ke [konsol TencentDB for Redis](https://console.cloud.tencent.com/redis), klik ID instans dalam daftar instans, dan masuk ke halaman manajemen instans.
2. Pada halaman **Node Management** (Manajemen Node), klik **Promote to Master Node Group** (Promosikan ke Grup Node Master) di daftar node.
3. Di kotak dialog pop-up, konfirmasikan bahwa semuanya sudah benar dan klik **OK** (OKE).
   ![](https://main.qcloudimg.com/raw/7519780d59c9ac4ced2f201499c599a8.png)
