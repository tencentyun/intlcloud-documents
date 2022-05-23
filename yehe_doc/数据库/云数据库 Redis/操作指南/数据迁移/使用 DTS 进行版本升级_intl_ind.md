
## Ikhtisar
Instans Edisi Memori 4.0 dan 5.0 TencentDB for Redis dalam [arsitektur standar](https://intl.cloud.tencent.com/document/product/239/31959) atau [arsitektur kluster](https://intl.cloud.tencent.com/document/product/239/18336) menampilkan konfigurasi spesifikasi yang lebih fleksibel, kinerja yang lebih tinggi, dan fungsionalitas yang lebih baik. Jika Anda menggunakan versi Redis yang lebih lama, kami menyarankan Anda meningkatkan ke Redis 4.0 atau 5.0 untuk pengalaman layanan TencentDB yang lebih baik.

Versi instans TencentDB for Redis sekarang dapat ditingkatkan melalui Layanan Transmisi Data (DTS) dengan hot migration, yang menjamin kontinuitas layanan instans selama proses peningkatan dan dapat memperbarui data tambahan secara real-time.

| Jangka Waktu | Deskripsi | 
|---------|---------|
| Instans sumber | Instans sumber untuk peningkatan versi | 
| Instans target | Instans target untuk peningkatan versi | 

#### Versi yang didukung
<table>
    <tr>
    <td rowspan=2 align=center>Versi Instans Sumber</td>
    <td colspan=4 align=center>Versi Instans Target</td>
    </tr>
    <tr>
    <td>Edisi Memori 4.0 (arsitektur standar)</td>
		<td>Edisi Memori 4.0 (arsitektur kluster)</td>
		<td>Edisi Memori 5.0 (arsitektur standar)</td>
		<td>Edisi Memori 5.0 (arsitektur kluster)</td>
    </tr>
    <tr>
    <td>Edisi Memori 2.8 (arsitektur standar)</td>
    <td>✓</td>
    <td>✓</td>
		<td>✓</td>
    <td>✓</td>
    </tr>
    <tr>
    <td>Edisi Memori 4.0 (arsitektur standar)</td>
    <td>N/A</td>
    <td>✓</td>
	  <td>✓</td>
		<td>✓</td>
    </tr>
		<tr>
    <td>Edisi Memori 4.0 (arsitektur kluster)</td>
    <td>N/A</td>
		<td>N/A</td>
    <td>✓</td>
		<td>✓</td>
    </tr>
		<tr>
    <td>Edisi Memori 5.0 (arsitektur standar)</td>
    <td>N/A</td>
		<td>N/A</td>
		<td>N/A</td>
    <td>✓</td>
    </tr>
</table>


## Prasyarat
- Instans TencentDB for Redis sumber harus berjalan dengan benar.
- Anda telah membeli instans Edisi Memori 4.0 atau 5.0 TencentDB for Redis  dalam arsitektur standar atau arsitektur kluster.
>?Jika data Anda saat ini kurang dari 12 GB dengan data tambahan tidak lebih dari 60 GB dan QPS tidak lebih dari 40.000, atau bisnis Anda memerlukan dukungan transaksional, disarankan Edisi Memori 4.0 atau 5.0 TencentDBfor Redis  (arsitektur standar); jika tidak, Edisi Memori 4.0 atau 5.0 TencentDB for Redis (arsitektur kluster) adalah pilihan terbaik Anda.

## Petunjuk
1. Gunakan DTS untuk memigrasikan data dari instans sumber TencentDB for Redis ke instans Edisi Memori 4.0 atau 5.0 Redis dalam arsitektur standar atau arsitektur kluster. Untuk informasi selengkapnya, lihat [Migrasi dengan DTS](https://intl.cloud.tencent.com/document/product/239/31941).
2. Setelah sinkronisasi data selesai dan data diverifikasi oleh bisnis Anda, Anda dapat memilih waktu untuk memutuskan hubungan instans Redis sumber berdasarkan metrik seperti QPS bisnis dan menghubungkan ke instans Redis tujuan. Ada dua metode beralih:
**Login ke konsol untuk beralih:**
 1) Catat alamat IP lama dari instans Redis sumber dan ubah.
 2) Ubah informasi jaringan instans Redis target ke subnet VPC instans Redis sumber, dan ubah alamat IP instans target ke alamat IP lama instans sumber untuk menyelesaikan peralihan di sisi bisnis. Untuk informasi selengkapnya tentang cara mengubah informasi jaringan dan alamat IP, lihat [Mengonfigurasi Jaringan](https://intl.cloud.tencent.com/document/product/239/31944).
**Login ke instans untuk beralih:** perbarui IP instans Redis sumber dalam kode ke IP instans Redis target.
