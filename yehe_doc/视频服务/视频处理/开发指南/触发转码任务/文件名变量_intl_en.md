MPS supports rendering target paths of output files with the following variables:

| Variable Name | Description |
| -- | -- |
| inputName | Input file name |
| inputFormat | Input file format |
| format | Output file format |
| definition | Parameter template ID |
| number | Output file number |


### Sample 1

If your transcoding requirements are as follows:
* The name of the input file is `AnimalWorldE01.mp4`.
* Transcoding templates 100010, 100020, and 100030 are used.
* The names of the output files are `AnimalWorldE01_100010.mp4`, `AnimalWorldE01_100020.mp4`, and `AnimalWorldE01_100030.mp4`, respectively.

Then, when using the [ProcessMedia](https://intl.cloud.tencent.com/document/product/1041/33640) API to initiate transcoding:
You should specify the `InputInfo.CosInputInfo.OutputObjectPath` parameter as `{inputName}_{definition}.{format}`.

#### Sample 2

If your transcoding requirements are as follows:
* The name of the input file is `AnimalWorldE01.mp4`.
* Transcoding template 100210 is used.
* The name of the output .m3u8 file is `AnimalWorldE01_from_mp4.m3u8`.
* The names of the output .ts files are `AnimalWorldE01_from_mp4_0.ts`, `AnimalWorldE01_from_mp4_1.ts`, `AnimalWorldE01_from_mp4_2.ts`, and so on.

Then, when using the [ProcessMedia](https://intl.cloud.tencent.com/document/product/1041/33640) API to initiate transcoding:
* You should specify the `InputInfo.CosInputInfo.OutputObjectPath` parameter as `{inputName}_from_{inputFormat}.{format}`.
* You should specify the `InputInfo.CosInputInfo.SegmentObjectName` parameter as `{inputName}_from_{inputFormat}_{number}.{format}`.
