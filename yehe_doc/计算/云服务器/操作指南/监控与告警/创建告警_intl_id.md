## Ikhtisar
Anda dapat mengatur alarm ambang batas untuk memantau performa CVM, serta alarm peristiwa untuk melihat status instans CVM dan infrastruktur platform yang mendasarinya. Ketika terjadi pengecualian, Anda akan segera menerima notifikasi melalui , email, SMS, telepon, dll. Kebijakan alarm yang tepat akan membantu meningkatkan ketahanan dan keandalan aplikasi Anda. Dokumen ini menjelaskan cara membuat kebijakan alarm. Untuk informasi selengkapnya, lihat [Membuat Kebijakan Alarm](https://intl.cloud.tencent.com/document/product/248/38916).

## Petunjuk
1. Login ke [Konsol Cloud Monitor], lalu pilih **Alarm Configuration** (Konfigurasi Alarm) > [**Alarm Policy** (Kebijakan Alarm)](https://console.cloud.tencent.com/monitor/alarm2/policy) di bilah sisi kiri.
2. Di halaman **Alarm Policy** (Kebijakan Alarm), klik **Create** (Buat).
3. Di jendela pop-up, konfigurasikan informasi dasar, kebijakan alarm, dan templat notifikasi seperti yang diinstruksikan di bawah ini.
<table>
  <tr>
    <th>Jenis Konfigurasi</th>
    <th width="19%" colspan=2>Item Konfigurasi</th>
    <th>Deskripsi</th>
  </tr>
  <tr>
    <td  rowspan="5"> Info Dasar</td>
    <td colspan=2>Nama Kebijakan</td>
    <td>Nama kebijakan kustom</td>
  </tr>
  <tr>
    <td colspan=2>Keterangan</td>
    <td>Keterangan untuk kebijakan</td>
  </tr>
  <tr>
    <td colspan=2>Jenis Pemantauan</td>
    <td>Pilih <b>Cloud Product Monitoring</b></td>
  </tr>
  <tr>
    <td colspan=2>Jenis Kebijakan</td>
    <td>Pilih jenis kebijakan yang diinginkan untuk memantau layanan Tencent Cloud.</td>
  </tr>
  <tr>
    <td colspan=2>Proyek</td>
    <td>Pilih proyek sesuai kebutuhan. Anda nanti dapat menemukan kebijakan ini dengan cepat dengan memfilter berdasarkan proyek.
  </tr>
  <tr>
    <td rowspan="4">Konfigurasikan Kebijakan Alarm</td>
    <td colspan=2>Objek Alarm</td>
    <td>
      <ul>
			         <li><b>ID Instans</b>: mengaitkan kebijakan dengan instans CVM yang ditentukan</li>
           <li><b>Tag</b>: mengaitkan kebijakan dengan instans CVM dengan tag yang ditentukan</li>
               <li><b>Grup Instans</b>: mengaitkan kebijakan dengan grup instans yang dipilih</li>
		            <li><b>Semua Objek</b>:  mengaitkan kebijakan dengan semua instans akun saat ini (diperlukan izin)</li>
           </ul>
        </td>
		<tr>
		<td rowspan=3>Kondisi Pemicu</td>
    <td><b>Konfigurasi Manual</b>(Alarm Metrik)</td>
    <td>
Kondisi pemicu: tentukan metrik, perbandingan, ambang batas, periode statistik, dan jumlah periode berturut-turut. Anda dapat memperluas kondisi pemicu untuk melihat tren metrik, dan berdasarkan pemicu yang menetapkan ambang batas yang tepat.
  <tr>
    <td><b>Konfigurasi Manual</b>(Alarm Peristiwa)</td>
    <td>Buat kebijakan alarm peristiwa untuk mendapatkan notifikasi jika ada sumber daya layanan atau pengecualian infrastruktur yang mendasarinya</td>
  </tr>
  <tr>
    <td>Pilih templat</td>
    <td>Pilih templat yang dikonfigurasi sesuai kebutuhan. Untuk informasi selengkapnya tentang konfigurasi, harap lihat <a href="https://intl.cloud.tencent.com/document/product/248/38911">Mengonfigurasi Templat Kondisi Pemicu</a>.</td>
  </tr>
        <tr>
        <td>Konfigurasikan Notifikasi Alarm (opsional)</td>
        <td colspan=2>Templat Notifikasi</td>
        <td>Pengaturan default-nya diatur ke templat notifikasi prasetel (mengirim notifikasi ke admin akun root melalui SMS dan email). Setiap kebijakan alarm dapat mengikat hingga 3 templat notifikasi. Untuk informasi selengkapnya tentang konfigurasi templat notifikasi, lihat <a href="https://intl.cloud.tencent.com/document/product/248/38922">Membuat Templat Notifikasi</a>.</li></td>
    </tr>
		</table>
4. Klik **Complete** (Selesai).





