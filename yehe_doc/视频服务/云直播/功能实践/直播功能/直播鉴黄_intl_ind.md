
Untuk mengaktifkan deteksi pornografi selama streaming langsung, Anda perlu mengaktifkan pengambilan tangkapan layar di [konsol CSS](https://intl.cloud.tencent.com/document/product/267/31072) atau melalui API. Dokumen ini menjelaskan cara menerapkan deteksi pornografi melalui API.

## Mengaktifkan Deteksi Pornografi
Karena fitur deteksi pornografi didasarkan pada pengambilan tangkapan layar, Anda harus mengaktifkan pengambilan tangkapan layar terlebih dahulu agar dapat mengaktifkan deteksi pornografi. Langkah-langkahnya dijelaskan sebagai berikut:

### 1. Membuat templat pengambilan tangkapan layar dengan mengaktifkan deteksi pornografi
Panggil [CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834), dengan mengatur `PornFlag` ke `1` untuk membuat templat pengambilan tangkapan layar dengan mengaktifkan deteksi pornografi.

### 2. Membuat aturan pengambilan tangkapan layar
Panggil [CreateLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30835) untuk membuat aturan pengambilan tangkapan layar dengan mengikatkan ID templat pengambilan tangkapan layar yang dibuat di langkah 1 ke `AppId`, `DomainName`, `AppName`, dan `StreamName` target.

### 3. Memulai streaming langsung
Setelah Anda membuat aturan pengambilan tangkapan layar dengan mengaktifkan deteksi pornografi, fitur deteksi pornografi akan diaktifkan secara otomatis untuk streaming baru. Jika ingin mengaktifkan deteksi pornografi untuk streaming yang sedang berlangsung, Anda harus menghentikan dan memulai ulang streaming.

## Mendapatkan Hasil Deteksi Pornografi
Setelah deteksi pornografi diaktifkan, Anda dapat mengonfigurasikan nama domain terdaftar di templat panggilan balik deteksi pornografi untuk menerima panggilan balik hasil deteksi pornografi.
>! Secara default, panggilan balik hanya diterapkan pada hasil yang dipertanyakan.

### 1. Membuat templat panggilan balik deteksi pornografi
Panggil [CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815), dengan mengatur `PornCensorshipNotifyUrl` ke nama domain Anda untuk membuat templat panggilan balik deteksi pornografi.
### 2. Membuat aturan panggilan balik deteksi pornografi

Panggil [CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816) untuk membuat aturan panggilan balik deteksi pornografi dengan mengikatkan ID templat panggilan balik deteksi pornografi yang dibuat di langkah 1 ke `AppId`, `DomainName`, dan `AppName` target.

### 3. Mendapatkan hasil deteksi pornografi
Backend CSS mengirimkan hasil deteksi pornografi ke nama domain terdaftar Anda melalui permintaan HTTP POST, lalu hasil tersebut disimpan di isi HTTP dalam format JSON. Anda dapat menentukan apakah streaming langsung termasuk dalam kategori pornografi atau tidak dengan mencentang bidang `type` (jenis).
>!Anda sebaiknya menggunakan `type` (jenis) suatu gambar untuk menentukan streaming langsung termasuk dalam kategori pornografi atau tidak. Karena sistem deteksi tidak dapat mencapai akurasi 100%, kemungkinan ada positif palsu atau negatif palsu sehingga konfirmasi manusia perlu diberikan.  

#### Protokol lengkap dapat dilihat di bagian berikut:
| Parameter       | Diperlukan | Jenis Data | Deskripsi    |
| -------- | -------- | -------- | -------- |
| streamId       | Tidak         | String       | Nama streaming    |
| channelId      | Tidak         | String       | ID saluran                                                      |
| img            | Ya         | String       | Tautan ke gambar yang diberi peringatan                                               |
| type    | Ya     | Array    | Kategori label negatif dengan prioritas tertinggi dalam hasil deteksi. Keterangan lengkap dapat dilihat di deskripsi `label`. |
| score | Ya | Array | Skor `type` |
| ocrMsg         | Tidak         | String       | Hasil OCR (jika ada)                         |
| suggestion | Ya | String | Saran. Nilai valid: <ul style="margin:0"><li/>Blokir<li/>Peninjauan<li/>Lulus</ul>     |
| label       | Ya     | String   | Label negatif dengan prioritas tertinggi dalam hasil deteksi (`LabelResults`). Ini adalah hasil moderasi yang direkomendasikan berdasarkan model. Anda sebaiknya menangani berbagai jenis pelanggaran dan saran berdasarkan kebutuhan bisnis Anda. |
| subLabel    | Ya     | String   | Sub-label di bawah label negatif dengan prioritas tertinggi dalam hasil deteksi, misalnya pornografi - tindakan seksual. Jika tidak ada konten yang diberi sub-label, bidang ini akan kosong. |
| labelResults   | Tidak     | [Array LabelResult](#labelresult)   | Detail hit label negatif untuk model kategori, termasuk konten pornografi yang terdeteksi, iklan, konten terorisme, dan konten yang sensitif secara politik <br>Catatan: **Bidang ini mungkin menampilkan nilai `null`, yang berarti bahwa tidak ada nilai valid yang diperoleh.** |
| objectResults  | Tidak     | [Array ObjectResult](#objectresult) | Hasil deteksi model objek, termasuk nama label, skor hit, koordinat, skenario, dan rekomendasi operasi yang berkaitan dengan objek, logo iklan, kode QR, dll. Keterangan lengkap dapat dilihat di deskripsi struktur data `ObjectResults`. <br> Catatan: **Bidang ini mungkin menampilkan nilai `null`, yang berarti bahwa tidak ada nilai valid yang diperoleh.** |
| ocrResults     | Tidak     | [Array OcrResult](#ocrresult)    | Hasil OCR, termasuk koordinat teks, teks yang dikenali, rekomendasi operasi, dll. Keterangan lengkap dapat dilihat di deskripsi struktur data `OcrResults`.<br> Catatan: **Bidang ini mungkin menampilkan nilai `null`, yang berarti bahwa tidak ada nilai valid yang diperoleh.** |
| libResults | Tidak    | [Array LibResult](#libresult) | Hasil moderasi Daftar Blokir/Daftar Izin  |
| screenshotTime | Ya         | Angka       | Waktu pengambilan tangkapan layar              |
| sendTime       | Ya         | Angka       | Waktu pengiriman permintaan dalam format stempel waktu Unix  |
| stream_param   | Tidak         | String       | Parameter push                              |
| app   | Tidak | String | Nama domain push   |
| appid  | Tidak | Angka |  ID Aplikasi |
| appname        | Tidak        | String       | Jalur push  |

 

#### LabelResult
Hasil hit untuk model kategori

| Parameter | Jenis | Deskripsi |
| ---------- | ------------------------ | ------------------------ |
| Scene      | String                                      | Skenario yang teridentifikasi oleh model, misalnya iklan, pornografi, dan berbahaya     |
| Suggestion | String                                       | Operasi yang direkomendasikan sistem untuk label negatif saat ini. Anda sebaiknya menangani berbagai jenis pelanggaran dan saran berdasarkan kebutuhan bisnis Anda. Nilai yang ditampilkan:<ul style="margin:0"><li/>Blokir<li/>Peninjauan<li/>Lulus</ul> |
| label | String   | Label negatif dalam hasil deteksi |
| SubLabel   | String | Nama sub-label |
| Score      | Integer | Skor hit untuk model label                                         |
| Details    | Array [LabelDetailItem](#labeldetailitem) | Detail hit sub-label untuk model kategori                                   |

#### LabelDetailItem

Detail hit sub-label untuk model kategori

| Parameter | Jenis | Deskripsi |
| -------- | -------- | ----- |
| Id       | Integer  | ID                        |
| Name     | String   | Nama sub-label                  |
| Score    | Integer  | Skor sub-label. Rentang nilai: 0‒100 |


#### ObjectResult

Hasil deteksi objek

| Parameter| Jenis | Deskripsi |
| ---------- | --------------------- | --------------------- |
| Scene      | String                                       | Skenario objek yang teridentifikasi, seperti kode QR, logo, dan OCR     |
| Suggestion | String                                       | Operasi yang direkomendasikan sistem untuk label negatif saat ini. Anda sebaiknya menangani berbagai jenis pelanggaran dan saran berdasarkan kebutuhan bisnis Anda. Nilai yang ditampilkan:<ul style="margin:0"><li/>Blokir<li/>Peninjauan<li/>Lulus</ul> |
| label | String   | Label negatif dalam hasil deteksi |
| SubLabel   | String | Nama sub-label |
| Score    | Integer | Skor hit sub-label untuk model skenario. Rentang nilai: 0‒100 |
| Name      | Array String       | Daftar nama objek |
| Details    | Array [ObjectDetail](#objectdetail) | Detail deteksi objek |

#### ObjectDetail

Detail deteksi objek. Ketika skenario deteksi adalah objek, logo iklan, atau kode QR, hasil yang ditampilkan berupa nama label, nilai label, skor label, dan informasi lokasi untuk frame deteksi.

| Parameter | Jenis | Deskripsi |
| -------- | -------- | -------- |
| Id    | Integer    | ID objek yang teridentifikasi    |
| Name     | String     | Label objek yang teridentifikasi   |
| Value    | String     | Nilai atau konten dari label objek yang teridentifikasi. Sebagai contoh, jika label adalah kode QR (`QrCode`), parameter ini akan berupa URL dari kode QR tersebut. |
| Score    | Integer    | Skor hit dari label objek. Rentang nilai: 0‒100. Sebagai contoh, `QrCode 99` menunjukkan kemungkinan yang tinggi bahwa konten berupa kode QR. |
| Location | [Lokasi](#location) | Koordinat (sudut kiri atas), dimensi, dan rotasi frame deteksi objek |

#### Lokasi

Koordinat dan informasi lain tentang frame deteksi

| Parameter | Jenis | Deskripsi |
| -------- | -------- | ---------------- |
| X        | Float    | Koordinat horizontal di sudut kiri atas     |
| Y        | Float    | Koordinat vertikal di sudut kiri atas     |
| Width    | Float    | Lebar             |
| Height   | Float    | Tinggi             |
| Rotate   | Float    | Sudut rotasi frame deteksi |

#### OcrResult

Hasil OCR

| Parameter| Jenis | Deskripsi |
| ---------- | ---------------------- | ---------------------- |
| Scene      | String                                   | Skenario pengenalan. Nilai default: OCR              |
| Suggestion | String                                       | Operasi yang direkomendasikan sistem untuk label negatif dengan prioritas tertinggi. Anda sebaiknya menangani berbagai jenis pelanggaran dan saran berdasarkan kebutuhan bisnis Anda. Nilai yang ditampilkan:<ul style="margin:0"><li/>Blokir<li/>Peninjauan<li/>Lulus</ul> |
| label | String   | Label negatif dalam hasil deteksi |
| SubLabel   | String | Nama sub-label |
| Score    | Integer | Skor hit sub-label untuk model skenario. Rentang nilai: 0‒100 |
| Text       | String | Teks |
| Details    | Array [OcrTextDetail](#ocrtextdetail) | Detail OCR |


#### OcrTextDetail
Detail OCR

| Parameter | Jenis | Deskripsi |
| -------- | --------------- | --------------- |
| Text | String | Teks yang dikenali (hingga **5.000 byte**) |
| label | String   | Label negatif dalam hasil deteksi |
| Keywords | Array String | Hit kata kunci dengan label yang sama |
| Score    | Integer  | Skor hit untuk model label. Rentang nilai: 0‒100 |
| Location | [Lokasi](#location) | Koordinat teks OCR |


#### LibResult
Hasil Daftar Blokir/Daftar Izin

| Parameter| Jenis | Deskripsi |
| ---------- | ------------------ | ------------------ |
| Scene      | String                           | Hasil pengenalan skenario untuk model. Nilai default: Similar                 |
| Suggestion | String                                       | Operasi yang direkomendasikan sistem. Anda sebaiknya menangani berbagai jenis pelanggaran dan saran berdasarkan kebutuhan bisnis Anda. Nilai yang ditampilkan:<ul style="margin:0"><li/>Blokir<li/>Peninjauan<li/>Lulus</ul> |
| label | String   | Label negatif dalam hasil deteksi |
| SubLabel   | String | Nama sub-label |
| Score | Integer | Skor pengenalan untuk model pencarian gambar. Rentang nilai: 0‒100 |
| Details    | Array [LibDetail](#libdetail) | Detail Daftar Blokir/Daftar Izin |

#### LibDetail
Detail daftar kustom atau daftar blokir/daftar izin

| Parameter | Jenis | Deskripsi |
| -------- | -------- | ------------------ |
| Id       | Integer  | ID                        |
| ImageId  | String   | ID Gambar                                                       |
| label | String   | Label negatif dalam hasil deteksi |
| Tag | String | Label kustom |
| Score | Integer | Skor pengenalan model. Rentang nilai: 0‒100 |



#### Pesan panggilan balik sampel
<dx-codeblock>
::: HTTPbody  json
{
        "ocrMsg": "",
        "type": [1],
        "socre": 99,
        "screenshotTime": 1610640000,
        "level": 0,
        "img": "http://1.1.1.1/download/porn/test.jpg",
        "abductionRisk": [],
        "faceDetails": [],
        "sendTime": 1615859827,
        "suggestion": "Block",
        "label": "Porn",
        "subLabel": "PornHigh",
        "labelResults": [{
                "HitFlag": 0,
                "Scene": "Illegal",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }, {
                "HitFlag": 1,
                "Scene": "Porn",
                "Suggestion": "Block",
                "Label": "Porn",
                "SubLabel": "PornHigh",
                "Score": 99,
                "Details": [{
                        "Id": 0,
                        "Name": "PornHigh",
                        "Score": 99
                }, {
                        "Id": 1,
                        "Name": "WomenChest",
                        "Score": 99
                }]
        }, {
                "HitFlag": 0,
                "Scene": "Sexy",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "Terror",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }],
        "objectResults": [{
                "HitFlag": 0,
                "Scene": "QrCode",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "MapRecognition",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "PolityFace",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }],
        "ocrResults": [{
                "HitFlag": 0,
                "Scene": "OCR",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Text": "",
                "Details": []
        }],
        "streamId": "teststream",
        "channelId": "teststream",
        "stream_param": "txSecret=40f38f69f574fd51126c421a3d96c374&txTime=5DEBEC80",
        "app": "5000.myqcloud.com",
        "appname": "live",
        "appid": 10000,
        "event_type": 317,
        "sign": "ac920c3e66**********78cf1b5de2c63",
        "t": 1615860427
}
:::
</dx-codeblock>



## Menonaktifkan Deteksi Pornografi

Anda dapat menonaktifkan deteksi pornografi dengan menghapus aturan pengambilan tangkapan layar atau memodifikasi templat pengambilan tangkapan layar. Deteksi dan modifikasi hanya akan diterapkan pada streaming langsung baru. Jika ingin menonaktifkan deteksi pornografi untuk streaming yang sedang berjalan, Anda harus menghentikan dan memulai ulang streaming.

### 1. Menghapus aturan pengambilan tangkapan layar

Panggil [DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833), dengan memasukkan `DomainName`, `AppName`, dan `StreamName` yang diikatkan ke ID templat pengambilan tangkapan layar untuk menghapus aturan pengambilan tangkapan layar.

### 2. Memodifikasi templat pengambilan tangkapan layar

Panggil [ModifyLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30828), dengan mengatur `PornFlag` ke `0`.
