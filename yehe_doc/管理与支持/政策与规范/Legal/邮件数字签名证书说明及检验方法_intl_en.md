Tencent Cloud value the security and confidentiality of our customers’ information. In order to prevent the email from being tempered during transmission, we implement digital signature via S/MIME on our email communication with our customers. The text below elaborates how recipients can read and verify a digitally signed email.

#### How to read and verify a digitally signed email
- A ribbon icon![](https://qcloudimg.tencent-cloud.cn/raw/978c0e157642c059d023b4c44835552e.png)in the message list or reading pane indicates a digitally signed message.
- If you normally use Conversation view, you'll have to open the message in a new window to read it. Information about the digital signature will be at the top of the message.
  ![](https://qcloudimg.tencent-cloud.cn/raw/e002606d95f8cc1331a8c152a55dfd96.png)
- If you would like to check whether the signature is valid, please click the![](https://qcloudimg.tencent-cloud.cn/raw/978c0e157642c059d023b4c44835552e.png)in the message list, and you can also select to learn more about the digital signature by clicking “Details…”.

![](https://qcloudimg.tencent-cloud.cn/raw/0bae064bc150b2d62411754d9645ae24.png)
![](https://qcloudimg.tencent-cloud.cn/raw/75f74cbc6c69b27ef890c277547cdedc.png)

#### Other information for checking the digital signature
- Internet Explorer 9 or more updated versions is required to receive digitally sign messages and to verify digital signatures on messages that you receive.
- A digitally signed message reassures the recipient that the message hasn't been tampered with and verifies the identity of the sender. Recipients must be using an email application that supports S/MIME and have installed the S/MIME control to verify the digital signature. Outlook and Outlook on the web both support S/MIME.
- **Common clients supporting Email S/MIME certificate include:**
<table>
<thead>
  <tr>
    <th colspan="2"  style="text-align:center">Platform</th>
    <th colspan="5" style="text-align:center">Client</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="3" style="text-align:center">Desktop</td>
    <td style="text-align:center">Windows</td>
    <td style="text-align:center">Outlook</td>
    <td style="text-align:center">Thunderbird</td>
    <td style="text-align:center">IBM Notes</td>
    <td colspan="2" style="text-align:center">Postbox</td>
  </tr>
  <tr>
    <td style="text-align:center">Mac</td>
    <td style="text-align:center">Mail</td>
    <td style="text-align:center">Airmail</td>
    <td style="text-align:center">Postbox</td>
    <td colspan="2" style="text-align:center">Thunderbird</td>
  </tr>
  <tr>
    <td style="text-align:center">Linux</td>
    <td  style="text-align:center">KMail</td>
    <td colspan="4" style="text-align:center">Thunderbird</td>
  </tr>
  <tr>
    <td rowspan="3" style="text-align:center">Mobile</td>
    <td style="text-align:center">iOS</td>
    <td style="text-align:center">Mail</td>
    <td style="text-align:center">WorxMail</td>
    <td colspan="3" style="text-align:center"> Outlook</td>
  </tr>
  <tr>
    <td style="text-align:center">Android</td>
    <td style="text-align:center">CipherMail</td>
    <td style="text-align:center">Nine</td>
    <td style="text-align:center">MailDroid</td>
    <td style="text-align:center">Sony Mail</td>
    <td style="text-align:center">Outlook</td>
  </tr>
  <tr>
    <td style="text-align:center">Windows phone</td>
    <td style="text-align:center">Citrix</td>
    <td style="text-align:center">BlackBerry</td>
    <td colspan="3" style="text-align:center"> Outlook</td>
  </tr>
  <tr>
    <td style="text-align:center">Web</td>
    <td colspan="6" style="text-align:center">Outlook Web Access/Outlook Web App
		</td>
  </tr>
	</tbody>
 </table>

- The S/MIME control is necessary to verify the signatures of digitally signed messages, but a certificate is not. If you receive a message that's been digitally signed and you haven't installed the S/MIME control, you'll see a warning in the message header notifying you that the S/MIME control isn't available. The message will direct you to the S/MIME options page where you can download an S/MIME control installer for the web browser you're using.
