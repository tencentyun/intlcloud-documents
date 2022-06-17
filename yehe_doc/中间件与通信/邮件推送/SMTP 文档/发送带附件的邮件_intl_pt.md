O método de enviar um e-mail com um anexo por SMTP é criar o conteúdo de um e-mail formatado em MIME.
## Formato MIME de e-mail
Para obter mais informações, consulte [Protocolo MIME](https://www.ietf.org/rfc/rfc4021.html).
>?Uma mensagem MIME consiste em duas partes: [cabeçalho do e-mail](#head) e [corpo do e-mail](#body).
[](id:head)
## Cabeçalho do e-mail
O cabeçalho do e-mail contém informações importantes, como remetente, destinatário, assunto, hora, versão do MIME e tipo de corpo.

>?Cada informação é chamada de campo, que consiste em um domínio seguido por “:” e o conteúdo da informação, podendo estar em uma ou várias linhas.
>- A primeira linha de um campo deve ser escrita “à esquerda”, ou seja, sem caracteres de espaço em branco (espaços e tabulações) à esquerda.
>- As próximas linhas devem começar com caracteres de espaço em branco, um dos quais não deve ser inerente à própria mensagem (ou seja, precisa ser filtrado durante a decodificação).

Não são permitidas linhas em branco no cabeçalho do e-mail. Se a primeira linha estiver em branco, alguns e-mails não poderão ser reconhecidos pelo software de alguns clientes de e-mail e o código original será exibido.

Por exemplo:
<table style="width: 400px;">
   <tr>
      <th width="50px" >Conteúdo</td>
      <th width="50px" >Exemplo</td>
   </tr>
   <tr>
      <td>Date</td>
      <td>Seg, 29 de junho de 2009 18:39:03 +0800</td>
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
      <td>teste</td>
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
      <th width="50px" >Campo</td>
      <th width="50px" >Descrição</td>
   </tr>
   <tr>
      <td>Bcc</td>
      <td>Endereço de cópia oculta</td>
   </tr>
   <tr>
      <td>Cc</td>
      <td>Endereço de cópia</td>
   </tr>
   <tr>
      <td>Content-Transfer-Encoding</td>
      <td>Método de codificação de transferência de conteúdo</td>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>Tipo de conteúdo</td>
   </tr>
   <tr>
      <td>Date</td>
      <td>Data e hora</td>
   </tr>
   <tr>
      <td>Delivered-To</td>
      <td>Endereço do destinatário</td>
   </tr>
   <tr>
      <td>From</td>
      <td>Endereço do remetente</td>
   </tr>
   <tr>
      <td>Message-ID</td>
      <td>ID da mensagem</td>
   </tr>
   <tr>
      <td>MIME-Version</td>
      <td>Versão do MIME</td>
   </tr>
   <tr>
      <td>Received</td>
      <td>Caminho de transferência</td>
   </tr>
   <tr>
      <td>Reply-To</td>
      <td>Endereço de resposta</td>
   </tr>
   <tr>
      <td>Return-Path</td>
      <td>Endereço de resposta</td>
   </tr>
   <tr>
      <td>Subject</td>
      <td>Assunto</td>
   </tr>
   <tr>
      <td>To</td>
      <td>Endereço do destinatário</td>
   </tr>
</table>

[](id:body)
## Corpo do e-mail
<table style="width: 400px;">
   <tr>
      <th width="50px" >Campo</td>
      <th width="50px" >Descrição</td>
   </tr>
   <tr>
      <td>Content-ID</td>
      <td>ID do conteúdo</td>
   </tr>
   <tr>
      <td>Content-Transfer-Encoding</td>
      <td>Método de codificação de transferência de conteúdo</td>
   </tr>
   <tr>
      <td>Content-Location</td>
      <td>Local do conteúdo (caminho)</td>
   </tr>
   <tr>
      <td>Content-Base</td>
      <td>Local da base de conteúdo</td>
   </tr>
   <tr>
      <td>Content-Disposition</td>
      <td>Método de disposição de conteúdo</td>
   </tr>
   <tr>
      <td>Content-Type</td>
      <td>Tipo de conteúdo</td>
   </tr>
</table>



Alguns campos possuem parâmetros além de valores. Valor e parâmetro, assim como parâmetro e parâmetro, são separados por “;”. O nome do parâmetro e o valor do parâmetro são separados por “=”.

- O corpo do e-mail contém o conteúdo do e-mail, cujo tipo é indicado pelo campo `Content-Type` no cabeçalho do e-mail.
>?Tipos simples incluem:
>- texto/sem formatação (texto sem formatação) 
>- texto/html (hipertexto)

- O tipo de várias partes é a essência dos e-mails com formatação MIME. O corpo do e-mail é dividido em várias partes, cada uma das quais consiste no cabeçalho e no corpo das respectivas partes, separadas por uma linha em branco.

- Existem três tipos comuns com várias partes:
  - multipart/mixed (várias partes/mista)
  - multipart/related (várias partes/relacionada)
  - multipart/alternative (várias partes/alternativa)
O significado e o uso de cada um desses tipos podem ser determinados através de seus nomes. A relação hierárquica entre eles pode ser resumida como mostrado abaixo:
![](https://qcloudimg.tencent-cloud.cn/raw/c8fc71fa5b2e90fd96e5ad2755effd2b.png)
Se deseja adicionar anexos a um e-mail, você deve definir a parte `multipart/mixed`. Se houver recursos incorporados, você deve definir pelo menos a parte `multipart/related`; se texto simples e hipertexto coexistem, você deve definir pelo menos a parte `multipart/alternative`.
>?A quantidade de anexos não deve exceder 10, o tamanho de um único anexo não deve exceder 4 MB e o tamanho total de todos os anexos não deve exceder 8 MB. Para obter mais informações, consulte [Estrutura de dados](https://intl.cloud.tencent.com/document/product/1084/39418#Attachment).

## Código de exemplo
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

// Test465Attachment  para a porta 465
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
	// Este campo não é usado por enquanto. Passe `1.0` por padrão
	header["Mime-Version"] = "1.0"
	// Este campo não é usado por enquanto
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
	// É possível unir vários anexos no final. Pode haver no máximo dez anexos, cada um dos quais não pode exceder 5 MB de tamanho. O tamanho TOTAL de todos os anexos não pode exceder 8–9 MB; caso contrário, será retornado EOF
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

// Dial retorna um cliente smtp
func Dial(addr string) (*smtp.Client, error) {
	conn, err := tls.Dial("tcp", addr, nil)
	if err != nil {
		log.Println("tls.Dial Error:", err)
		return nil, err
	}

	host, _, _ := net.SplitHostPort(addr)
	return smtp.NewClient(conn, host)
}

// SendMailWithTLS envia e-mail com tls
func SendMailWithTLS(addr string, auth smtp.Auth, from string,
	to []string, msg []byte) (err error) {
	//cria cliente smtp
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

// writeFile lê o arquivo para buffer
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
