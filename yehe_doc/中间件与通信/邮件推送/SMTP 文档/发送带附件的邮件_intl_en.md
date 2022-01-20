The method of sending an email with an attachment through SMTP is to construct the content of a MIME-formatted email.
## Email MIME Format
For more information, see [MIME Protocol](https://www.ietf.org/rfc/rfc4021.html).
>?A MIME message consists of two parts: [email header](#head) and [email body](#body).
[](id:head)
## Email Header
The email header contains important information such as sender, recipient, subject, time, MIME version, and body type.

>?Each piece of information is called a field, which consists of a domain followed by ":" and the information content and can be in one or multiple lines.
>- The first line of a field must be written "to the left", i.e., without whitespace characters (spaces and tabs) on the left.
>- The next lines must start with whitespace characters, one of which must not be inherent in the message itself (that is, it needs to be filtered out during decoding).

Blank lines are not allowed in the email header. If the first line is blank, some emails cannot be recognized by certain email client software, and the original code is displayed.

For example:
<table style="width: 400px;">
   <tr>
      <th width="50px" >Content</td>
      <th width="50px" >Example</td>
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
      <th width="50px" >Field</td>
      <th width="50px" >Description</td>
   </tr>
   <tr>
      <td>Bcc</td>
      <td>Blind carbon copy address</td>
   </tr>
   <tr>
      <td>Cc</td>
      <td>Copy address</td>
   </tr>
   <tr>
      <td>Content-Transfer-Encoding</td>
      <td>Content transfer encoding method</td>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>Content type</td>
   </tr>
   <tr>
      <td>Date</td>
      <td>Date and time</td>
   </tr>
   <tr>
      <td>Delivered-To</td>
      <td>Recipient address</td>
   </tr>
   <tr>
      <td>From</td>
      <td>Sender address</td>
   </tr>
   <tr>
      <td>Message-ID</td>
      <td>Message ID</td>
   </tr>
   <tr>
      <td>MIME-Version</td>
      <td>MIME version</td>
   </tr>
   <tr>
      <td>Received</td>
      <td>Transfer path</td>
   </tr>
   <tr>
      <td>Reply-To</td>
      <td>Reply-to address</td>
   </tr>
   <tr>
      <td>Return-Path</td>
      <td>Reply-to address</td>
   </tr>
   <tr>
      <td>Subject</td>
      <td>Subject</td>
   </tr>
   <tr>
      <td>To</td>
      <td>Recipient address</td>
   </tr>
</table>

[](id:body)
## Email Body
<table style="width: 400px;">
   <tr>
      <th width="50px" >Field</td>
      <th width="50px" >Description</td>
   </tr>
   <tr>
      <td>Content-ID</td>
      <td>Content ID</td>
   </tr>
   <tr>
      <td>Content-Transfer-Encoding</td>
      <td>Content transfer encoding method</td>
   </tr>
   <tr>
      <td>Content-Location</td>
      <td>Content location (path)</td>
   </tr>
   <tr>
      <td>Content-Base</td>
      <td>Content base location</td>
   </tr>
   <tr>
      <td>Content-Disposition</td>
      <td>Content disposition method</td>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>Content type</td>
   </tr>
</table>



Some fields have parameters in addition to values. Value and parameter as well as parameter and parameter are separated with ";". Parameter name and parameter value are separated with "=".

- The email body contains the content of the email, whose type is indicated by the `Content-Type` field in the email header.
>?Common simple types include:
>- text/plain (plain text) 
>- text/html (hypertext)

- The multipart type is the essence of MIME emails. The email body is divided into multiple parts, each of which consists of part header and part body separated by a blank line.

- There are three common multipart types:
 - multipart/mixed
 - multipart/related
 - multipart/alternative
The meaning and use of each of these types can be seen from their names. The hierarchical relationship between them can be summarized as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/c8fc71fa5b2e90fd96e5ad2755effd2b.png)
If you want to add attachments to an email, you must define the `multipart/mixed` part. If there are embedded resources, you must define at least the `multipart/related` part; if plain text and hypertext coexist, you must define at least the `multipart/alternative` part.
>?The number of attachments should not exceed 10, the size of a single attachment should not exceed 5 MB, and the total size of all attachments should not exceed 10 MB. For more information, see [Data Structure](https://intl.cloud.tencent.com/document/product/1084/39418#Attachment).

## Sample Code
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
	// This field is not used for the time being. Pass in `1.0` by default
	header["Mime-Version"] = "1.0"
	// This field is not used for the time being
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
	// Multiple attachments can be spliced at the end. There can be 10 attachments at most, each of which cannot exceed 5 MB in size. The TOTAL size of all attachments cannot exceed 8–9 MB; otherwise, EOF will be returned
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
