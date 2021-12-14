腾讯云重视客户信息的安全性和保密性，因此在和客户之间的电子邮件通信实施了S/MIME数字签名，以防止邮件在传输过程中被他人篡改。本文将详细解释收件人应该如何阅读和验证经过数字签名的邮件。

#### 如何阅读和验证经过数字签名的邮件的签名
- 邮件列表或阅读窗格中的丝带图标![](https://qcloudimg.tencent-cloud.cn/raw/978c0e157642c059d023b4c44835552e.png)表示邮件经过数字签名。
- 如果您通常使用对话视图，您必须在新窗口中打开邮件才能阅读它，有关数字签名的信息位于邮件顶部。
  ![](https://qcloudimg.tencent-cloud.cn/raw/e002606d95f8cc1331a8c152a55dfd96.png)
- 若要检查签名是否有效，请单击签名者状态行上的![](https://qcloudimg.tencent-cloud.cn/raw/978c0e157642c059d023b4c44835552e.png)。 然后，若要查看有关数字签名的详细信息，请单击“详细信息”。
![](https://qcloudimg.tencent-cloud.cn/raw/6619a1691f6c05ef540e4c389bcbd411.png)
![](https://qcloudimg.tencent-cloud.cn/raw/9e8d3e9a771bc6832f6bdba889610f6a.png)

#### 检查邮件数字签名我需要了解的其他信息
- Internet Explorer 9 或更高版本对接收经过数字签名的邮件或验证您收到的邮件上的数字签名是必需的。
- 经过数字签名的邮件可再次向收件人保证邮件未被篡改，并验证发件人的身份。 收件人必须使用支持 S/MIME 的电子邮件应用程序并且安装了 S/MIME 控件才能验证数字签名。 Outlook 和 Outlook Web App 都支持 S/MIME。
- **邮件（S/MIME） 证书支持的常用客户端包括：**
<table>
<thead>
  <tr>
    <th colspan="2"  style="text-align:center">平台</th>
    <th colspan="5" style="text-align:center">客户端</th>
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

- 需要 S/MIME 控件才能验证经过数字签名的邮件的签名，但证书不是必需的。 如果您收到经过数字签名的邮件，但是未安装 S/MIME 控件，那么您将在邮件标题中看到一个警告，通知您 S/MIME 控件不可用。 该消息会将您定向到 S/MIME 选项页面帮助您安装该控件。

