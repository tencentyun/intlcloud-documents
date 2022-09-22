## Feature Description

Based on Tencent Cloud's industry-leading deep learning technology, the optical character recognition (OCR) feature is capable of intelligently recognizing words on images and converting them into editable text. It can be used in photo scanning, paper document digitization, ecommerce ad moderation, and many other scenarios to greatly improve the efficiency of information processing.

This API adopts the sync GET request method.

## Billing Description

- Calling the API successfully will incur OCR fees and COS read request fees as described in [Content Recognition Fees]() and [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100) respectively.
- If the image files are stored in COS STANDARD_IA storage class, calling the API successfully will incur [STANDARD_IA data retrieval fees](https://intl.cloud.tencent.com/document/product/436/40097).
- Image processing is not supported for objects stored in the ARCHIVE or DEEP ARCHIVE storage classes. To process these objects, you need to restore them first as instructed in [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633).

## Restrictions

- Supported image formats: PNG, JPG, JPEG, BMP, PDF.
- Image size: The downloaded file **cannot exceed 7 MB** in size after being Base64-encoded.
- Image resolution: A resolution above **600\*800 px** is recommended; otherwise, the recognition effect may be affected.
- Calling the API requires a signature. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/1045/33452).

## Request

#### Sample request

```plaintext
GET /<ObjectKey>?ci-process=OCR&type=general&language-type=zh&ispdf=true&pdf-pagenumber=1&isword=false&enable-word-polygon=false HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 


#### Request parameters

| Parameter | Description | Type | Required |
| :------------------ | :----------------------------------------------------------- | :------ | :------- |
| ObjectKey | Object name, such as `folder/document.jpg`. | String  | Yes |
| ci-process | CI's processing capability, which is fixed at `OCR` for OCR. | String | Yes |
| type | OCR recognition type. Valid values: `general` (general print recognition), `accurate` (high-precision print recognition), `efficient` (simplified print recognition), `fast` (high-speed print recognition), `handwriting` (handwriting recognition). Default value: `general`. | String | No |
| language-type | Language type. This parameter takes effect only if `type` is `general`. The language can be automatically recognized or manually specified. Chinese-English mix (`zh`) is selected by default. Mixed characters in English and each supported language can be recognized together. For valid values, see [Recognizable language types](#language-type). | String | No |
| ispdf               | Whether to enable PDF recognition. This parameter takes effect only if `type` is `general` or `fast`. Valid values: `true`, `false`. Default value: `false`. After this feature is enabled, images and PDF files can be recognized at the same time.   | Boolean | No       |
| pdf-pagenumber      | Page number of the PDF page to be recognized. This parameter takes effect only if `type` is `general` or `fast`, the uploaded file is a PDF, and `ispdf` is `true`. Only one single PDF page can be recognized. Default value: 1. | Integer | No       |
| isword | Whether to return the word information after recognition. This parameter takes effect only if `type` is `general` or `accurate`. Valid values: `true`, `false`. Default value: `false`. | Boolean | No |
| enable-word-polygon | Whether to output four-point word coordinates. This parameter takes effect only if `type` is `handwriting`. Valid values: `true`, `false`. Default value: `false`. | Boolean | No |

<span id="language-type"></span>

#### Recognizable language types

| Value | Language | Value | Language |
| ------- | ---------------------------------------------- | ---- | -------- |
| zh | Chinese-English mix | rus | Russian |
| zh_rare | English, digits, rare Chinese characters, traditional Chinese characters, special symbols | ita | Italian |
| auto | Automatic | hol | Dutch |
| mix | Multi-language | swe | Swedish |
| jap | Japanese | fin | Finnish |
| kor | Korean | dan | Danish |
| spa | Spanish | nor | Norwegian |
| fre | French | hun | Hungarian |
| ger | German | tha | Thai |
| por | Portuguese | hi | Hindi |
| vie | Vietnamese | ara | Arabic |
| may | Malay | | |

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/49351).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49352).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
  <TextDetections>
    <DetectedText></DetectedText>
    <Confidence></Confidence>
    <Polygon>
      <X></X>
      <Y></Y>
    </Polygon>
    <ItemPolygon>
      <X></X>
      <Y></Y>
      <Width></Width>
      <Height></Height>
    </ItemPolygon>
    <Words>
      <Confidence></Confidence>
      <Character></Character>
      <WordCoordPoint>
        <WordCoordinate>
          <X></X>
          <Y></Y>
        </WordCoordinate>
	  </WordCoordPoint>
    </Words>
  </TextDetections>
  <Language></Language>
  <Angel></Angel>
  <PdfPageSize></PdfPageSize>
  <RequestId></RequestId>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| TextDetections     | Response | Information of the recognized text, including the text line content, confidence, text line coordinates, and text line coordinates after rotation correction. | Container |
| Language           | Response | Detected language. For more information on the supported languages, see the description of the `language-type` input parameter. | String    |
| Angel              | Response | Image rotation angle in degrees. 0° indicates horizontal text, a positive value indicates clockwise rotation, and a negative value indicates anticlockwise rotation. | Float     |
| PdfPageSize        | Response | Total number of PDF pages to be returned if the image is a PDF. Default value: 0.                      | Integer   |
| RequestId          | Response | Unique ID of the request. Each request returns a unique ID. The `RequestId` is required to troubleshoot issues. | String    |

`TextDetections` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------- | :----------------------------------------------------------- | :-------- |
| DetectedText       | TextDetections | Recognized text line content.                                           | String    |
| Confidence         | TextDetections | Confidence between 0 and 100.                                                | Integer   |
| Polygon            | TextDetections | Text line coordinates, which are represented by the coordinates of vertices. Note: This field may return null, indicating that no valid values can be obtained. | Container |
| ItemPolygon        | TextDetections | Pixel coordinates of the text line in the image after rotation correction, which is in the format of (Abscissa of the top-left corner, ordinate of the top-left corner, width, height). | Container |
| Words              | TextDetections | Information of the recognized words (including characters and confidence). Supported recognition types are `general` and `accurate`. | Container |
| WordPolygon        | TextDetections | Array of word coordinates, which are represented by the coordinates of four vertices. <br>Note: This field may return null, indicating that no valid values can be obtained. The supported recognition type is `handwriting`. | Container |

`Polygon` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------ | :----- | :------ |
| X                  | Polygon | Abscissa. | Integer |
| Y                  | Polygon | Ordinate. | Integer |

`ItemPolygon` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------- | :------- | :------ |
| X                  | ItemPolygon | Abscissa of the top-left corner.  | Integer |
| Y                  | ItemPolygon |  Ordinate of the top-left corner.  | Integer |
| Width              | ItemPolygon | Width.  | Integer |
| Height             | ItemPolygon | Height. | Integer |

`Words` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :--------------------------------------------------------- | :-------- |
| Confidence         | Words  | Confidence between 0 and 100.                                              | Integer   |
| Character          | Words  | Recognized word information.                                         | String    |
| WordCoordPoint     | Words  | Four-point coordinates of the word in the input image. Supported recognition types are `general` and `accurate`. | Container |

`WordCoordPoint` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------- | :----------------------------------------------------------- | :-------- |
| WordCoordinate     | WordCoordPoint | Coordinates of the word in the input image, which are represented by the coordinates of four vertices and returned clockwise starting from the top-left vertex. | Container |

`WordCoordinate` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------- | :----- | :------ |
| X                  | WordCoordinate | Abscissa. | Integer |
| Y                  | WordCoordinate | Ordinate. | Integer |

`WordPolygon` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------- | :----------- | :-------- |
| LeftTop            | WordPolygon | Coordinates of the top-left vertex. | Container |
| RightTop           | WordPolygon | Coordinates of the top-right vertex. | Container |
| RightBottom        | WordPolygon | Coordinates of the bottom-right vertex. | Container |
| LeftBottom         | WordPolygon | Coordinates of the bottom-left vertex. | Container |

`LeftTop`, `RightTop`, `RightBottom`, and `LeftBottom` have the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------- | :----- | :------ |
| X                  | WordCoordinate | Abscissa. | Integer |
| Y                  | WordCoordinate | Ordinate. | Integer |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request

```plaintext
GET /<ObjectKey>?ci-process=OCR&type=general&language-type=zh&ispdf=true&isword=true HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 414641
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-image
x-cos-request-id: NWFjMzQ0MDZfOTBmYTUwXzZkZV8z****

<Response>
	<Angel>359.99</Angel>
	<Language>mix</Language>
	<PdfPageSize>0</PdfPageSize>
	<RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
	<TextDetections>
		<Confidence>99</Confidence>
		<DetectedText>Hey you</DetectedText>
		<ItemPolygon>
			<Height>64</Height>
			<Width>123</Width>
			<X>140</X>
			<Y>167</Y>
		</ItemPolygon>
		<Polygon>
			<X>140</X>
			<Y>167</Y>
		</Polygon>
		<Polygon>
			<X>263</X>
			<Y>167</Y>
		</Polygon>
		<Polygon>
			<X>263</X>
			<Y>231</Y>
		</Polygon>
		<Polygon>
			<X>140</X>
			<Y>231</Y>
		</Polygon>
		<Words>
			<Character>Hey</Character>
			<Confidence>99</Confidence>
			<WordCoordPoint>
				<WordCoordinate>
					<X>212</X>
					<Y>167</Y>
				</WordCoordinate>
				<WordCoordinate>
					<X>341</X>
					<Y>167</Y>
				</WordCoordinate>
				<WordCoordinate>
					<X>341</X>
					<Y>231</Y>
				</WordCoordinate>
				<WordCoordinate>
					<X>212</X>
					<Y>231</Y>
				</WordCoordinate>
			</WordCoordPoint>
		</Words>
		<Words>
			<Character>You</Character>
			<Confidence>99</Confidence>
			<WordCoordPoint>
				<WordCoordinate>
					<X>341</X>
					<Y>167</Y>
				</WordCoordinate>
				<WordCoordinate>
					<X>263</X>
					<Y>167</Y>
				</WordCoordinate>
				<WordCoordinate>
					<X>263</X>
					<Y>231</Y>
				</WordCoordinate>
				<WordCoordinate>
					<X>341</X>
					<Y>230</Y>
				</WordCoordinate>
			</WordCoordPoint>
		</Words>
	</TextDetections>
	<TextDetections>
		<Confidence>99</Confidence>
		<DetectedText>Bye bye</DetectedText>
		<ItemPolygon>
			<Height>43</Height>
			<Width>245</Width>
			<X>526</X>
			<Y>1444</Y>
		</ItemPolygon>
		<Polygon>
			<X>526</X>
			<Y>1444</Y>
		</Polygon>
		<Polygon>
			<X>771</X>
			<Y>1444</Y>
		</Polygon>
		<Polygon>
			<X>771</X>
			<Y>1487</Y>
		</Polygon>
		<Polygon>
			<X>526</X>
			<Y>1487</Y>
		</Polygon>
		<Words>
			<Character>Bye</Character>
			<Confidence>99</Confidence>
			<WordCoordPoint>
				<WordCoordinate>
					<X>564</X>
					<Y>1444</Y>
				</WordCoordinate>
				<WordCoordinate>
					<X>608</X>
					<Y>1444</Y>
				</WordCoordinate>
				<WordCoordinate>
					<X>608</X>
					<Y>1487</Y>
				</WordCoordinate>
				<WordCoordinate>
					<X>564</X>
					<Y>1487</Y>
				</WordCoordinate>
			</WordCoordPoint>
		</Words>
		<Words>
			<Character>Bye</Character>
			<Confidence>99</Confidence>
			<WordCoordPoint>
				<WordCoordinate>
					<X>608</X>
					<Y>1444</Y>
				</WordCoordinate>
				<WordCoordinate>
					<X>641</X>
					<Y>1444</Y>
				</WordCoordinate>
				<WordCoordinate>
					<X>641</X>
					<Y>1487</Y>
				</WordCoordinate>
				<WordCoordinate>
					<X>608</X>
					<Y>1487</Y>
				</WordCoordinate>
			</WordCoordPoint>
		</Words>
	</TextDetections>
</Response>
```
