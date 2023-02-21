
The JS-SDK provides advanced features to directly manipulate files. Below is the call process of advanced features:

## 1. Wait for a file to be loaded

```plaintext
await demo.ready() // You can call an advanced API only after the demo is ready. The demo object is the object after the JS-SDK is instantiated.
```

## 2. Get the file object

```plaintext
// Text
const wordApp = demo.WordApplication()
// Spreadsheet
const excelApp = demo.ExcelApplication()
// Presentation
const pptApp = demo.PPTApplication()
// PDF
const pdfApp = demo.PDFApplication()

// Automatic recognition
const app = demo.Application
```

## 3. Use advanced features

Below is the sample code of using advanced features on text, spreadsheet, presentation, and PDF files. For the specific formats supported for each file type, see [Specifications and Limits](https://intl.cloud.tencent.com/document/product/1045/33425).

### Text file

<dx-accordion>
::: Get the total number of pages
```plaintext
  /*
  * @param: WdInformation: {
  *      wdNumberOfPagesInDocument: 4
  *  }
  * @return: {PagesCount: number, End: boolean}
  */
  const app = demo.WordApplication()
  const {Enum} = app
  let totalPages = await app.ActiveDocument.Range.Information(Enum.WdInformation.wdNumberOfPagesInDocument)
  if (totalPages.End) {
    // Getting the total number of pages is an async operation. The obtained number of pages is accurate only after `totalPages.End` becomes `true`.
    console.log("All pages are loaded. There are ", totalPages.PagesCount, " pages in total.")
  }
```
:::
::: Get the current page
```plaintext
  /*
  * @param: WdInformation: {
  *      wdActiveEndPageNumber: 3
  *  }
  * @return: number
  */
  const app = demo.WordApplication()
  const {Enum} = app
  let currentPage = await app.ActiveDocument.Selection.Information(Enum.WdInformation.wdActiveEndPageNumber)
```
:::
::: Go to the specified page
```plaintext
  /*
  * @param: { What?: WdGoToItem, Which?: WdGoToDirection.wdGoToAbsolute, Count?: number, Name?: string}
  * WdGoToItem: {
  *      wdGoToPage: 1,
  *  }
  *  WdGoToDirection: {
  *      wdGoToAbsolute: 1
  *  }
  * @return: number Return the target page number
  */
  const app = demo.WordApplication()
  const {Enum} = app
  const page = await app.ActiveDocument.Selection.GoTo(Enum.WdGoToItem.wdGoToPage, Enum.WdGoToDirection.wdGoToAbsolute, 10)
  // Or
  const page = await app.ActiveDocument.Selection.GoTo({
    What: Enum.WdGoToItem.wdGoToPage,
    Which: Enum.WdGoToDirection.wdGoToAbsolute,
    Count: 10
  })
```
:::
::: Set whether to show comments
```plaintext
  /*
  * @param: bool
  * Valid values: `true` (yes); `false` (no).
  */

  // Hide comments.
  demo.WordApplication().ActiveDocument.ActiveWindow.View.ShowComments = false
```
:::
::: Set whether to show the table of contents
```plaintext
  /*
  * @param: bool
  * Valid values: `true` (yes); `false` (no).
  */

  // Hide the table of contents.
  demo.WordApplication().ActiveDocument.ActiveWindow.DocumentMap = false
```
:::
::: Zoom the view
```plaintext
  /*
  * @return: number
  */
  await demo.WordApplication().ActiveDocument.ActiveWindow.View.Zoom.Percentage  // Read the view zoom level.

  /*
  * @param : 50 <= number <= 300 (The zoom level is between 50% and 300%.)
  */
  demo.WordApplication().ActiveDocument.ActiveWindow.View.Zoom.Percentage = 100  // Set the view zoom level.
```
:::
</dx-accordion>

### Spreadsheet file

<dx-accordion>
::: Get the names of all sheets
```plaintext
const app = demo.ExcelApplication()
const Names = []
const count = await app.Sheets.Count;
for(let index = 1; index <= count; index++) {
  Names.push(await app.Sheets.Item(index).Name);
}
console.log(Names)
```
:::
::: Get the name of the current sheet
```plaintext
const app = demo.ExcelApplication()
const name = await app.ActiveSheet.Name
```
:::
::: Switch to the specified sheet
```plaintext
const app = demo.ExcelApplication()
const sheetIndex = 1 // Sheet number, which starts from 1.
app.Sheets.Item(sheetIndex).Activate() // Switch the sheet.
```
:::
::: Zoom the view
```plaintext
  /*
  * @return: number
  */
  await demo.ExcelApplication().ActiveWorkbook.ActiveSheetView.Zoom	// Read the view zoom level.
  /*
  * @param : 10 <= number <= 500 (The zoom level is between 10% and 500%.)
  */
  demo.ExcelApplication().ActiveWorkbook.ActiveSheetView.Zoom = 100	// Set the view zoom level.
```
:::
</dx-accordion>

### Presentation file

<dx-accordion>
::: Get the total number of pages
```plaintext
  /*
  * @return: number
  */
  let totalPages = await demo.PPTApplication().ActivePresentation.Slides.Count
```
:::
::: Get the current page
```plaintext
  /*
  * @return: number
  */
  let totalPages = await demo.PPTApplication().ActivePresentation.SlideShowWindow.View.Slide.SlideIndex
```
:::
::: Go to the specified page
```plaintext
  /*
  * @param: number
  */
  await demo.PPTApplication().ActivePresentation.SlideShowWindow.View.GotoSlide(3)	// Go to page 3.
```
:::
::: Start a slide show
```plaintext
await demo.PPTApplication().ActivePresentation.SlideShowSettings.Run()
```
:::
::: Exit the slide show
```plaintext
await demo.PPTApplication().ActivePresentation.SlideShowWindow.View.Exit()
```
:::
::: Play the next animation
```plaintext
  await demo.PPTApplication().ActivePresentation.SlideShowWindow.View.GotoNextClick()
```
:::
::: Play the previous animation
```plaintext
  await demo.PPTApplication().ActivePresentation.SlideShowWindow.View.GotoPreClick()
```
:::
::: Get the play status
```plaintext
  /*
  * @return: string ('preview' | 'play')
  */
  let currentState = await demo.PPTApplication().ActivePresentation.SlideShowWindow.View.State
```
:::
::: Zoom the view
```plaintext
  /*
  * @return: number
  */
  await demo.PPTApplication().ActivePresentation.View.Zoom	// Read the view zoom level.
  /*
  * @param : 1 <= number <= 400 (The zoom level is between 1% and 400%.)
  */
  demo.PPTApplication().ActivePresentation.View.Zoom = 100	// Set the view zoom level (non-play mode).
```
:::
</dx-accordion>

### PDF file

<dx-accordion>
::: Get the total number of pages
```plaintext
  /*
  * @return: number
  */
  let totalPages = await demo.PDFApplication().ActivePDF.PagesCount
```
:::
::: Get the current page
```plaintext
  /*
  * @return: number
  */
  let totalPages = await demo.PDFApplication().ActivePDF.CurrentPage
```
:::
::: Go to the specified page
```plaintext
  /*
  * @param : { PageNum: number }
  */
  let PageNum = 10
  await demo.PDFApplication().ActivePDF.JumpToPage({PageNum})
```
:::
::: Set the page rendering mode
```plaintext
  /*
  * 1: Single-page mode
  * 0: Multi-page mode
  */

  demo.PDFApplication().ActivePDF.PageMode = 1	  // Set the single-page mode.
```
:::
::: Set whether to show the table of contents
```plaintext
  /*
  * true: Show the table of contents
  * false: Hide the table of contents
  */
  demo.PDFApplication().ActivePDF.DocumentMap = true	// Show the table of contents.
```
:::
::: Zoom the view
```plaintext
  /*
  * @return: number
  */
  await demo.PDFApplication().ActivePDF.Zoom  // Read the view zoom level.
  /*
  * @param : 1 <= number <= 400 (The zoom level is between 1% and 400%.)
  */
  demo.PDFApplication().ActivePDF.Zoom = 100  // Set the view zoom level.
```
:::
::: Listen on events
You can use the `on` method of the instance to listen on events.

```plaintext
demo.on('Event name', function(data) {
    // do something...
})
```

| Event     | Description                                                         |
| ---------- | ------------------------------------------------------------ |
| fileOpen   | The file was opened successfully or failed to be opened.                             |
| error      | An error occurred, and an error code was returned.                           |
| fileStatus | The file was saved, and a `status` value was returned. Valid values: `0` (the file had no updates); `1` (the version was saved successfully); `2` (the file was empty and couldn't be saved); `3` (the space was full); `4` (the file was being saved); `5` (the file failed to be saved); `6` (the file updates were being saved; this status will be triggered when the file content is modified); `7` (the change to the file content was saved successfully). |


:::
</dx-accordion>

