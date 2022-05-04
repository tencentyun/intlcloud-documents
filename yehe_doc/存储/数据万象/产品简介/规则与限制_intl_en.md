<table>
   <tr>
      <th>Category</td>
      <th>Feature</td>
      <th>Specifications/Limit</td>
   </tr>
   <tr>
      <td rowspan="5">Basic image processing</td>
      <td>Common limits</td>
      <td><li>Supported format: JPG, BMP, GIF, PNG, WebP, as well as HEIF decoding and processing <li>Supported size: The input image cannot exceed 20 MB, with its width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 250 million. The width and height of an output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million. <li>Maximum number of frames (for GIF): 300</td>
   </tr>
   <tr>
      <td> <a href="https://intl.cloud.tencent.com/document/product/1045/33716">Format Conversion</a></td>
      <td>Supports JPG, BMP, GIF, PNG, WebP (default value: format of the input image). Converting GIF into HEIF is not supported.</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33717">Quality Conversion</a></td>
      <td>Supports JPG and WebP only.</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33716">Progressive Display</a></td>
      <td>Supports JPG only. If the format of the output image is not JPG, this parameter will be ignored.</td>
   </tr>
   <tr>
      <td><a href="https://intl.cloud.tencent.com/document/product/1045/33727">Pipeline Operator</a></td>
      <td>Performs multiple operations on an image in sequence. Currently, up to 10 layers of pipelines are supported.</td>
   </tr>
   <tr>
      <td rowspan="3">Advanced features</td>
      <td>Guetzli Image Compression</a></td>
      <td>Supports only JPG images whose quality is larger than 70 and the total number of pixels is smaller than 4 million.</td>
   </tr>
   <tr>
      <td>Image Advanced Compression</a></td>
      <td><li>Format: supports converting JPG, PNG, GIF, WebP, and other formats into TPG or HEIF. <li>Size: The input image cannot exceed 20 MB, with its width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 250 million. The width and height of an output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million. <li>Maximum number of frames (for GIF): 300</td>
   </tr>
   <tr>
      <td>Blind watermarking</a></td>
      <td><li>Adding blind watermark to animated images such as GIF is not supported.<li>Width or height of the image watermark cannot be larger than 1/8 of the input image.<li>A text watermark can contain only numbers (0−9) and English letters (A−Z, a−z).</td>
   </tr>
   <tr>
      <td>Media processing</td>
      <td>Video Processing</a></td>
      <td>Supports AVI, MP4, MKV, FLV, HLS, TS, MP3, AAC, FLAC, and more.</td>
   </tr>
   <tr>
      <td rowspan="4">Content moderation</td>
      <td>Image Moderation</a></td>
      <td>Supports PNG, JPEG, JPG, BMP, WebP, and GIF. An image cannot be larger than 10 MB. To ensure recognition accuracy, the image resolution should not be lower than 256x256.</td>
   </tr>
   <tr>
      <td>Video Moderation</a></td>
      <td>Supports MP4, AVI, MKV, WMV, RMVB, FLV, and M3U8. A video cannot be larger than 5 GB and the number of frames cannot be more than 100 thousand.</td>
   </tr>
   <tr>
      <td>Audio Moderation</a></td>
      <td><li>Supports MP3, WAV, AAC, FLAC, AMR, 3GP, M4A, WMA, OGG, and APE. <li>Audio bitrate: 128−256 kbps <li>Audio size: smaller than 600 MB <li>Maximum duration: 3 hours</td>
   </tr>
   <tr>
      <td>Text Moderation</a></td>
      <td>Supports TXT files not larger than 1 MB only.</td>
   </tr>
   <tr>
      <td rowspan="5">Content recognition</td>
      <td>QR Code Recognition</a>、Image Label Recognition</a></td>
      <td>Supports PNG, JPEG, and JPG. An image cannot be larger than 3 MB and the resolution should be higher than 50x50.</td>
   </tr>
   <tr>
      <td>Speech Recognition</a></td>
      <td><li>Supports Mandarin, English, and Cantonese.<li>Supported format: WAV, MP3, M4A<li>An audio file cannot be longer than 5 hours or larger than 512 MB.</td>
   </tr>
   <tr>
      <td>Face Filter</a></td>
      <td>A Base64-encoded image cannot be larger than 5 MB. PNG, JPG, JPEG, and BMP are supported, while GIF is not supported. To use portrait segmentation, the image resolution must be lower than 2000×2000.</td>
   </tr>
   <tr>
      <td>ID Card Recognition</a></td>
      <td>A Base64-encoded image cannot be larger than 7 MB, and a resolution higher than 500×800 is recommended. Supported formats are PNG, JPG, JPEG, and BMP. It is recommended that the ID card should occupy over 2/3 of the image.</td>
   </tr>
   <tr>
      <td>Face ID</a></td>
      <td>The Base64-encoded video cannot be larger than 8 MB. Supported formats are MP4, AVI, and FLV.</td>
   </tr>
   <tr>
      <td rowspan="2">File preview</td>
      <td>File Preview</a></td>
      <td>1. Supported format:<li>Presentation file: PPTX, PPT, POT, POTX, PPS, PPSX, DPS, DPT, PPTM, POTM, PPSM<li>Text file: DOC, DOT, WPS, WPT, DOCX, DOTX, DOCM, DOTM <li>Form file: XLS, XLT, ET, ETT, XLSX, XLTX, CSV, XLSB, XLSM, XLTM, ETS <li>Other file: PDF,  LRC, C, CPP, H, ASM, S, Java, ASP, BAT, BAS, PRG, CMD, RTF, TXT, LOG, XML, HTM, HTML <br>2. Supports previewing files within 200 MB with no more than 5,000 pages.</td>
   </tr>
   <tr>
      <td>Privacy Compliance Protection</a></td>
      <td>Supported format: <li>MS office file: DOC, DOCX, PPT, PPTX, XLS, XLSX, RTF<li>WPS file: WPS, DPS, ET<li>PDF<li>Plain text file: TXT, XML, SLK <li>HTML, MSG<li>Email: EML, PST</td>
   </tr>
</table>
