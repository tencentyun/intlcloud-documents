## Ikhtisar

### Langkah-Langkah Umum

**Cross-region replication** (Replikasi lintas-wilayah) dapat membantu pengguna men-deploy CVM yang sama **across regions** (di seluruh wilayah) dengan cepat. Anda dapat menggunakan fitur ini untuk menyalin citra di seluruh wilayah, lalu membuat CVM dengan menyalin citra di bawah wilayah baru.

### Catatan
 - Citra yang disalin harus berupa citra kustom. Anda harus membuat citra kustom terlebih dahulu. Untuk detailnya, lihat [Membuat Citra Kustom](https://intl.cloud.tencent.com/document/product/213/4942).
 - Replikasi lintas wilayah memungkinkan Anda menyalin citra di dalam atau di luar Tiongkok. Jika Anda perlu menyalin citra dari Tiongkok ke negara lain atau sebaliknya, harap hubungi layanan purna jual.
 - Replikasi citra lintas wilayah saat ini gratis.
 - Replikasi lintas wilayah saat ini tidak mendukung citra kustom yang lebih besar dari 50 GB.
 - Replikasi lintas wilayah memerlukan waktu 10 hingga 30 menit.
 
## Metode
<dx-tabs>
::: Copy\simages\svia\sconsole
 1. Login ke [Konsol CVM](https://console.cloud.tencent.com/cvm/).
 2. Di bilah sisi kiri, klik **[Images](https://console.cloud.tencent.com/cvm/image)** ([Citra]) untuk masuk ke halaman pengelolaan citra.
 3. Pilih wilayah tempat citra asli berada yang ingin Anda salin, dan klik tab **Custom Image** (Citra Kustom), seperti yang ditunjukkan di bawah ini:
 Misalnya, pilih wilayah Guangzhou.
 ![](https://main.qcloudimg.com/raw/f845cfeef21663bf8aaff58d5145f08c.png)
 4. Temukan instans yang citranya perlu disalin, klik **More** (Lainnya) > **Cross-region replication** (Replikasi lintas wilayah).
<dx-alert infotype="explain"> Untuk operasi batch, pilih semua citra yang ingin Anda salin, lalu klik **Cross-region replication** (Replikasi lintas wilayah).
 </dx-alert>
 5. Di jendela pop-up "Cross-region copying" (Penyalinan lintas wilayah), pilih wilayah tempat citra akan disalin dan klik **OK** (OKE).
Setelah penyalinan selesai, daftar citra di wilayah tujuan akan menampilkan citra dengan nama yang sama dan ID yang berbeda.
 6. Beralih ke wilayah tujuan. Pilih citra yang berhasil disalin dalam daftar citra di bawah wilayah, lalu klik **Create Instance** (Buat Instans) untuk membuat instans CVM yang sama.
:::
::: Copy\simages\svia\sAPI
Anda juga dapat menggunakan SyncCvmImage API untuk menyalin citra. 
:::
</dx-tabs>
