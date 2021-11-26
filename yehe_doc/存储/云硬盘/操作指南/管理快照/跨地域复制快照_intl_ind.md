Replikasi snapshot lintas wilayah saat ini dalam versi beta.Dengan fitur ini, Anda dapat dengan mudah memigrasikan data dan layanan ke wilayah lain, atau membangun sistem pemulihan bencana lintas wilayah untuk bisnis Anda.
Anda dapat **mengirim pengajuan** untuk menggunakan fitur ini.

## Batas Penggunaan
- **Apply for Beta** (Pengajuan Permintaan Beta): replikasi snapshot lintas wilayah saat ini dalam versi beta.Anda perlu **mengirim pengajuan** untuk mengajukan permintaan atas fitur ini.
- **Wilayah yang didukung**: untuk informasi selengkapnya, lihat [Wilayah dan Zona Ketersediaan](https://intl.cloud.tencent.com/document/product/362/32396)。


## Petunjuk

1.Masuk ke halaman [Daftar Snapshot](https://console.cloud.tencent.com/cvm/snapshot).
2.Klik **Cross-Region Replication** (Replikasi Lintas Wilayah) untuk snapshot target.
3.Konfigurasikan parameter berikut:
- **New snapshot name** (Nama snapshot baru): (opsional) masukkan nama snapshot baru hingga 60 karakter.
Secara default, nama snapshot baru berisi ID snapshot sumber dan informasi wilayah dan dalam format berikut:`Copied <ID snapshot sumber> from <Wilayah snapshot sumber>`, misalnya, `Copied snap-oi5spwt2 from ap-shanghai`.
- **Region** (Wilayah): (wajib) wilayah target tempat snapshot disalin
Silakan periksa kuota snapshot dan batasan geografis saat Anda memilih wilayah.
4.Klik **OK** untuk memulai replikasi.Arahkan kursor ke ikon informasi untuk melihat status snapshot sumber.Snapshot baru ditambahkan ke wilayah target.
5.Setelah replikasi selesai, Anda dapat melihat snapshot baru di daftar snapshot dari wilayah target.
> Snapshot sumber tidak dapat dihapus selama replikasi lintas wilayah snapshot ini.
>
Selama proses replikasi lintas wilayah:
- Status snapshot sumber: Anda dapat melihatnya dengan membuka **snapshot list** (daftar snapshot) wilayah sumber dan mencari di kolom status pada baris snapshot sumber.
- Status snapshot target: Anda dapat melihatnya dengan membuka halaman daftar snapshot dari wilayah target.
