Tencent Cloud SESで添付ファイル付きのメッセージを送信する場合、添付ファイルの形式は表の**サポート**タイプに従って送信する必要があります。以下は、Tencent Cloud SESでサポートされている添付ファイルの種類と制限のリストです。
>!ISPによっては他の制限がある場合もありますので、本番環境でEメールを送信する前に、主要な送信ISPで添付ファイルがスムーズに到達するかどうかテストすることをお勧めします。

<table>
<thead>
<tr>
<th>サポートあり</th>
<td style="word-break: break-all"><code>.xlsx</code>,<code>.xls</code>,<code>.ods</code>,<code>.docx</code>,<code>.docm</code>,<code>.doc</code>,<code>.csv</code>,<code>.pdf</code>,<code>.txt</code>,<code>.gif</code>,<code>.jpg</code>,<code>.jpeg</code>,<code>.png</code>,<code>.tif</code>,<code>.tiff</code>,<code>.rtf</code>,<code>.bmp</code>,<code>.cgm</code>,<code>.css</code>,<code>.shtml</code>,<code>.html</code>,<code>.htm</code>,<code>.zip</code>,<code>.xml</code>,<code>.ppt</code>,<code>.pptx</code>,<code>.tar</code>,<code>.ez</code>,<code>.ics</code>,<code>.mobi</code>,<code>.msg</code>,<code>.pub</code>,<code>.eps</code>,<code>.odt</code>,<code>.mp3</code>,<code>.m4a
</code></td></tr>
</thead>
<tbody><tr>
<th>サポートなし</th>
<td style="word-break: break-all"><code>.m4v</code>,<code>.wma</code>,<code>.ogg</code>,<code>.flac</code>,<code>.wav</code>,<code>.aif</code>,<code>.aifc</code>,<code>.aiff</code>,<code>.mp4</code>,<code>.mov</code>,<code>.avi</code>,<code>.mkv</code>,<code>.mpeg</code>,<code>.mpg</code>,<code>.wmv</code>,<code>.ade</code>,<code>.adp</code>,<code>.app</code>,<code>.asp</code>,<code>.bas</code>,<code>.bat</code>,<code>.cer</code>,<code>.chm</code>,<code>.cmd</code>,<code>.com</code>,<code>.cpl</code>,<code>.crt</code>,<code>.csh</code>,<code>.der</code>,<code>.exe</code>,<code>.fxp</code>,<code>.gadget</code>,<code>.hlp</code>,<code>.hta</code>,<code>.inf</code>,<code>.ins</code>,<code>.isp</code>,<code>.its</code>,<code>.js</code>,<code>.jse</code>,<code>.ksh</code>,<code>.lib</code>,<code>.lnk</code>,<code>.mad</code>,<code>.maf</code>,<code>.mag</code>,<code>.mam</code>,<code>.maq</code>,<code>.mar</code>,<code>.mas</code>,<code>.mat</code>,<code>.mau</code>,<code>.mav</code>,<code>.maw</code>,<code>.mda</code>,<code>.mdb</code>,<code>.mde</code>,<code>.mdt</code>,<code>.mdw</code>,<code>.mdz</code>,<code>.msc</code>,<code>.msh</code>,<code>.msh1</code>,<code>.msh2</code>,<code>.mshxml</code>,<code>.msh1xml</code>,<code>.msh2xml</code>,<code>.msi</code>,<code>.msp</code></td>
</tr>
</tbody></table>

>?添付ファイル名には、「? \ * | " < > : /」といった特殊文字やスペースを含めることはできません。

