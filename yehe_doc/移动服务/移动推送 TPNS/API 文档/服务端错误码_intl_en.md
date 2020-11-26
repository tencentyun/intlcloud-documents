 The common errors of the TPNS RESTful API mainly include the following:

| Error code | English descriptor | Error description | Feedback API |
| -------- | ---------------- | ---------------- | ----------- |
|       1008001 | paramter parse error | Parameter parse error | General API |
| 1008002 | missing parameter | A required parameter is missing | General API |
| 1008003 | auth failure | Verification and authentication failed | General API |
| 1008004 | invoke service error | Failed to call the internal service | General API |
| 1008006 | invalid token | Invalid token. Please check it | Tag operation and account operation APIs |
| 1008007 | invalid parameter | Parameter verification failed | General API |
| 1008011 | upload file error | File upload failed | Certificate upload API and number package upload API |
| 1008012 | upload empty file | The uploaded file is empty | Certificate upload API and number package upload API |
| 1008013 | parse certificate error | Certificate parse failed | Certificate upload API |
| 1008015 | push id not exist | The push task ID does not exist | Statistics query API |
| 1008016 | date param formate error | Incorrect date and time parameter format | Statistics query API |
| 1008019 | content may be evil | Determined to be non-compliant by the content security service | Push API |
| 1008020  |cert bundleId check failed| Certificate package name verification failed | Certificate upload API |
| 1008021 | not correct p12 file | p12 certificate format verification failed | Certificate upload API |
| 1008022  |p12 password is not correct| Incorrect p12 certificate password | Certificate upload API |
| 1008025  |create app , platform exist| Application creation failed. The application already exists under the product | Application creating API |
| 1008026 | batch op, partly error | Batch operation partially failed | Account binding and query API |
| 1008027 | batch op, total error | Batch operation fully failed | Account binding and query API |
| 1008028  |request too fast| Limit exceeded | Statistics API |
| 1008029  |token is not valid| Invalid token | Single push API, account binding API, and tag binding API |
| 1008030  |app not paid| No payment has been made for the application | General error |
| 1008031  |app was expired| The application resource has been terminated | General error |
| 10110008 | no token, no account  | The queried token and account do not exist | Account binding and query API |
| 10010005 | internal error | The push target does not exist | Push API |
| 10010018 | Push repeat | Repeated push | Push APIs for full push and tag push |
