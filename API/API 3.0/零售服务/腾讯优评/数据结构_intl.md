## AgePortrait

User age profile

Referenced by: DescribeUserPortrait.

| Name | Type | Description |
|------|------|-------|
| AgeRange | String | Age range |
| Percent | Float | Percentage |

## AgePortraitInfo

User age profile element array

Referenced by: DescribeUserPortrait.

| Name | Type | Description |
|------|------|-------|
| PortraitSet | Array of [AgePortrait](#AgePortrait) | User age profile array |

## BrandReportArticle

Article information

Referenced by: DescribeBrandSocialOpinion.

| Name | Type | Description |
|------|------|-------|
| Title | String | Article title |
| Url | String | Article URL address |
| FromSite | String | Article source |
| PubTime | Timestamp | Article release date |
| Flag | Integer | Article ID |
| Hot | Integer | Article buzz volume |
| Level | Integer | Article source level |
| Abstract | String | Article abstract |
| ArticleId | String | Article ID |

## Comment

User positive/negative comment count information

Referenced by: DescribeBrandCommentCount.

| Name | Type | Description |
|------|------|-------|
| Date | Date | Comment date |
| NegCommentCount | Integer | Number of negative comments |
| PosCommentCount | Integer | Number of positive comments |

## CommentInfo

User comment content type

Referenced by: DescribeBrandNegComments, DescribeBrandPosComments.

| Name | Type | Description |
|------|------|-------|
| Comment | String | Comment content |
| Date | Timestamp | Comment time |

## DateCount

Statistics by date

Referenced by: DescribeBrandExposure, DescribeBrandMediaReport, DescribeBrandSocialReport, DescribeIndustryNews.

| Name | Type | Description |
|------|------|-------|
| Date | Date | Statistics date |
| Count | Integer | Statistical count |

## GenderPortrait

Gender profile element

Referenced by: DescribeUserPortrait.

| Name | Type | Description |
|------|------|-------|
| Gender | String | Gender |
| Percent | Integer | Percentage |

## GenderPortraitInfo

User gender profile element array

Referenced by: DescribeUserPortrait.

| Name | Type | Description |
|------|------|-------|
| PortraitSet | Array of [GenderPortrait](#GenderPortrait) | User gender profile array |

## IndustryNews

Industry report news

Referenced by: DescribeIndustryNews.

| Name | Type | Description |
|------|------|-------|
| IndustryId | String | Industry ID |
| PubTime | Timestamp | Report release time |
| FromSite | String | Report source |
| Title | String | Report title |
| Url | String | Report source URL |
| Level | Integer | Report source level |
| Hot | Integer | Buzz volume |
| Flag | Integer | Report ID |
| Abstract | String | Report abstract |

## MoviePortrait

Movie preference profile element

Referenced by: DescribeUserPortrait.

| Name | Type | Description |
|------|------|-------|
| Name | String | Movie name |
| Percent | Float | Percentage |

## MoviePortraitInfo

User favorite movie profile element array

Referenced by: DescribeUserPortrait.

| Name | Type | Description |
|------|------|-------|
| PortraitSet | Array of [MoviePortrait](#MoviePortrait) | User favorite movie profile array |

## ProvincePortrait

Province profile element

Referenced by: DescribeUserPortrait.

| Name | Type | Description |
|------|------|-------|
| Province | String | Province name |
| Percent | Float | Percentage |

## ProvincePortraitInfo

User province profile element array

Referenced by: DescribeUserPortrait.

| Name | Type | Description |
|------|------|-------|
| PortraitSet | Array of [ProvincePortrait](#ProvincePortrait) | User province profile array |

## StarPortrait

Celebrity preference profile element

Referenced by: DescribeUserPortrait.

| Name | Type | Description |
|------|------|-------|
| Name | String | Favorite celebrity name |
| Percent | Float | Percentage |

## StarPortraitInfo

User favorite celebrity profile element array

Referenced by: DescribeUserPortrait.

| Name | Type | Description |
|------|------|-------|
| PortraitSet | Array of [StarPortrait](#StarPortrait) | User favorite celebrity profile array |


