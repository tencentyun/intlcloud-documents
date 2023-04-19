The common errors of the RESTful APIs of Tencent Push Notification Service mainly include the following:

| Error Code | Description | Feedback API |
| -------- | ---------------- | ---------------- | ----------- |
| 1008001 | Parameter parsing error | General API |
| 1008002 | Parameter missing | General API |
| 1008003 | Authentication failed | General API |
| 1008004 | Failed to call internal service | General API |
| 1008006 | Invalid token | Tag operation and account operation APIs |
| 1008007 | Invalid parameter | General API |
| 1008011 | File upload failed | Certificate upload API and number package upload API |
| 1008012 | The uploaded file is empty | Certificate upload API and number package upload API |
| 1008013 | Failed to parse the certificate | Certificate upload API |
| 1008015 | The push task ID does not exist | Statistics query API |
| 1008016 | Incorrect date and time parameter format | Statistics query API |
| 1008019 | The content is considered non-compliant by the content security service | Push API |
| 1008020 | Failed to verify the certificate package name | Certificate upload API |
| 1008021 | Failed to verify the content and format of the .p12 certificate | Certificate upload API |
| 1008022  | Incorrect .p12 certificate password | Certificate upload API |
| 1008023  |iOS push cert was expired for the environment: PRODUCT| Push certificate verification error. Check whether the certificate is within its validity period. | Push API |
| 1008025 | Failed to create the application. The application already exists under the product | App creation API |
| 1008026 | Batch operation partially failed | Account binding and query API |
| 1008027 | Batch operation completely failed | Account binding and query API |
| 1008028  | Request too fast| Exceeded the frequency limit:<li>Exceeded the call frequency limit of statistics APIs.</li><li>Exceeded the push frequency limits of push to all devices, push to devices with specified tags, and push by account package. For related information, see "Note" in [Push API](https://www.tencentcloud.com/document/product/1024/33764).</li> | Statistics API and push API|
| 1008029 | Invalid token | Single push API, account binding API, and tag binding API |
| 1008030 | The app is not paid | General error |
| 1008031  | Application resources are terminated | General error |
| 10110008 | The queried token or account does not exist | Account binding and query API |
| 10010005 | The push target does not exist | Push API |
| 10010012 | Invalid push time | Push API |
| 10010018 | Repeated push | Push APIs for full push and tag push |
| 1008035  | The application AccessID is incorrect, or the service access point of your application does not match the domain address entered. Refer to [Service URL](https://www.tencentcloud.com/document/product/1024/38517) | General error |

