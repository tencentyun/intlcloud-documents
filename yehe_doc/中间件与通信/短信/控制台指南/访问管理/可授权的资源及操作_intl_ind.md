>!Dokumen ini menjelaskan fitur manajemen akses **SMS**. Informasi selengkapnya tentang manajemen akses untuk layanan Tencent Cloud lainnya dapat dilihat di [CAM-Enabled Products (Produk yang Didukung CAM)](https://intl.cloud.tencent.com/document/product/598/10588).

Fitur inti CAM adalah untuk **mengizinkan atau melarang akun melakukan operasi tertentu atau memanipulasi sumber daya tertentu**. Manajemen akses SMS mendukung [otorisasi tingkat sumber daya](https://intl.cloud.tencent.com/document/product/598/10588#.E7.AE.80.E4.BB.8B). Perincian sumber daya adalah aplikasi SMS, dan perincian operasi adalah [TencentCloud API (API TencentCloud)](https://intl.cloud.tencent.com/product/api), termasuk [API 3.0](https://intl.cloud.tencent.com/document/product/382/34689) dan API yang dapat digunakan saat konsol SMS diakses.

Jika Anda perlu mengelola akses ke SMS, silakan login ke Tencent Cloud [akun root](https://intl.cloud.tencent.com/document/product/598/34899) dan gunakan [kebijakan prasetel](https://intl.cloud.tencent.com/document/product/382/38455) atau [kebijakan kustom](https://intl.cloud.tencent.com/document/product/382/38456) untuk menyelesaikan operasi otorisasi khusus.

## Jenis Sumber Daya yang Dapat Diotorisasi
Jenis sumber daya yang dapat diotorisasi dalam manajemen akses SMS adalah aplikasi.

## API yang Mendukung Otorisasi Tingkat Sumber Daya
SMS mendukung otorisasi tingkat sumber daya untuk semua API konsol yang tercantum di bagian ini, tetapi tidak untuk API server. Deskripsi sintaks dari sumber daya yang dimanipulasi oleh API tersebut di [sintaks kebijakan otorisasi](https://intl.cloud.tencent.com/document/product/382/38456#.E6.8E.88.E6.9D.83.E7.AD.96.E7.95.A5.E8.AF.AD.E6.B3.95) bersifat identik, seperti yang dijelaskan di bawah ini:
- Memberikan izin untuk mengakses semua aplikasi: `qcs::sms::uin/$ownerUin:app/*`.
- Memberikan izin untuk mengakses satu aplikasi: `qcs::sms::uin/$ownerUin:app/$BizId`.

## Tindakan API Konsol

| Nama API | Modul yang Berlaku | Deskripsi Fitur |
|-----------------------------|--------------------------------------------------------|-------------|
| DescribeAppList             | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Application List (Aplikasi > Daftar Aplikasi) | Mendapatkan daftar aplikasi |
| DescribeAppInfo             | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Application List > Application Info (Aplikasi > Daftar Aplikasi > Info Aplikasi) | Mendapatkan informasi aplikasi |
| ModifyAppInfo               | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Application List > Application Info (Aplikasi > Daftar Aplikasi > Info Aplikasi) | Mengedit informasi aplikasi |
| ModifyAppStatus             | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Application List (Aplikasi > Daftar Aplikasi) | Mengaktifkan/Menonaktifkan aplikasi |
| DeleteAppInfo               | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Application List (Aplikasi > Daftar Aplikasi) | Menghapus aplikasi |
| DescribeWarningThreshold    | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Over-limit Delivery Notification (Aplikasi > Konfigurasi Dasar > Pemberitahuan Pengiriman Melebihi Batas) | Mendapatkan pemberitahuan pengiriman melebihi batas |
| ModifyWarningThreshold      | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Over-limit Delivery Notification (Aplikasi > Konfigurasi Dasar > Pemberitahuan Pengiriman Melebihi Batas) | Mengedit pemberitahuan pengiriman melebihi batas |
| DescribeFreqRule            | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Delivery Rate Limit (Aplikasi > Konfigurasi Dasar > Batas Tingkat Pengiriman) | Mendapatkan batas tingkat pengiriman |
| ModifyFreqRule              | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Delivery Rate Limit (Aplikasi > Konfigurasi Dasar > Batas Tingkat Pengiriman) | Mengedit batas tingkat pengiriman |
| DescribeCallbackInfo        | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Event Callback Configuration (Aplikasi > Konfigurasi Dasar > Konfigurasi Callback Peristiwa) | Mendapatkan konfigurasi callback |
| ModifyCallbackInfo          | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Event Callback Configuration (Aplikasi > Konfigurasi Dasar > Konfigurasi Callback Peristiwa) | Mengedit konfigurasi callback |
| DescribeFrequencyWhiteList  | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Rate Limit Allowlist (Aplikasi > Konfigurasi Dasar > Daftar Izin Batas Tingkat) | Mendapatkan daftar izin batas tingkat |
| AddFrequencyWhiteList       | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Rate Limit Allowlist (Aplikasi > Konfigurasi Dasar > Daftar Izin Batas Tingkat) | Menambahkan daftar izin batas tingkat |
| DeleteFrequencyWhiteList    | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Basic Configuration > Rate Limit Allowlist (Aplikasi > Konfigurasi Dasar > Daftar Izin Batas Tingkat) | Menghapus daftar izin batas tingkat |
| DescribeNewsReceiver        | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Notifications & Alarms (Aplikasi > Pemberitahuan & Alarm) | Mendapatkan informasi kontak alarm |
| AddNewsReceiver             | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Notifications & Alarms (Aplikasi > Pemberitahuan & Alarm) | Menambahkan informasi kontak alarm |
| ModifyNewsReceiver          | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Notifications & Alarms (Aplikasi > Pemberitahuan & Alarm) | Mengedit informasi kontak alarm |
| DeleteNewsReceiver          | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Applications > Notifications & Alarms (Aplikasi > Pemberitahuan & Alarm) | Menghapus informasi kontak alarm |
| ModifyTaskStatusStart       | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Mainland China SMS/Global SMS > Bulk SMS (SMS Tiongkok Daratan/SMS Global > SMS Massal) | Memulai tugas pengiriman instan atau terjadwal |
| ModifyTaskStatusStop        | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Mainland China SMS/Global SMS > Bulk SMS (SMS Tiongkok Daratan/SMS Global > SMS Massal) | Menghentikan tugas pengiriman instan |
| CancelSendSMSTask           | [SMS console (Konsol SMS)](https://console.cloud.tencent.com/smsv2) > Mainland China SMS/Global SMS > Bulk SMS (SMS Tiongkok Daratan/SMS Global > SMS Massal) | Membatalkan tugas pengiriman terjadwal |


>!Untuk API yang tidak mendukung kontrol izin tingkat sumber daya, Anda tetap dapat memberikan izin kepada pengguna untuk memakainya melalui [kebijakan kustom](https://intl.cloud.tencent.com/document/product/382/38456), tetapi Anda harus menentukan `*` sebagai elemen sumber daya dalam pernyataan kebijakan.

## Pembaruan Modul CAM

Modul CAM SMS telah diperbarui dari "consolesms" menjadi "sms". Jika akun Tencent Cloud Anda telah memberikan izin API sub-akun dari modul "consolesms" dalam kebijakan yang telah ditetapkan, sub-akun akan secara otomatis terikat ke izin API yang sesuai dari modul "sms". Jika suatu kebijakan kustom yang terkait dengan sub-akun berisi API dari modul "consolesms", Anda perlu mengganti API "consolesms" dengan API "sms" yang sesuai saat memperbarui sintaks kebijakan selanjutnya. Berikut ini adalah hubungan pemetaan API:

| API consolesms lama | API sms baru yang dipetakan |
|-------------------------------------------|-----------------------------|
| SMS\_GetAPPList                           | DescribeAppList            |
| SMS\_GetAPPInfo                           | DescribeAppInfo            |
| SMS\_GetWarningThreshold                  | DescribeWarningThreshold    |
| SMS\_GetFreqRule                          | DescribeFreqRule            |
| SMS\_GetCallbackList                      | DescribeCallbackInfo        |
| SMS\_GetFrqWhiteList                      | DescribeFrequencyWhiteList |
| SMS\_GetNewsReceiver                      | DescribeNewsReceiver       |
| SMS\_GetBlackListByQappid                 | DescribeBlackList           |
| SMS\_SendSMSResultStatisticQuery\_export  | DescribeSmsResultFile       |
| SMS\_Statistic\_QuerySMS\_ByAppid\_export | DescribeSmsRecordFile       |
| SMS\_StatisticQueryByQAppid               | DescribeStatisticQuery      |
| SMS\_QuerySendSMSByQAppid                 | DescribeSendSmsRecord       |
| SMS\_GetPkgAutoRenew                      | DescribePkgAutoRenew        |
| SMS\_QueryDumpLogTask                     | DescribeQueryDumpLogTask    |
| SMS\_QuerySendSMSDumpLogTask              | DescribeSendSmsDumpLogTask  |
| SMS\_CancelDumpLogTask                    | CancelDumpLogTask           |
| SMS\_AddDumpLogTask                       | AddDumpLogTask              |
| SMS\_GetWarningThreshold                  | DescribeWarningThreshold    |
| SMS\_StatisticNationCode                  | DescribeNationCodeStatistic |
| SMS\_SendSMSResultStatisticQuery          | DescribeSendSMSResult       |
| SMS\_Stat\_InnerQuery\_Reply              | DescribeInnerSMSReply       |
| SMS\_QuerySendSMSTaskSummary              | DescribeSendSMSTaskSummary  |
| SMS\_StatisticMonth                       | DescribeMonthStatistic      |
| SMS\_QuerySendSMSStatistic                | DescribeSendSMSStatistic    |
| SMS\_QuerySendSMSDetail                   | DescribeSendSMSDetail       |
| SMS\_QuerySmsPkgRemain                    | DescribeSmsPkgRemain        |
| SMS\_GetPackageList                       | DescribePackageList         |
| SMS\_UnsubscribeQuery                     | DescribeUnsubscribe         |
| SMS\_ReceiptAnalysis                      | DescribeReceiptResult       |
| SMS\_GetTPLSignInfo                       | DescribeTPLSignInfo         |
| SMS\_GetTPLSignList                       | DescribeTPLSignList         |


Akibat peningkatan versi konsol, beberapa API dalam "consolesms" modul CAM tidak lagi digunakan. Jika API berikut terdapat dalam kebijakan kustom yang terkait dengan sub-akun Anda, silakan hapus konten yang relevan dalam sintaks kebijakan:

| API | Status |
|-------------------------------------------|-----------------------------|
| SMS\_Stat\_InnerQuery\_export             | Tidak digunakan                        |
| SMS\_GetConsoleFlag                       | Tidak digunakan                        |
| SMS\_IsWhiteDumpAppid                     | Tidak digunakan                        |
| SMS\_IsWhiteAppId                         | Tidak digunakan                        |
| SMS\_QueryBill\_export                    | Tidak digunakan                        |
| SMS\_CheckAppidBizid                      | Tidak digunakan                        |
| SMS\_GetAllBizList                        | Tidak digunakan                        |
| SMS\_GetSMSNotice                         | Tidak digunakan                        |
| Voice\_GetSelfAccountTypes                | Tidak digunakan                        |
| Voice\_GetAccountTypeInfo                 | Tidak digunakan                        |
| Voice\_GetBizTypes                        | Tidak digunakan                        |
| Voice\_GetBizAndAccountTypeInfo           | Tidak digunakan                        |
| SMS\_GetServiceState                      | Tidak digunakan                        |
| SMS\_StatisticQueryIOTAnalysis            | Tidak digunakan                        |
| SMS\_StatisticQueryIOTByOper              | Tidak digunakan                        |
| SMS\_StatisticQueryIOT                    | Tidak digunakan                        |
| SMS\_Stat\_InnerQueryVoice                | Tidak digunakan                        |
| SMS\_StatisticQueryEx                     | Tidak digunakan                       |
| SMS\_StatisticQueryNew                    | Tidak digunakan                        |
| SMS\_GetNewsReceiverFlag                  | Tidak digunakan                        |
| SMS\_QueryTemplateStatisticEx             | Tidak digunakan                        |
| SMS\_QueryTemplateStatistic               | Tidak digunakan                        |
| SMS\_QueryBill                            | Tidak digunakan                       |
| SMS\_QuerySendSMSRemain                   | Tidak digunakan                        |
| SMS\_QuerySendSMS                         | Tidak digunakan                        |
| SMS\_IsWhiteUin                           | Tidak digunakan                        |
| SMS\_GetBlackList                         | Tidak digunakan                        |
| SMS\_Statistic\_QuerySMS\_export          | Tidak digunakan                        |
| SMS\_GetSendList                          | Tidak digunakan                        |
| SMS\_GetReceiver                          | Tidak digunakan                        |
| SMS\_Query\_Black                         | Tidak digunakan                        |



