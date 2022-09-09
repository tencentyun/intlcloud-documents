SMTPのメソッドで添付ファイル付きメールを送信する方法、すなわちMIME形式のメールコンテンツを作成します。
## メールMIME形式
プロトコルの詳細については、[MIMEプロトコル](https://www.ietf.org/rfc/rfc4021.html)をご参照ください。
>?MIMEメッセージは、メッセージヘッダーとメッセージボディの2つの主なパートから構成されています。これらは、[メールヘッダー](#head)、[メールボディ](#body)と呼ばれます。
[](id:head)
## メールヘッダー
送信者、受信者、件名、時刻、MIMEバージョン、メールコンテンツのタイプといった重要情報が含まれています。

>?各情報はドメインと呼ばれ、ドメイン名の後に付く「：」と情報内容で構成されています。1行にすることも、複数行になる長めのものにすることもできます。
>- ドメインの最初の行は、「トップ」に書き込む必要があります。すなわち、左側に空白文字（スペースやタブ）を入れないようにします。
>- 継続行の先頭は、空白文字で始まる必要があります。空白文字はメッセージ固有のものではありません（デコード時にフィルタリングします）。

メールヘッダーに空白行を入れることはできません。メールの中にはメールクライアントソフトで認識されず、1行目が空白行のため、元のコードが表示される場合があります。

例：
<table style="width: 400px;">
   <tr>
      <th width="50px" >コンテンツ</td>
      <th width="50px" >事例 </td>
   </tr>
   <tr>
      <td>Date</td>
      <td>Mon, 29 Jun 2009 18:39:03 +0800</td>
   </tr>
   <tr>
      <td>From</td>
      <td>abc@123.com</td>
   </tr>
   <tr>
      <td>To</td>
      <td>abc1@123.com</td>
   </tr>
   <tr>
      <td>BCC</td>
      <td>abc3@123.com</td>
   </tr>
   <tr>
      <td>Subject</td>
      <td>test</td>
   </tr>
   <tr>
      <td>Message-ID</td>
      <td>123@123.com</td>
   </tr>
   <tr>
      <td>Mime-Version</td>
      <td>1.0</td>
   </tr>
</table>

<table style="width: 400px;">
   <tr>
      <th width="50px" >ドメイン名</td>
      <th width="50px" >意味</td>
   </tr>
   <tr>
      <td>Bcc</td>
      <td>Bccアドレス</td>
   </tr>
   <tr>
      <td>Cc</td>
      <td>Ccアドレス</td>
   </tr>
   <tr>
      <td>Content-Transfer-Encoding</td>
      <td>コンテンツ転送エンコード</td>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>コンテンツのタイプ</td>
   </tr>
   <tr>
      <td>Date</td>
      <td>日付と時刻</td>
   </tr>
   <tr>
      <td>Delivered-To</td>
      <td>送信アドレス</td>
   </tr>
   <tr>
      <td>From</td>
      <td>送信者アドレス</td>
   </tr>
   <tr>
      <td>Message-ID</td>
      <td>メッセージID</td>
   </tr>
   <tr>
      <td>MIME-Version</td>
      <td>MIMEバージョン</td>
   </tr>
   <tr>
      <td>Received</td>
      <td>伝送パス</td>
   </tr>
   <tr>
      <td>Reply-To</td>
      <td>返信アドレス</td>
   </tr>
   <tr>
      <td>Return-Path</td>
      <td>返信アドレス</td>
   </tr>
   <tr>
      <td>Subject</td>
      <td>件名</td>
   </tr>
   <tr>
      <td>To</td>
      <td>受信者アドレス</td>
   </tr>
</table>

[](id:body)
## メールボディ
<table style="width: 400px;">
   <tr>
      <th width="50px" >ドメイン名</td>
      <th width="50px" >意味</td>
   </tr>
   <tr>
      <td>Content-ID</td>
      <td>コンテンツID</td>
   </tr>
   <tr>
      <td>Content-Transfer-Encoding</td>
      <td>コンテンツ転送エンコード</td>
   </tr>
   <tr>
      <td>Content-Location</td>
      <td>コンテンツの位置（パス）</td>
   </tr>
   <tr>
      <td>Content-Base</td>
      <td>コンテンツベース</td>
   </tr>
   <tr>
      <td>Content-Disposition</td>
      <td>コンテンツの配置方法</td>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>コンテンツタイプ</td>
   </tr>
</table>



ドメインの中には値の他にパラメータを持つものがあります。値とパラメータ、パラメータとパラメータの間は「;」で区切ります。パラメータ名とパラメータ値は「=」で区切ります。

- メールボディにはメールコンテンツが含まれ、そのタイプはメールヘッダーの`Content-Type`ドメインによって示されます。
>?一般的なシンプルタイプには、以下があります。
>- text/plain（プレーンテキスト） 
>- text/html（ハイパーテキスト）

- multipartタイプは、MIMEメールの基本です。メールボディは複数のフィールドに分割されており、各フィールドにはヘッダーとボディという2つの部分があります。これらも空白行で区切られています。

- 一般的なmultipartタイプには、以下3タイプあります。
  - multipart/mixed
  - multipart/related
  - multipart/alternative
上記の名前から、これらの各タイプの意味と用途がわかります。これらの階層的な関係をまとめると下図のようになります。
![](https://qcloudimg.tencent-cloud.cn/raw/c8fc71fa5b2e90fd96e5ad2755effd2b.png)
メールに添付ファイルを追加する場合は、multipart/mixedフィールドを定義する必要があります。埋め込みリソースがある場合は、少なくともmultipart/relatedフィールドを定義する必要があります。プレーンテキストとハイパーテキストが共存する場合、少なくとも multipart/alternativeフィールドを定義する必要があります。
>?添付ファイルの数は10件以下、個々の添付ファイルのサイズは4M以下、添付ファイルの合計サイズは8M以下とします。詳細については、[データ構造](https://intl.cloud.tencent.com/document/product/1084/39418#Attachment)をご参照ください。

## コード例
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
	host := "sg-smtp.qcloudmail.com"
	port := 465
	email := "abc@cd.com"
	password := "***"
	toEmail := "test@test123.com"
	header := make(map[string]string)
	header["From"] = "test " + "<" + email + ">"
	header["To"] = toEmail
	header["Subject"] = "Test465Attachment"
	header["Content-Type"] = "multipart/mixed;boundary=" + boundary
	//このフィールドは現在使用されておらず、デフォルトで1.0が渡されます
	header["Mime-Version"] = "1.0"
	//このフィールドは現在使用されていません
	header["Date"] = time.Now().String()
	bodyHtml := "<!DOCTYPE html>\n<html>\n<head>\n<meta charset=\"utf-8\">\n<title>hello world</title>\n</head>\n<body>\n " +
		"<h1>私の最初の件名</h1>\n    <p>私の最初の段落。</p>\n</body>\n</html>"
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
	//複数の添付ファイルをまとめます。添付ファイルは最大10件とし、添付ファイル1件につき5M以下、全添付ファイルの合計は8～9M以下とします。メッセージボディが大きすぎるとEOFを返します
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

// SendMailWithTLS send email with tls
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
