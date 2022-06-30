Speech Synthesis Markup Language (SSML) is based on XML to define the effects of synthetic speeches more accurately and specifically.  
>? 
>- Tencent TTS implements SSML based on [Speech Synthesis Markup Language (SSML) Version 1.1](https://www.w3.org/TR/speech-synthesis/).
>- Currently, the SSML feature is supported only for Chinese.

## Directions
The tagged text is uploaded to TTS as the value of the `text` parameter. Below is the content of the request sent to TTS:
```
{
 "Action" : "TextToVoice",
 "AppId" : 12345,
 "Codec" : "mp3",
 "Expired" : 1603271036,
 "ModelType" : 1,
 "PrimaryLanguage" : 1,
 "ProjectId" : 0,
 "SampleRate" : 8000,
 "SecretId" : "AKID****",
 "SessionId" : "1234",
 "Speed" : 0,
 "Text" : "<speak>The mobile number is <say-as interpret-as=\"telephone\">4008110510</say-as>.</speak>",
 "Timestamp" : 1603184636,
 "VoiceType" : 1002,
 "Volume" : 5
}
```

TTS supports SSML [tags](#jump). Here, text in undefined `<speak>` tags will not be synthesized, and an incorrect XML format may interrupt synthesizing the text in `<speak>` tags.

The SSML feature of TTS supports nesting multiple `<speak>` tags in the text; for example:
```
<speak>Her name is <say-as interpret-as="name">Ren Yingying</say-as>.
Her mobile number is <say-as interpret-as="telephone">+86-15188888888</say-as>.
She is <say-as interpret-as="cardinal">22</say-as> years old.
She has a package with the tracking number <say-as interpret-as="digits">5648234514237588</say-as>.
Her address is <say-as interpret-as="address">304, Unit 3, No. 10,000, Shennan Boulevard</say-as>.
</speak>By the way,<speak>
Her username is <say-as interpret-as="characters">b888_uαβγ</say-as>.
</speak>
```

[](id:jump)
## Tag
### &lt;speak&gt;
#### Description
```
The `<speak>` tag is the root node of all SSML tags to be supported but doesn't support attributes. All text for which to call SSML tags must be enclosed in `<speak></speak>`.
```

#### Syntax
```
<speak>Text for which to call SSML tags</speak>
```

#### Tag relationships
The `<speak>` tag can contain text and the following tags: `<break>`, `<phoneme>`, `<say-as>`, and `<sub>`.

#### Sample
```
<speak>Text for which to call SSML tags.</speak>
```
Output speech audio: [SSML-speak1.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/SSML-speak1.wav)

### &lt;sub&gt;
#### Description
This tag uses an alias to replace the text in it.

#### Syntax
```
<sub alias="Alias">Text</sub>
```

#### Attributes
<table>
<thead>
<tr>
<th>Attribute</th>
<th>Type</th>
<th>Value</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>alias</td>
<td>String</td>
<td>New content</td>
<td>Yes</td>
<td>It is used to replace the text in the tag.</td>
</tr>
</tbody></table>

#### Tag relationships
This tag can contain text only.

#### Sample
```
<speak><sub alias="TTS">TTS</sub></speak>
```
Output speech audio: [SSML-sub.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/SSML-sub.wav)

### &lt;break&gt;
#### Description
This optional tag is used to insert a pause in the text.

#### Syntax
```
<break time="string"/>
```

#### Attributes
<table>
<thead>
<tr>
<th>Attribute</th>
<th>Type</th>
<th>Value</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>time</td>
<td>String</td>
<td>[number]s/[number]ms</td>
<td>Yes</td>
<td>You can set the pause duration in seconds or milliseconds, such as `2s` or `50ms`. [number]s: The unit is second, and the value of `[number]` must be an integer between 1 and 10. [number]ms: The unit is millisecond, and the value of `[number]` must be an integer between 50 and 10000.</td>
</tr>
</tbody></table>

#### Tag relationships
`<break>` is an empty tag and cannot contain any tags.

#### Sample
```
<speak>Close your eyes and take a rest<break time="500ms"/>OK. Now open your eyes.</speak>
```

### &lt;phoneme&gt;
#### Description
This optional tag is used to control the pronunciation of the text in it.

#### Syntax
```
<phoneme alphabet="py" ph="Pinyin string">Text</phoneme>
```
<table>
<thead>
<tr>
<th>Attribute</th>
<th>Type</th>
<th>Value</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>alphabet</td>
<td>String</td>
<td>py</td>
<td>Yes</td>
<td>`py` indicates pinyin.</td>
</tr>
<tr>
<td>ph</td>
<td>String</td>
<td>Pinyin string of the text in the tag</td>
<td>Yes</td>
<td>Limits on the pinyin value: <br>- Pinyin syllables of different characters need to be separated with spaces, and the number of pinyin syllables must be the same as the number of Chinese characters.<br>- Each pinyin syllable consists of the pronunciation and tone. The tone is an integer between 1 and 5, where 5 indicates a neutral tone.</td>
</tr>
</tbody></table>

#### Tag relationships
The `<phoneme>` tag can contain text only.

#### Sample
```
<speak>
Currently, the economic levels of different areas are <phoneme alphabet="py" ph="cen1 ci1 bu4 qi2">uneven</phoneme>. We need to bridge the <phoneme alphabet="py" ph="cha1 ju4">gap</phoneme> between the richer and poorer areas. However, the <phoneme alphabet="py" ph="chai1 shi4">job</phoneme> is not easy.
</speak>
```
Output speech audio: [SSML-phoneme.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/SSML-phoneme.wav)

### &lt;say-as&gt;
#### Description
This tag is used to specify the information type of the text in it. The text will then be spoken in the default pronunciation method for the specified information type.

#### Syntax
```
<say-as interpret-as="string">Text</say-as>
```
<table>
<thead>
<tr>
<th>Attribute</th>
<th>Type</th>
<th>Value</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>interpret-as</td>
<td>String</td>
<td>cardinal/digits/telephone/name/address/<br>id/characters/punctuation/<br>date/time/currency/measure</td>
<td>Yes</td>
<td>Information type of the text in the tag: <br>• cardinal: Speak the text as an integral or decimal number. <br>• digits: Speak the text as individual digits.<br>• telephone: Speak the text in a common way of saying phone numbers.<br>• name: Speak the text as a name.<br>• address: Speak the text as an address.<br>• id: Speak the text as an account name or nickname.<br>• characters: Speak the text as individual characters.<br>• punctuation: Speak the text as a punctuation mark.<br>• date: Speak the text as a date.<br>• time: Speak the text as a time.<br>• currency: Speak the text as an amount of money.<br>• measure: Speak the text as a number with a unit.</td>
</tr>
</tbody></table>

#### Values supported by each &lt;say-as&gt; type
- cardinal
 <table>
<tr>
<th>Format</th>
<th>Example</th>
<th>Output</th>
<th>Description</th>
</tr>
<tr>
<td>Digit string</td>
<td>1487</td>
<td>One thousand four hundred and eighty-seven</td>
<td rowspan="8">Integral value range: [-18446744073709551615,18446744073709551615].<br>Decimal value range: The number of decimal places is unlimited but should be no more than 10 preferably.</td>
</tr>
<tr>
<td>Minus sign + digit string</td>
<td>-1487</td>
<td>Negative one thousand four hundred and eighty-seven</td>
</tr>
<tr>
<td>Digit string where every three digits are separated with a comma</td>
<td>10,500</td>
<td>Ten thousand five hundred</td>
</tr>
<tr>
<td>Minus sign + digit string where every three digits are separated with a comma</td>
<td>-10,500</td>
<td>Negative ten thousand five hundred</td>
</tr>
<tr>
<td>Digit string + decimal point + two zeros</td>
<td>9.00</td>
<td>Nine</td>
</tr>
<tr>
<td>Minus sign + digit string + decimal point + two zeros</td>
<td>-110.00</td>
<td>Negative one hundred and ten</td>
</tr>
<tr>
<td>Digit string + decimal point + digit string</td>
<td>88.090</td>
<td>Eighty-eight point zero nine</td>
</tr>
<tr>
<td>Minus sign + digit string + decimal point + digit string</td>
<td>-88.001</td>
<td>Negative eighty-eight point zero nine</td>
</tr>
</table>
- digits
 <table>
<tr>
<th>Format</th>
<th>Example</th>
<th>Output</th>
<th>Description</th>
</tr>
<tr>
<td>Digit string</td>
<td>356210985</td>
<td>Three five six two one zero nine eight five</td>
<td>The length of the digit string is unlimited.<br>We recommend you use no more than 20 digits and insert a pause after each digit if the string contains more than 10 digits.</td>
</tr>
</table>
- telephone
 <table>
<tr>
<th>Format</th>
<th>Example</th>
<th>Output</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="6">Landline number</td>
<td>5605560</td>
<td>Five six oh  five five six oh</td>
<td rowspan="6">7- and 8-digit landline numbers are supported. Different groups of digits can be separated with spaces or `-`.<br>Here, a 7-digit landline number can be separated in the "3 digits-4 digits" format, and an 8-digit one can be separated in the "4 digits-4 digits" format.</td>
</tr>
<tr>
<td>560 5560</td>
<td>Five six oh  five five six oh</td>
</tr>
<tr>
<td>560-5560</td>
<td>Five six oh  five five six oh</td>
</tr>
<tr>
<td>55605560</td>
<td>Five five six oh  five five six oh</td>
</tr>
<tr>
<td>5560 5560</td>
<td>Five five six oh  five five six oh</td>
</tr>
<tr>
<td>5560-5560</td>
<td>Five five six oh  five five six oh</td>
</tr>
<tr>
<td rowspan="4">Landline number + extension</td>
<td>55605560-105</td>
<td>Five five six oh  five five six oh  extension one oh five</td>
<td rowspan="4">The extension can contain 1–4 digits.</td>
</tr>
<tr>
<td>55605560 ext. 105</td>
<td>Five five six oh  five five six oh  extension one oh five</td>
</tr>
<tr>
<td>55605560 extension 105</td>
<td>Five five six oh  five five six oh  extension one oh five</td>
</tr>
<tr>
<td>55605560 extension 105</td>
<td>Five five six oh  five five six oh  extension one oh five</td>
</tr>
<tr>
<td rowspan="6">Area code + landline number</td>
<td>01055605560</td>
<td>Oh one oh  five five six oh  five five six oh</td>
<td rowspan="6">The following area codes are supported: 010, 02x, 03xx, 04xx, 05xx, 07xx, 08xx, and 09xx.</td>
</tr>
<tr>
<td>010 55605560</td>
<td>Oh one oh  five five six oh  five five six oh</td>
</tr>
<tr>
<td>010-5560-5560</td>
<td>Oh one oh  five five six oh  five five six oh</td>
</tr>
<tr>
<td>(010)55605560</td>
<td>Oh one oh  five five six oh  five five six oh</td>
</tr>
<tr>
<td>031955605560</td>
<td>Oh three one nine  five five six oh  five five six oh</td>
</tr>
<tr>
<td>0319-55605560</td>
<td>Oh three one nine  five five six oh  five five six oh</td>
</tr>
<tr>
<td rowspan="6">Area code + landline number + extension</td>
<td>010 33878528-1054</td>
<td>Oh one oh  three three eight seven  eight five two eight  extension one oh five four</td>
<td rowspan="6">None</td>
</tr>
<tr>
<td>010-33878528-1054</td>
<td>Oh one oh  three three eight seven  eight five two eight  extension one oh five four</td>
</tr>
<tr>
<td>(010)33878528-1054</td>
<td>Oh one oh  three three eight seven  eight five two eight  extension one oh five four</td>
</tr>
<tr>
<td>(010)33878528 ext. 1054</td>
<td>Oh one oh  three three eight seven  eight five two eight  extension one oh five four</td>
</tr>
<tr>
<td>(010)33878528 extension 1054</td>
<td>Oh one oh  three three eight seven  eight five two eight  extension one oh five four</td>
</tr>
<tr>
<td>(010)33878528 extension 1054</td>
<td>Oh one oh  three three eight seven  eight five two eight  extension one oh five four</td>
</tr>
<tr>
<td rowspan="5">Country code + area code + landline number</td>
<td>86-010-33878528</td>
<td>Eight six  oh one oh  three three eight seven</td>
<td rowspan="5">Country codes in the following formats are supported: 86, (86), +86, (+86), and 0086, which are collectively spoken as "eight six".</td>
</tr>
<tr>
<td>(86)10-33878528</td>
<td>Eight six  one oh  three three eight seven  eight five two eight</td>
</tr>
<tr>
<td>+86-010-33878528</td>
<td>Eight six  oh one oh  three three eight seven  eight five two eight</td>
</tr>
<tr>
<td>0086-10-33878528</td>
<td>Eight six  one oh  three three eight seven  eight five two eight</td>
</tr>
<tr>
<td>(+86)-10-3387 8528</td>
<td>Eight six  one oh  three three eight seven  eight five two eight</td>
</tr>
<tr>
<td rowspan="5">Country code + area code + landline number + extension</td>
<td>(86)21-33878528-1054</td>
<td>Eight six  two one  three three eight seven  eight five two eight  extension one oh five four</td>
<td rowspan="5">None</td>
</tr>
<tr>
<td>(86)021-3387-8528-1054</td>
<td>Eight six  oh two one  three three eight seven  eight five two eight  extension one oh five four</td>
</tr>
<tr>
<td>(86)021-33878528 ext. 1054</td>
<td>Eight six  oh two one  three three eight seven  eight five two eight  extension one oh five four</td>
</tr>
<tr>
<td>(86)21-3387-8528 extension 1054</td>
<td>Eight six  two one  three three eight seven  eight five two eight  extension one oh five four</td>
</tr>
<tr>
<td>+86-021-3387-8528 extension 1054</td>
<td>Eight six  oh two one  three three eight seven  eight five two eight  extension one oh five four</td>
</tr>
<tr>
<td rowspan="3">Mobile number</td>
<td>151 8828 1075</td>
<td>One five one  eight eight two eight  one oh seven five</td>
<td rowspan="3">11-digit mobile numbers separated in "3-3-5" and "3-4-4" formats are supported.</td>
</tr>
<tr>
<td>151-882-81075</td>
<td>One five one  eight eight two  eight one oh seven five</td>
</tr>
<tr>
<td>151-8828-1075</td>
<td>One five one  eight eight two eight  one oh seven five</td>
</tr>
<tr>
<td rowspan="4">Country code + mobile number</td>
<td>+86-15188281075</td>
<td>Eight six  one five one  eight eight two eight  one oh seven five</td>
<td rowspan="4">None</td>
</tr>
<tr>
<td>(+86)-151-8828-1075</td>
<td>Eight six  one five one  eight eight two eight  one oh seven five</td>
</tr>
<tr>
<td>+8615188281075</td>
<td>Eight six  one five one  eight eight two eight  one oh seven five</td>
</tr>
<tr>
<td>0086-151 882 81075</td>
<td>Eight six  one five one  eight eight two  eight one oh seven five</td>
</tr>
<tr>
<td rowspan="5">Service number</td>
<td>110</td>
<td>Oh oh one</td>
<td rowspan="5"><ul><li/>Common service numbers such as 110 are supported.<li/>10-digit service numbers beginning with 400 and 800 and separated in "3-3-4" format are supported.<br><li/>16-digit service numbers beginning with 12530, 17951, and 12593 are supported.</ul></td>
</tr>
<tr>
<td>95566</td>
<td>Nine five five six six</td>
</tr>
<tr>
<td>4008110280</td>
<td>Four oh oh  eight one one  oh two eight oh</td>
</tr>
<tr>
<td>800-810-8888</td>
<td>Eight oh oh  eight one oh  eight eight eight eight</td>
</tr>
<tr>
<td>1253013520638377</td>
<td>One two five three oh  one three five  two oh six three  eight three seven seven</td>
</tr>
<tr>
<td>Other</td>
<td>(86)(21)8832-80976-0907</td>
<td>Eight six  two one  eight eight three two  eight oh nine seven six  oh nine oh seven</td>
<td>Digit strings separated with left and right parentheses or hyphens are supported.</td>
</tr>
</table>
- address
 <table>
<tr>
<th>Format</th>
<th>Example</th>
<th>Output</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="5">Common address format</td>
<td>103-3, No. 1,000, Shennan Boulevard</td>
<td>One oh three dash three  Number one oh oh oh  Shennan Boulevard</td>
<td rowspan="5">Standard postal addresses in common formats are supported.</td>
</tr>
<tr>
<td>No.1137-1128, Alley 377, Gaoxin Middle Avenue 4th Road</td>
<td>Number one one three seven dash one one two eight  Alley three seven seven  Gaoxin Middle Avenue Fourth Road</td>
</tr>
<tr>
<td>3-1-3805, Phase 6, Huaruncheng</td>
<td>Number three dash one dash three eight oh five  Phase six  Huaruncheng</td>
</tr>
<tr>
<td>Room 2106, Building 2, Dazu Yunfeng</td>
<td>Room two one oh six  Building two  Dazu Yunfeng</td>
</tr>
<tr>
<td>No.19, Alley 151, Gaoxin Middle Avenue 3rd Road</td>
<td>Number one nine  Alley one five one  Gaoxin Middle Avenue Third Road</td>
</tr>
</table>
- id
 <table>
<tr>
<th>Format</th>
<th>Example</th>
<th>Output</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="3">String</td>
<td>dell3301</td>
<td>D E L L three three oh one</td>
<td rowspan="3">It can contain letters, digits, and underscores.<br>Spaces between two characters in the output result indicate a pause. Characters separated with spaces are spoken one by one.</td>
</tr>
<tr>
<td>tencent_1998</td>
<td>T E N C E N T underscore one nine nine eight</td>
</tr>
<tr>
<td>AiDemo</td>
<td>A I D E M O</td>
</tr>
</table>
- characters
 <table>
<tr>
<th>Format</th>
<th>Example</th>
<th>Output</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="8">String</td>
<td>ISO 1-001-095498-1</td>
<td>I S O one dash oh oh one dash oh five four oh nine eight dash one</td>
<td rowspan="8">It can contain letters, digits, and certain full-width and half-width characters.<br>Spaces between two characters in the output result indicate a pause. Characters separated with spaces are spoken one by one. If the text in the tag contains special XML symbols, they need to be escaped, commonly including: <br>&amp;lt;<br>&amp;gt;<br>&amp;amp;<br>&amp;quot;<br>&amp;apos;<br>They represent `<`, `>`,`&`, `"`, and `'` respectively.
</td>
</tr>
<tr>
<td>x10u2385_u</td>
<td>X one zero U two three eight five underscore U</td>
</tr>
<tr>
<td>v1.1.1</td>
<td>V one dot one dot one</td>
</tr>
<tr>
<td>Version 2.0</td>
<td>Version two dot oh</td>
</tr>
<tr>
<td>Yue B BA000</td>
<td>Yue B B A oh oh oh</td>
</tr>
<tr>
<td>Airbus A330</td>
<td>Airbus A three three oh</td>
</tr>
<tr>
<td>Models B01, B02, and B03</td>
<td>Models B oh one B oh two and B oh three</td>
</tr>
<tr>
<td>αβγ</td>
<td>Alpha beta gamma</td>
</tr>
</table>
- punctuation
 <table>
<tr>
<th>Format</th>
<th>Example</th>
<th>Output</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="7">Punctuation mark</td>
<td>...</td>
<td>Ellipsis</td>
<td rowspan="7">It supports common punctuation marks. Spaces between two characters in the output result indicate a pause. Characters separated with spaces are spoken one by one. <br>If the text in the tag contains special XML symbols, they need to be escaped, commonly including: <br>&amp;lt;<br>&amp;gt;<br>&amp;amp;<br>&amp;quot;<br>&amp;apos;<br>They represent `<`, `>`,`&`, `"`, and `'` respectively.
</td>
</tr>
<tr>
<td>……</td>
<td>Ellipsis</td>
</tr>
<tr>
<td>!"#$%&</td>
<td>Exclamation mark  double quotation mark  hash sign  dollar  percent sign  and</td>
</tr>
<tr>
<td>'()*+</td>
<td>Single quotation mark  left parenthesis  right parenthesis  asterisk  plus sign</td>
</tr>
<tr>
<td>,-./:;</td>
<td>Comma  hyphen  dot  slash  colon  semicolon</td>
</tr>
<tr>
<td><=>?@</td>
<td>Less-than sign  equal sign  greater-than sign  question mark  at</td>
</tr>
<tr>
<td>[\]^_</td>
<td>Left square bracket  backslash  right square bracket  caret  underscore</td>
</tr>
</table>
- date
 <table>
<tr>
<th>Format</th>
<th>Example</th>
<th>Output</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="6">xx year</td>
<td>71</td>
<td>Seventy-one</td>
<td rowspan="6">2- and 4-digit years are supported.<ul><li>2-digit years 60–99, 00–09, and 10–19 are supported.
<li>4-digit years 1000–1999 and 2000–2099 are supported.</ul>
</td>
</tr>
<tr>
<td>08</td>
<td>Oh eight</td>
</tr>
<tr>
<td>20</td>
<td>Twenty</td>
</tr>
<tr>
<td>2020</td>
<td>Twenty twenty</td>
</tr>
<tr>
<td>1998</td>
<td>Nineteen ninety-eight</td>
</tr>
<tr>
<td>2008</td>
<td>Two thousand and eight</td>
</tr>
<tr>
<td rowspan="4">xx year xx month</td>
<td>5/08</td>
<td>May oh eight</td>
<td rowspan="4">For January to September, the input month number can start either with or without a "0", such as 4/1908 and 04/1908.</td>
</tr>
<tr>
<td>04/2020</td>
<td>April twenty twenty</td>
</tr>
<tr>
<td>08/08</td>
<td>August oh eight</td>
</tr>
<tr>
<td>8/2020</td>
<td>August twenty twenty</td>
</tr>
<tr>
<td rowspan="4">xx year xx month xx day<br></td>
<td>4/23/98</td>
<td>April twenty-third ninety-eight</td>
<td rowspan="4">For the first to ninth day, the input day number can start either with or without a "0", such as "4/8/1908" and "04/08/1908".</td>
</tr>
<tr>
<td>08/23/2020</td>
<td>August twenty-third twenty twenty</td>
</tr>
<tr>
<td>8/8/2020</td>
<td>August eighth twenty</td>
</tr>
<tr>
<td>08/08/2020</td>
<td>August eighth twenty twenty</td>
</tr>
<tr>
<td rowspan="2">xx month xx day</td>
<td>8/20</td>
<td>August twentieth</td>
<td rowspan="2">None</td>
</tr>
<tr>
<td>08/08</td>
<td>August eighth</td>
</tr>
<tr>
<td rowspan="3">Numeric date (year and month)</td>
<td>2020/08</td>
<td>August twenty twenty</td>
<td rowspan="6">You can use "/", "-", or "_" to separate the numeric year, month, and day.</td>
</tr>
<tr>
<td>2020-08</td>
<td>August twenty twenty</td>
</tr>
<tr>
<td>2020.08</td>
<td>August twenty twenty</td>
</tr>
<tr>
<td rowspan="3">Numeric date (year, month, and day)</td>
<td>2020/08/09</td>
<td>August ninth twenty twenty</td>
</tr>
<tr>
<td>2020-8-9</td>
<td>August ninth twenty eighteen</td>
</tr>
<tr>
<td>2020.08.09</td>
<td>August ninth twenty eighteen</td>
</tr>
<tr>
<td rowspan="2">xx year xx month xx day~xx year xx month xx day<br></td>
<td>8/9~30/2020</td>
<td>August ninth to thirtieth twenty</td>
<td rowspan="8">You can use "~" and "-" to indicate a span of time.</td>
</tr>
<tr>
<td>08/09/2020-09/09/2020</td>
<td>August ninth twenty twenty to September ninth twenty twenty</td>
</tr>
<tr>
<td rowspan="2">xx month xx year~xx month xx year</td>
<td>04/20~04/21</td>
<td>April twenty to April twenty-one</td>
</tr>
<tr>
<td>04/2020~04/2021</td>
<td>April twenty twenty to April twenty twenty-one</td>
</tr>
<tr>
<td rowspan="2">xx month xx day~xx month xx day<br></td>
<td>10/1~10/7</td>
<td>October first to October seventh</td>
</tr>
<tr>
<td>10/01~10/07</td>
<td>October first to October seventh</td>
</tr>
<tr>
<td rowspan="2">xx month xx day~xx day<br></td>
<td>10/1~7</td>
<td>October first to seventh</td>
</tr>
<tr>
<td>10/01~07</td>
<td>October first to seventh</td>
</tr>
<tr>
<td rowspan="2">Numeric date (year, month, and day)~numeric date (year, month, and day)</td>
<td>2020/03/03~2021/03/03</td>
<td>March third twenty twenty to March third twenty twenty-one</td>
<td rowspan="5">You can use "/" or "." to separate the numeric year, month, and day and use "~" or "-" to indicate a span of time.</td>
</tr>
<tr>
<td>2020.9.9~2021.9.9</td>
<td>September ninth twenty twenty to September ninth twenty twenty-one</td>
</tr>
<tr>
<td>Numeric date (month and day)~numeric date (month and day)</td>
<td>10/20~10/31</td>
<td>October twentieth to October thirty-first</td>
</tr>
<tr>
<td rowspan="2">xx~xx month or xx month~xx month</td>
<td>1~10</td>
<td>January to October</td>
</tr>
<tr>
<td>1~10</td>
<td>January to October</td>
</tr>
<tr>
<td>>Numeric date (month, day, and year)</td>
<td>10/25/2020</td>
<td>October twenty-fifth twenty twenty</td>
<td>Only 4-digit years in the "MM/DD/YYYY" format are supported, and only "/" can be used to separate the day, month, and year.</td>
</tr>
</table>
- time
 <table>
<tr>
<th>Format</th>
<th>Example</th>
<th>Output</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="5">Time</td>
<td>12:00</td>
<td>Twelve o'clock</td>
<td rowspan="14">Common time and time range formats are supported.</td>
</tr>
<tr>
<td>12:00:00</td>
<td>Twelve o'clock</td>
</tr>
<tr>
<td>10:25</td>
<td>Ten twenty-five</td>
</tr>
<tr>
<td>10:25:30</td>
<td>Ten twenty-five thirty</td>
</tr>
<tr>
<td>09:25:14</td>
<td>Nine twenty-five fourteen</td>
</tr>
<tr>
<td rowspan="9">Time~time</td>
<td>11:00~12:00</td>
<td>Eleven to twelve o'clock</td>
</tr>
<tr>
<td>09:00-14:00</td>
<td>Nine o'clock to fourteen</td>
</tr>
<tr>
<td>11:00~11:30</td>
<td>Eleven o'clock to eleven thirty</td>
</tr>
<tr>
<td>11:00-15:18</td>
<td>Eleven o'clock to fifteen eighteen</td>
</tr>
<tr>
<td>10:30~11:00</td>
<td>Ten thirty to eleven o'clock</td>
</tr>
<tr>
<td>09:28-10:00</td>
<td>Nine twenty-eight to ten o'clock</td>
</tr>
<tr>
<td>10:20~11:20</td>
<td>Ten twenty to eleven twenty</td>
</tr>
<tr>
<td>06:00~08:00</td>
<td>Six to eight o'clock</td>
</tr>
<tr>
<td>10:20 am~1:30 pm</td>
<td>Ten twenty A M to one thirty P M</td>
</tr>
<tr>
<td rowspan="18">Numeric time</td>
<td>5:00am</td>
<td>Five o'clock in the early morning</td>
<td rowspan="18">If `am` is used, for 00:00–05:59, `am` is spoken as "in the early morning".<br>If `am` is used, for 06:00–11:59, `am` is spoken as "in the morning".<br>If `pm` is used, for 12:00–12:59, `pm` is spoken as "at noon".<br>If `pm` is used, for 01:00–05:59, `pm` is spoken as "in the afternoon"; for 06:00–11:59, `pm` is spoken as "at night".</td>
</tr>
<tr>
<td>5:30am</td>
<td>Five thirty in the early morning</td>
</tr>
<tr>
<td>5:20:12am</td>
<td>Five thirty twelve in the early morning</td>
</tr>
<tr>
<td>7:00am</td>
<td>Seven o'clock in the morning</td>
</tr>
<tr>
<td>7:30AM</td>
<td>Seven thirty in the morning</td>
</tr>
<tr>
<td>7:20:25a.m.</td>
<td>Seven twenty twenty-five in the morning</td>
</tr>
<tr>
<td>07:08:12A.M.</td>
<td>Seven eight twelve in the morning</td>
</tr>
<tr>
<td>5:00pm</td>
<td>Five o'clock in the afternoon</td>
</tr>
<tr>
<td>5:30PM</td>
<td>Five thirty in the afternoon</td>
</tr>
<tr>
<td>5:20:12p.m.</td>
<td>Five twenty twelve in the afternoon</td>
</tr>
<tr>
<td>05:09:12P.M</td>
<td>Five nine twelve in the afternoon</td>
</tr>
<tr>
<td>9:00pm</td>
<td>Nine o'clock at night</td>
</tr>
<tr>
<td>9:30pm</td>
<td>Nine thirty at night</td>
</tr>
<tr>
<td>9:20:12PM</td>
<td>Nine twenty twelve at night</td>
</tr>
<tr>
<td>9:02:12P.M.</td>
<td>Nine two twelve at night</td>
</tr>
<tr>
<td>12:00pm</td>
<td>Twelve o'clock at noon</td>
</tr>
<tr>
<td>12:30p.m.</td>
<td>Twelve thirty at noon</td>
</tr>
<tr>
<td>12:20:12PM</td>
<td>Twelve twenty twelve at noon</td>
</tr>
</table>
- currency
 <table>
<tr>
<th>Format</th>
<th>Example</th>
<th width="150px">Output</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="5">Number + currency</td>
<td>12.00USD</td>
<td>Twelve dollars</td>
<td rowspan="5">AUD (Australian dollar),  CAD (Canadian dollar), HKD (Hong Kong dollar), JPY (Japanese yen), USD (US dollar), CHF (Swiss franc), NOK (Norwegian krone), SEK (Swedish krona), GBP (Pound sterling), RMB (Renminbi), CNY (Chinese yuan), and EUR (euro) are supported.<br>The number can be an integer or decimal and can be separated by commas according to international standards.</td>
</tr>
<tr>
<td>12.50USD</td>
<td>Twelve dollars and fifty cents</td>
</tr>
<tr>
<td>15,000,000USD</td>
<td>Fifteen million dollars</td>
</tr>
<tr>
<td>15,000,000.00USD</td>
<td>Fifteen million dollars</td>
</tr>
<tr>
<td>12,000.35USD</td>
<td>Twelve thousand dollars and thirty-five cents</td>
</tr>
<tr>
<td rowspan="6">Concurrency + number</td>
<td>$12</td>
<td>Twelve dollars</td>
<td rowspan="6">$ (US dollar), fr (French franc), kr (Danish krone), £ (Pound sterling), ¥ (Chinese yuan), and € (Euro) are supported.<br>The number can be an integer or decimal and can be separated by commas according to international standards.</td>
</tr>
<tr>
<td>$12.00</td>
<td>Twelve dollars</td>
</tr>
<tr>
<td>$12.12</td>
<td>Twelve dollars and twelve cents</td>
</tr>
<tr>
<td>$12,000</td>
<td>Twelve thousand dollars</td>
</tr>
<tr>
<td>$12,000.00</td>
<td>Twelve thousand dollars</td>
</tr>
<tr>
<td>$12,000.99</td>
<td>Twelve thousand dollars and ninety-nine cents</td>
</tr>
<tr>
<td rowspan="8">Other default pronunciations</td>
<td>1213</td>
<td>One thousand two hundred and thirteen</td>
<td rowspan="8">None</td>
</tr>
<tr>
<td>1213KML</td>
<td>One thousand two hundred and thirteen K M L</td>
</tr>
<tr>
<td>1213.00KML</td>
<td>One thousand two hundred and thirteen K M L</td>
</tr>
<tr>
<td>1213.9KML</td>
<td>One hundred and twenty-one point three nine K M L</td>
</tr>
<tr>
<td>1,000KML</td>
<td>One thousand K M L</td>
</tr>
<tr>
<td>1,000.00KML</td>
<td>One thousand K M L</td>
</tr>
<tr>
<td>1,000.98KML</td>
<td>One thousand point nine eight K M L</td>
</tr>
<tr>
<td>12,000</td>
<td>Twelve thousand</td>
</tr>
</table>
- measure
 <table>
<tr>
<th>Format</th>
<th>Example</th>
<th>Output</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="7">Number + Chinese unit</td>
<td>2 sheets</td>
<td>Two sheets</td>
<td rowspan="21">Common Chinese units and unit abbreviations are supported.</td>
</tr>
<tr>
<td>120 hectares</td>
<td>One hundred twenty hectares</td>
</tr>
<tr>
<td>Over 100 milligrams</td>
<td>Over one hundred milligrams</td>
</tr>
<tr>
<td>Over 100 meters</td>
<td>Over one hundred meters</td>
</tr>
<tr>
<td>Over 100 people</td>
<td>Over one hundred people</td>
</tr>
<tr>
<td>1 centimeter 20 millimeters</td>
<td>One centimeter twenty millimeters</td>
</tr>
<tr>
<td>120.00 square kilometers</td>
<td>One hundred twenty square kilometers</td>
</tr>
<tr>
<td rowspan="3">Number + unit abbreviation</td>
<td>120.56cm²</td>
<td>One hundred and twenty point five six square centimeters</td>
</tr>
<tr>
<td>120m²56cm²</td>
<td>One hundred and twenty square meters fifty-six square centimeters</td>
</tr>
<tr>
<td>100m12cm6mm</td>
<td>One hundred meters twelve centimeters six millimeters</td>
</tr>
<tr>
<td rowspan="4">Range</td>
<td>10~15kg</td>
<td>Ten to fifteen kilograms</td>
</tr>
<tr>
<td>10.24~789.82 mu</td>
<td>Ten point two four to seven hundred and eighty-nine point eight two mu</td>
</tr>
<tr>
<td>10m~15m</td>
<td>Ten meters to fifteen meters</td>
</tr>
<tr>
<td>10.24cm~19.08cm</td>
<td>Ten point two four centimeters to nineteen point zero eight centimeters</td>
</tr>
<tr>
<td rowspan="3">Number + unit + "/" + unit</td>
<td>10 dollars/kilogram</td>
<td>Ten dollars per kilogram</td>
</tr>
<tr>
<td>199~299 dollars/piece</td>
<td>One hundred and ninety-nine to two hundred and ninety-nine dollars per piece</td>
</tr>
<tr>
<td>299.99 dollars/g~399.99 dollars/g</td>
<td>Two hundred and ninety-nine point nine nine dollars per gram to three hundred and ninety-nine point nine nine dollars per gram</td>
</tr>
<tr>
<td rowspan="4">Other default pronunciations</td>
<td>12 dozens</td>
<td>Twelve dozens</td>
</tr>
<tr>
<td>30rm</td>
<td>Thirty R M</td>
</tr>
<tr>
<td>400 million fellow citizens</td>
<td>Four hundred million fellow citizens</td>
</tr>
<tr>
<td>12.897 micrograms</td>
<td>Twelve point eight nine seven micrograms</td>
</tr>
</table>

#### Pronunciations of common &lt;say-as&gt; special symbols
<table>
<thead>
<tr>
<th>Special Symbol</th>
<th>Pronunciation</th>
</tr>
</thead>
<tbody><tr>
<td>!</td>
<td>Exclamation mark</td>
</tr>
<tr>
<td>"</td>
<td>Double quotation mark</td>
</tr>
<tr>
<td>#</td>
<td>Hash sign</td>
</tr>
<tr>
<td>$</td>
<td>Dollar</td>
</tr>
<tr>
<td>%</td>
<td>Percent sign</td>
</tr>
<tr>
<td>&amp;</td>
<td>and</td>
</tr>
<tr>
<td>'</td>
<td>Single quotation mark</td>
</tr>
<tr>
<td>(</td>
<td>Left parenthesis</td>
</tr>
<tr>
<td>)</td>
<td>Right parenthesis</td>
</tr>
<tr>
<td>*</td>
<td>Asterisk</td>
</tr>
<tr>
<td>+</td>
<td>Plus sign</td>
</tr>
<tr>
<td>,</td>
<td>Comma</td>
</tr>
<tr>
<td>-</td>
<td>Dash</td>
</tr>
<tr>
<td>.</td>
<td>Dot</td>
</tr>
<tr>
<td>/</td>
<td>Slash</td>
</tr>
<tr>
<td>:</td>
<td>Colon</td>
</tr>
<tr>
<td>;</td>
<td>Semicolon</td>
</tr>
<tr>
<td>&lt;</td>
<td>Less-than sign</td>
</tr>
<tr>
<td>=</td>
<td>Equal sign</td>
</tr>
<tr>
<td>&gt;</td>
<td>Greater-than sign</td>
</tr>
<tr>
<td>?</td>
<td>Quotation mark</td>
</tr>
<tr>
<td>@</td>
<td>at</td>
</tr>
<tr>
<td>[</td>
<td>Left square bracket</td>
</tr>
<tr>
<td>\</td>
<td>Backslash</td>
</tr>
<tr>
<td>]</td>
<td>Right square bracket</td>
</tr>
<tr>
<td>^</td>
<td>Caret</td>
</tr>
<tr>
<td>_</td>
<td>Underscore</td>
</tr>
<tr>
<td>`</td>
<td>Backtick</td>
</tr>
<tr>
<td>{</td>
<td>Left curly bracket</td>
</tr>
<tr>
<td></td>
<td></td>
</tr>
<tr>
<td>}</td>
<td>Right curly bracket</td>
</tr>
<tr>
<td>~</td>
<td>Tilde</td>
</tr>
<tr>
<td>！</td>
<td>Exclamation mark</td>
</tr>
<tr>
<td>“</td>
<td>Left double quotation mark</td>
</tr>
<tr>
<td>”</td>
<td>Right double quotation mark</td>
</tr>
<tr>
<td>‘</td>
<td>Left single quotation mark</td>
</tr>
<tr>
<td>’</td>
<td>Right single quotation mark</td>
</tr>
<tr>
<td>（</td>
<td>Left parenthesis</td>
</tr>
<tr>
<td>）</td>
<td>Right parenthesis</td>
</tr>
<tr>
<td>，</td>
<td>Comma</td>
</tr>
<tr>
<td>。</td>
<td>Period</td>
</tr>
<tr>
<td>—</td>
<td>Dash</td>
</tr>
<tr>
<td>：</td>
<td>Colon</td>
</tr>
<tr>
<td>；</td>
<td>Semicolon</td>
</tr>
<tr>
<td>？</td>
<td>Quotation mark</td>
</tr>
<tr>
<td>、</td>
<td>Enumeration comma</td>
</tr>
<tr>
<td>...</td>
<td>Ellipsis</td>
</tr>
<tr>
<td>……</td>
<td>Ellipsis</td>
</tr>
<tr>
<td>《</td>
<td>Left title mark</td>
</tr>
<tr>
<td>》</td>
<td>Right title mark</td>
</tr>
<tr>
<td>￥</td>
<td>Chinese yuan sign</td>
</tr>
<tr>
<td>≥</td>
<td>Greater-than-or-equal-to sign</td>
</tr>
<tr>
<td>≤</td>
<td>Less-than-or-equal-to sign</td>
</tr>
<tr>
<td>≠</td>
<td>Not-equal sign</td>
</tr>
<tr>
<td>≈</td>
<td>Approximately-equal-to sign</td>
</tr>
<tr>
<td>±</td>
<td>Plus-minus sign</td>
</tr>
<tr>
<td>×</td>
<td>Multiplication sign</td>
</tr>
<tr>
<td>π</td>
<td>Pi</td>
</tr>
<tr>
<td>Α</td>
<td>Alpha</td>
</tr>
<tr>
<td>Β</td>
<td>Beta</td>
</tr>
<tr>
<td>Γ</td>
<td>Gamma</td>
</tr>
<tr>
<td>Δ</td>
<td>Delta</td>
</tr>
<tr>
<td>Ε</td>
<td>Epsilon</td>
</tr>
<tr>
<td>Ζ</td>
<td>Zeta</td>
</tr>
<tr>
<td>Ε</td>
<td>Eta</td>
</tr>
<tr>
<td>Θ</td>
<td>Theta</td>
</tr>
<tr>
<td>Ι</td>
<td>Iota</td>
</tr>
<tr>
<td>Κ</td>
<td>Kappa</td>
</tr>
<tr>
<td>∧</td>
<td>Lambda</td>
</tr>
<tr>
<td>Μ</td>
<td>Mu</td>
</tr>
<tr>
<td>Ν</td>
<td>Nu</td>
</tr>
<tr>
<td>Ξ</td>
<td>Xi</td>
</tr>
<tr>
<td>Ο</td>
<td>Omicron</td>
</tr>
<tr>
<td>∏</td>
<td>Pi</td>
</tr>
<tr>
<td>Ρ</td>
<td>Rho</td>
</tr>
<tr>
<td>∑</td>
<td>Sigma</td>
</tr>
<tr>
<td>Τ</td>
<td>Tau</td>
</tr>
<tr>
<td>Υ</td>
<td>Upsilon</td>
</tr>
<tr>
<td>Φ</td>
<td>Phi</td>
</tr>
<tr>
<td>Χ</td>
<td>Chi</td>
</tr>
<tr>
<td>Ψ</td>
<td>Psi</td>
</tr>
<tr>
<td>Ω</td>
<td>Omega</td>
</tr>
<tr>
<td>α</td>
<td>Alpha</td>
</tr>
<tr>
<td>β</td>
<td>Beta</td>
</tr>
<tr>
<td>γ</td>
<td>Gamma</td>
</tr>
<tr>
<td>δ</td>
<td>Delta</td>
</tr>
<tr>
<td>ε</td>
<td>Epsilon</td>
</tr>
<tr>
<td>ζ</td>
<td>Zeta</td>
</tr>
<tr>
<td>η</td>
<td>Eta</td>
</tr>
<tr>
<td>θ</td>
<td>Theta</td>
</tr>
<tr>
<td>ι</td>
<td>Iota</td>
</tr>
<tr>
<td>κ</td>
<td>Kappa</td>
</tr>
<tr>
<td>λ</td>
<td>Lambda</td>
</tr>
<tr>
<td>μ</td>
<td>Mu</td>
</tr>
<tr>
<td>ν</td>
<td>Nu</td>
</tr>
<tr>
<td>ξ</td>
<td>Xi</td>
</tr>
<tr>
<td>ο</td>
<td>Omicron</td>
</tr>
<tr>
<td>π</td>
<td>Pi</td>
</tr>
<tr>
<td>ρ</td>
<td>Rho</td>
</tr>
<tr>
<td>σ</td>
<td>Sigma</td>
</tr>
<tr>
<td>τ</td>
<td>Tau</td>
</tr>
<tr>
<td>υ</td>
<td>Upsilon</td>
</tr>
<tr>
<td>φ</td>
<td>Phi</td>
</tr>
<tr>
<td>χ</td>
<td>Chi</td>
</tr>
<tr>
<td>ψ</td>
<td>Psi</td>
</tr>
<tr>
<td>ω</td>
<td>Omega</td>
</tr>
</tbody></table>

#### Common &lt;say-as&gt; units
<table>
<tr>
<th>Format</th>
<th>Type</th>
<th>Example</th>
</tr>
<tr>
<td rowspan="9">Abbreviation</td>
<td>Length</td>
<td>nm (nanometer), μm (micrometer), mm (millimeter), cm (centimeter), m (meter), km (kilometer), ft (foot), in (inch)</td>
</tr>
<tr>
<td>Area</td>
<td>cm² (square centimeter), m² (square meter), km² (square kilometer), SqFt (square foot)</td>
</tr>
<tr>
<td>Volume</td>
<td>cm³ (cubic centimeter), m³ (cubic meter), km³ (cubic kilometer), mL (milliliter), L (liter), gal (gallon)</td>
</tr>
<tr>
<td>Mass</td>
<td>μg (microgram), mg (milligram), g (gram), kg (kilogram)</td>
</tr>
<tr>
<td>Time</td>
<td>min (minute), sec (second), ms (millisecond)</td>
</tr>
<tr>
<td>Electromagnetism</td>
<td>μA (microampere), mA (milliampere), Ω (ohm), Hz (hertz), KHz (kilohertz), MHz (megahertz), GHz (gigahertz), V (volt), kV (kilovolt), kWh (kilowatt-hour)</td>
</tr>
<tr>
<td>Sound</td>
<td>dB (decibel)</td>
</tr>
<tr>
<td>Atmospheric pressure</td>
<td>Pa (pascal), kPa (kilopascal), Mpa (megapascal)</td>
</tr>
<tr>
<td>Chinese unit</td>
<td>This type includes without limitation the Chinese units of the aforementioned units, such as "meter", "second", "dollar", and "milliliter per bottle".</td>
</tr>
</table>

#### Tag relationships
The `<say-as>` tag can contain text only.

#### Sample
- cardinal
```
<speak>
 <say-as interpret-as="cardinal">12345</say-as>
</speak>
```
Output speech audio: [say-as-cardinal.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/say-as-cardinal.wav)
- digits
```
<speak>
<say-as interpret-as="digits">12345</say-as>
</speak>
```
Output speech audio: [say-as-digits.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/say-as-digits.wav)
- telephone
```
<speak>
  <say-as interpret-as="telephone">12345</say-as>
</speak>
```
Output speech audio: [say-as-telephone.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/say-as-telephone.wav)
- name
```
<speak>
  Her former name is <say-as interpret-as="name">Zeng Xiaofan</say-as>.
</speak>
```
Output speech audio: [say-as-name.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/say-as-name.wav)
- address
```
<speak>
  <say-as interpret-as="address">304, Unit 3, Building 1, No. 10,000, Shennan Boulevard</say-as>
</speak>
```
Output speech audio: [say-as-address.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/say-as-address.wav)
- id
```
<speak>
  My username is <say-as interpret-as="id">tencent_8858</say-as>
</speak>
```
Output speech audio: [say-as-id.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/say-as-id.wav)
- characters
```
<speak>
  Greek letters <say-as interpret-as="characters">αβ</say-as>
</speak>
```
Output speech audio: [say-as-characters.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/say-as-characters.wav)
- punctuation
```
<speak>
  The punctuation mark that I use the most frequently is <say-as interpret-as="punctuation">,</say-as>
</speak>
```
Output speech audio: [say-as-punctuation.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/say-as-punctuation.wav)
- date
```
<speak>
  <say-as interpret-as="date">2020-10-10</say-as>
</speak>
```
Output speech audio: [say-as-date.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/say-as-date.wav)
- time
```
<speak>
  <say-as interpret-as="time">5:30am</say-as>
</speak>
```
Output speech audio: [SSML-say-as_time.mp3](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/say-as-time.wav)
- currency
```
<speak>
  <say-as interpret-as="currency">15,000.00RMB</say-as>
</speak>
```
Output speech audio: [say-as-currency.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/say-as-currency.wav)
- measure
```
<speak>
  <say-as interpret-as="measure">100m²15cm²</say-as>
</speak>
```
Output speech audio: [say-as-measure.wav](https://ssml-demo-1300466766.cos.ap-guangzhou.myqcloud.com/say-as-measure.wav)

