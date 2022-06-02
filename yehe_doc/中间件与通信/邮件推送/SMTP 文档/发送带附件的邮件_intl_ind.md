Metode pengiriman email dengan lampiran melalui SMTP adalah dengan membuat konten email berformat MIME.
## Format Email MIME
Untuk informasi selengkapnya, lihat [Protokol MIME](https://www.ietf.org/rfc/rfc4021.html).
>?Pesan MIME terdiri dari dua bagian: [email header](#head) dan [email body](#body).
[](id:head)
## Header Email
Header email berisi informasi penting seperti pengirim, penerima, subjek, waktu, versi MIME, dan jenis badan email.

>?Setiap informasi disebut bidang, yang terdiri dari domain yang diikuti oleh ":" dan konten informasi dan dapat dalam satu atau beberapa baris.
>- Baris pertama bidang harus ditulis "di sebelah kiri", yaitu, tanpa karakter spasi (spasi dan tab) di sebelah kiri.
>- Baris berikutnya harus dimulai dengan karakter spasi, salah satunya tidak boleh melekat pada pesan itu sendiri (yaitu, perlu disaring selama decoding).

Baris kosong tidak diperbolehkan di header email. Jika baris pertama kosong, beberapa email tidak dapat dikenali oleh perangkat lunak klien email tertentu, dan kode aslinya ditampilkan.

Sebagai contoh:
<table style="width: 400px;">
   <tr>
      <th width="50px" >Konten</td>
      <th width="50px" >Contoh</td>
   </tr>
   <tr>
      <td>Tanggal</td>
      <td>Sen, 29 Jun 2009 18.39:03 +0800</td>
   </tr>
   <tr>
      <td>Dari</td>
      <td>abc@123.com</td>
   </tr>
   <tr>
      <td>Kepada</td>
      <td>abc1@123.com</td>
   </tr>
   <tr>
      <td>BCC</td>
      <td>abc3@123.com</td>
   </tr>
   <tr>
      <td>Subjek</td>
      <td>test</td>
   </tr>
   <tr>
      <td>ID-Pesan</td>
      <td>123@123.com</td>
   </tr>
   <tr>
      <td>Mime-Version</td>
      <td>1.0</td>
   </tr>
</table>

<table style="width: 400px;">
   <tr>
      <th width="50px" >Bidang</td>
      <th width="50px" >Deskripsi</td>
   </tr>
   <tr>
      <td>Bcc</td>
      <td>Alamat BCC</td>
   </tr>
   <tr>
      <td>Cc</td>
      <td>Salin alamat</td>
   </tr>
   <tr>
      <td>Pengkodean-Transfer-Konten</td>
      <td>Metode pengkodean transfer konten</td>
   </tr>
   <tr>
      <td>Jenis-Konten</td>
      <td>Jenis konten</td>
   </tr>
   <tr>
      <td>Tanggal</td>
      <td>Tanggal dan waktu</td>
   </tr>
   <tr>
      <td>Dikirim-Ke</td>
      <td>Alamat penerima</td>
   </tr>
   <tr>
      <td>Dari</td>
      <td>Alamat pengirim</td>
   </tr>
   <tr>
      <td>ID-Pesan</td>
      <td>ID Pesan</td>
   </tr>
   <tr>
      <td>Versi-MIME</td>
      <td>Versi MIME</td>
   </tr>
   <tr>
      <td>Diterima</td>
      <td>Jalur transfer</td>
   </tr>
   <tr>
      <td>Balas-Ke</td>
      <td>Alamat balas-ke</td>
   </tr>
   <tr>
      <td>Jalur-Kembali</td>
      <td>Alamat balas-ke</td>
   </tr>
   <tr>
      <td>Subjek</td>
      <td>Subjek</td>
   </tr>
   <tr>
      <td>Kepada</td>
      <td>Alamat penerima</td>
   </tr>
</table>

[](id:body)
## Badan Email
<table style="width: 400px;">
   <tr>
      <th width="50px" >Bidang</td>
      <th width="50px" >Deskripsi</td>
   </tr>
   <tr>
      <td>ID-Konten</td>
      <td>ID Konten</td>
   </tr>
   <tr>
      <td>Pengkodean-Transfer-Konten</td>
      <td>Metode pengkodean transfer konten</td>
   </tr>
   <tr>
      <td>Lokasi-Konten</td>
      <td>Lokasi konten (jalur)</td>
   </tr>
   <tr>
      <td>Basis-Konten</td>
      <td>Lokasi basis konten</td>
   </tr>
   <tr>
      <td>Disposisi-Konten</td>
      <td>Metode disposisi konten</td>
   </tr>
   <tr>
      <td>Jenis-Konten</td>
      <td>Jenis konten</td>
   </tr>
</table>



Beberapa bidang memiliki parameter selain nilainya. Nilai dan parameter serta parameter dan parameter dipisahkan dengan ";". Nama parameter dan nilai parameter dipisahkan dengan "=".

- Badan email berisi konten email, yang jenisnya ditunjukkan oleh bidang `Content-Type` di header email.
>?Jenis sederhana umum meliputi:
>- teks/biasa (teks biasa) 
>- teks/html (hiperteks)

- Jenis multi bagian adalah inti dari email MIME. Badan email dibagi menjadi beberapa bagian yang masing-masing terdiri dari bagian header dan bagian badan email yang dipisahkan oleh garis kosong.

- Ada tiga tipe multi bagian umum:
  - multi bagian/campuran (multipart/mixed)
  - multi bagian/terkait (multipart/related)
  - multi bagian/alternatif (multipart/alternative)
Arti dan kegunaan dari masing-masing jenis ini bisa dilihat dari namanya. Hubungan hierarkis di antara mereka dapat diringkas seperti yang ditunjukkan di bawah ini:
![](https://qcloudimg.tencent-cloud.cn/raw/c8fc71fa5b2e90fd96e5ad2755effd2b.png)
Jika Anda ingin menambahkan lampiran ke email, Anda harus menentukan bagian `multipart/mixed`. Jika ada sumber daya yang disematkan, Anda harus mendefinisikan setidaknya bagian `multipart/related`; jika teks biasa dan hiperteks hidup berdampingan, Anda harus mendefinisikan setidaknya bagian `multipart/alternative`.
>?Jumlah lampiran tidak boleh lebih dari 10, ukuran satu lampiran tidak boleh melebihi 4 MB, dan ukuran total semua lampiran tidak boleh melebihi 8 MB. Untuk informasi selengkapnya, lihat [Stuktur Data](https://intl.cloud.tencent.com/document/product/1084/39418#Attachment).

## Kode sampel
<dx-codeblock>
:::  go
package main
import (
	"bytes"
	"crypto/tls"
	"encoding/base64"
	"fmt"
	"io/ioutil"
	"log"
	"mime"
	"net"
	"net/smtp"
	"time"
)

// Test465Attachment  for port 465
func Test465Attachment() error {
	boundary := "GoBoundary"
	host := "smtp.qcloudmail.com"
	port := 465
	email := "abc@cd.com"
	password := "***"
	toEmail := "test@test123.com"
	header := make(map[string]string)
	header["From"] = "test " + "<" + email + ">"
	header["To"] = toEmail
	header["Subject"] = "Test465Attachment"
	header["Content-Type"] = "multipart/mixed;boundary=" + boundary
	// Bidang ini tidak digunakan untuk saat ini. Masukkan `1.0` secara default
	header["Mime-Version"] = "1.0"
	// Bidang ini tidak digunakan untuk saat ini
	header["Date"] = time.Now().String()
	bodyHtml := "<!DOCTYPE html>\n<html>\n<head>\n<meta charset=\"utf-8\">\n<title>hello world</title>\n</head>\n<body>\n " +
		"<h1>My first heading</h1>\n    <p>My first paragraph.</p>\n</body>\n</html>"
	message := ""
	for k, v := range header {
		message += fmt.Sprintf("%s: %s\r\n", k, v)
	}
	buffer := bytes.NewBuffer(nil)
	buffer.WriteString(message)
	contentType := "Content-Type: text/html" + "; charset=UTF-8"
	body := "\r\n--" + boundary + "\r\n"
	body += "Content-Type:" + contentType + "\r\n"
	body += "\r\n" + bodyHtml + "\r\n"
	buffer.WriteString(body)

	attachment := "\r\n--" + boundary + "\r\n"
	attachment += "Content-Transfer-Encoding:base64\r\n"
	attachment += "Content-Disposition:attachment\r\n"
	attachment += "Content-Type:" + "application/octet-stream" + ";name=\"" + mime.BEncoding.Encode("UTF-8",
		"./go.mod") + "\"\r\n"
	buffer.WriteString(attachment)
	writeFile(buffer, "./go.mod")
	// Beberapa lampiran dapat disambungkan di akhir. Paling banyak ada 10 lampiran, yang masing-masing tidak boleh lebih dari 5 MB. Ukuran TOTAL semua lampiran tidak boleh melebihi 8–9 MB; jika tidak, EOF akan dikembalikan
	attachment1 := "\r\n--" + boundary + "\r\n"
	attachment1 += "Content-Transfer-Encoding:base64\r\n"
	attachment1 += "Content-Disposition:attachment\r\n"
	attachment1 += "Content-Type:" + "application/octet-stream" + ";name=\"" + mime.BEncoding.Encode("UTF-8",
		"./bbbb.txt") + "\"\r\n"
	buffer.WriteString(attachment1)
	writeFile(buffer, "./bbbb.txt")
	defer func() {
		if err := recover(); err != nil {
			log.Fatalln(err)
		}
	}()
	
	buffer.WriteString("\r\n--" + boundary + "--")
	message += "\r\n" + body
	auth := smtp.PlainAuth(
		"",
		email,
		password,
		host,
	)
	err := SendMailWithTLS(
		fmt.Sprintf("%s:%d", host, port),
		auth,
		email,
		[]string{toEmail},
		buffer.Bytes(),
	)
	if err != nil {
		fmt.Println("Send email error:", err)
	} else {
		fmt.Println("Send mail success!")
	}
	return err
}

// Dial return a smtp client
func Dial(addr string) (*smtp.Client, error) {
	conn, err := tls.Dial("tcp", addr, nil)
	if err != nil {
		log.Println("tls.Dial Error:", err)
		return nil, err
	}

	host, _, _ := net.SplitHostPort(addr)
	return smtp.NewClient(conn, host)
}

// SendMailWithTLS mengirim email dengan tls
func SendMailWithTLS(addr string, auth smtp.Auth, from string,
	to []string, msg []byte) (err error) {
	//create smtp client
	c, err := Dial(addr)
	if err != nil {
		log.Println("Create smtp client error:", err)
		return err
	}
	defer c.Close()
	if auth != nil {
		if ok, _ := c.Extension("AUTH"); ok {
			if err = c.Auth(auth); err != nil {
				log.Println("Error during AUTH", err)
				return err
			}
		}
	}
	if err = c.Mail(from); err != nil {
		return err
	}
	for _, addr := range to {
		if err = c.Rcpt(addr); err != nil {
			return err
		}
	}
	w, err := c.Data()
	if err != nil {
		return err
	}
	_, err = w.Write(msg)
	if err != nil {
		return err
	}
	err = w.Close()
	if err != nil {
		return err
	}
	return c.Quit()
}

// writeFile read file to buffer
func writeFile(buffer *bytes.Buffer, fileName string) {
	file, err := ioutil.ReadFile(fileName)
	if err != nil {
		panic(err.Error())
	}
	payload := make([]byte, base64.StdEncoding.EncodedLen(len(file)))
	base64.StdEncoding.Encode(payload, file)
	buffer.WriteString("\r\n")
	for index, line := 0, len(payload); index < line; index++ {
		buffer.WriteByte(payload[index])
		if (index+1)%76 == 0 {
			buffer.WriteString("\r\n")
		}
	}
}

func main() {
	Test465Attachment()
}
:::
</dx-codeblock>
