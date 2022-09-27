
## Display Mode

Enable different display modes by initializing the configuration option class:
```plaintext
var demo = COSDocPreviewSDK.config({
    mode: 'normal', 
})
```

The configuration options are as described below:

| `mode` Value        | Description                  | Default Option                                                         | 
| ----------- | ------------------------------------------------------------ | -------------- | 
| normal | Normal mode, with all functional UIs shown | Yes | 
| simple | Simple mode, with no header and toolbar shown | No | 
 
## Custom Configuration Options

When initializing the JS-SDK, by configuring different options for different types of files, you can enable or disable specific configurations in a file and control its status when it is opened.
```plaintext
COSDocPreviewSDK.config({
    // Common option, which is applicable to all types of files.
    commonOptions: {
      isShowTopArea: false, // Hide the top area (header and toolbar).
      isShowHeader: false // Hide the header area.

    },
    // Word file configurations.
    wordOptions: {
      isShowDocMap: false,
      isBestScale: true
    },
    // PDF file configurations.
    pdfOptions: {
      isShowComment: true,
      isInSafeMode: false
    },
    // Presentation file configurations.
    pptOptions: {
      isShowBottomStatusBar: true
    }
})
```

- Common configuration items: `commonOptions`
<table>
	<tr><th>Configuration Item</th><th>Description</th><th>Default Value</th></tr>
	<tr><td>isShowTopArea</td><td>Whether to show the top area (header and toolbar)</td><td>false</td></tr>
	<tr><td>isShowHeader</td><td>Whether to show the header area</td><td>false</td></tr>
	<tr><td>isBrowserViewFullscreen</td><td>Whether to enable full screen mode in the browser area</td><td>false</td></tr>
	<tr><td>isIframeViewFullscreen</td><td>Whether to enable full screen mode in the iframe area</td><td>false</td></tr>
</table>
- Text file configuration items: `wordOptions`
<table>
	<tr><th>Configuration Item</th><th>Description</th><th>Default Value</th></tr>
	<tr><td>isShowDocMap</td><td>Whether to enable the directory feature, which is enabled by default.</td><td>true</td></tr>
	<tr><td>isBestScale</td><td>Whether to display the file at the best scale by default (for PC) when the file is opened</td><td>true</td></tr>
	<tr><td>isShowBottomStatusBar</td><td>Whether to show the bottom status bar (for PC)</td><td>false</td></tr>
</table>
- PDF file configuration items: `pdfOptions`
<table>
	<tr><th>Configuration Item</th><th>Description</th><th>Default Value</th></tr>
	<tr><td>isShowComment</td><td>Whether to show annotations, which are shown by default.</td><td>true</td></tr>
	<tr><td>isInSafeMode</td><td>Whether to enable the safe mode (text cannot be selected or copied and links cannot be opened). It is disabled by default.</td><td>false</td></tr>
	<tr><td>isShowBottomStatusBar</td><td>Whether to show the bottom status bar (for PC)</td><td>false</td></tr>
</table>
- Presentation file configuration items: `pptOptions`
<table>
	<tr><th>Configuration Item</th><th>Description</th><th>Default Value</th></tr>
	<tr><td>isShowBottomStatusBar</td><td>Whether to show the bottom status bar (for PC)</td><td>false</td></tr>
</table>


## Component Status Settings

Page components can be hidden or disabled through the `commandBars` option.

```plaintext
COSDocPreviewSDK.config({
    // Common option, which is applicable to all types of files.
    commandBars: [
      {
        cmbId: 'Print', // Component ID
        attributes: {
          visible: false, // Whether to show the component. Valid values: `false` (no), `true` (yes). Default value: `true`.
          enable: false, // Whether to enable the component. Default value: `true`.
        },
      },
    ]
})
```

The list of currently available components is as follows:

<table>
	<tr><th>Component ID</th><th>Description</th><th>Scope of Application</th></tr>
	<tr><td>Print</td><td>Print feature and the Ctrl + P shortcut for print</td><td>All files</td></tr>
	<tr><td>MobileHeader</td><td>Top toolbar in the client</td><td>All files</td></tr>
	<tr><td>WriterHoverToolbars</td><td>Bottom toolbar in the client</td><td>Word files</td></tr>
	<tr><td>DownloadImg</td><td>Download icon when the image is double-clicked</td><td>Presentation files</td></tr>
	<tr><td>PlayComponentToolbar</td><td>Toolbar in the top-right corner when in full screen mode</td><td>Presentation files</td></tr>
	<tr><td>PlayContextCheckImage</td><td>Right click during playback - View original image</td><td>Presentation files</td></tr>
	<tr><td>FloatMenuCheckImage</td><td>Floating menu bar when the image is selected - View original image</td><td>Presentation files</td></tr>
	<tr><td>WPPMobileCommentButton</td><td>Comment button on the bottom toolbar in the client</td><td>Presentation files</td></tr>
	<tr><td>PDFMobilePageBar</td><td>Page number in the client</td><td>PDF files</td></tr>
</table>