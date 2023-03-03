1. MPS provides preset moderation templates, which can be added directly to a scheme. You can also click **Create template** to customize your own moderation templates.

	- Template name: Up to 64 characters; supports Chinese characters, letters, digits, spaces, underscores (_), hyphens (-), and periods (.).
	- Moderation items: Image recognition, speech recognition, and text recognition. The subitems of the selected moderation items will appear in the column on the right.

<table border=0 cellpadding="0" cellspacing="0">
<thead>
<tr>
<th >Moderation Item</th>
<th nowrap="nowrap">Subitem</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td rowspan = 3 nowrap="nowrap">Image recognition</td>
<td>Pornographic content</td>
<td>Porn, vulgarity, intimacy, and sexiness</td>
</tr>
<tr>
<td>Terrorist content</td>
<td>Bloody scenes, explosions, and fires</td>
</tr>
<tr>
<td>Politically sensitive content</td>
<td>Banned icons, and celebrities in sports and the entertainment industry</td>
</tr>
<tr>
<td rowspan = 2>Speech recognition</td>
<td>Pornographic content</td>
<td align="center">Porn, vulgarity, intimacy, and sexiness</td>
</tr>
<tr>
<td>Politically sensitive content</td>
<td>Banned icons, and celebrities in sports and the entertainment industry</td>
</tr>
<tr>
<td rowspan = 2>Text recognition</td>
<td>Pornographic content</td>
<td align="center">Porn, vulgarity, intimacy, and sexiness</td>
</tr>
<tr>
<td>Politically sensitive content</td>
<td>Banned icons, and celebrities in sports and the entertainment industry</td>
</tr>
</tbody></table>

2. For each subitem, you can set a **Confirm Threshold** and a **Suspicion Threshold**, which determine the strictness of moderation. If they are left empty, the default values will be used.
 - **Confirm threshold**: MPS analyzes the videos uploaded and gives them confirmation scores. If the score of a video exceeds the confirm threshold, the video will be marked confirmed. The value range of the threshold is 0-100. The default value is recommended.
 - **Suspicion threshold**: MPS analyzes the videos uploaded and gives them suspicion scores. If the score of a video exceeds the suspicion threshold, the video will be marked suspicious. You can initiate human moderation for suspicious videos on the video moderation page. The value range of the threshold is 0-100. The default value is recommended.
>? You can view **preset** moderation templates in [Template Management > Moderation](https://console.intl.cloud.tencent.com/mps/templates/audits) of the MPS console.

3. The templates created are displayed in the moderation template list, where you can view the details of, edit, or delete a template.
