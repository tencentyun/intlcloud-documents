The common errors of the TPNS rest API mainly include the following:

| Error code | English descriptor | Error description | Feedback API |
| --- | --- | --- | --- |
|       1008001 | paramter parse error | Parameter parse error | General API |
| 1008002 | missing parameter | Required parameter missing | General API |
| 1008003 | auth failure | Verification and authentication failed | General API |
| 1008004 | invoke service error | Calling internal service failed | General API |
| 1008006 | invalid token | Token invalid: please check it | Tag operation and account operation APIs |
| 1008007 | invalid parameter | Parameter verification failed | General API |
| 1008011 | upload file error | File upload failed | Certificate upload API and number package upload API |
| 1008012 | upload empty file | Uploaded file is empty | Certificate upload API and number package upload API |
| 1008013 | parse certificate error | Certificate parse failed | Certificate upload API |
| 1008015 | push id not exist | Push task ID does not exist | Statistics query API |
| 1008016 | date param formate error | Incorrect date and time parameter format | Statistics query API |
| 1008019 | content may be evil | Determined to be discordant by the content security service | Push API |
| 10010005 | internal error | Push target does not exist | Push API |
| 1008026 | batch op，partly error | Batch operation partially failed | Account binding and query API |
| 1008027 | batch op，total error | Batch operation fully failed | Account binding and query API |
| 10110008 | no token，no account  | Queried token and account do not exist | Account binding and query API |
