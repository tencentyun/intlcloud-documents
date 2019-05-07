## Candidate

Most matching candidates recognized.

Referenced by: SearchFaces.

| Name | Type | Description |
|------|------|-------|
| PersonId | String | Person ID |
| FaceId | String | Face ID |
| Score | Float | Match score of the candidate. <br/>In a library of 100,000 faces, if the face images are snapshots (with poor face quality), <br/>the 1%, 0.1%, and 0.01% FARs correspond to scores of 70, 80, and 90, respectively; <br/>if the face images are selfies (with high face quality), <br/>the 1%, 0.1%, and 0.01% FARs correspond to scores of 60, 70, and 80, respectively. <br/>It is recommended to choose an appropriate score based on the actual situation, preferably no more than 90. |

## FaceAttributesInfo

Face attributes, including gender, age, expression,
beauty, glass, mask, hair, and pose (pitch, roll, yaw). Valid information is returned only when NeedFaceAttributes is set to 1.

Referenced by: DetectFace.

| Name | Type | Description |
|------|------|-------|
| Gender | Integer | Gender;  [0(female)-100(male)]. If NeedFaceAttributes is not 1 or more than 5 faces are detected, this parameter is still returned but meaningless. |
| Age | Integer | Age; [0,100]. If NeedFaceAttributes is not 1 or more than 5 faces are detected, this parameter is still returned but meaningless. |
| Expression | Integer | Expression [0(normal)-50(smile)-100(laugh)]. If NeedFaceAttributes is not 1 or more than 5 faces are detected, this parameter is still returned but meaningless. |
| Glass | Boolean | Whether glasses are present; [true,false]. If NeedFaceAttributes is not 1 or more than 5 faces are detected, this parameter is still returned but meaningless. |
| Pitch | Integer | Vertical offset; [-30,30]. If NeedFaceAttributes is not 1 or more than 5 faces are detected, this parameter is still returned but meaningless. <br/>It is recommended to select images in the [-10,10] range for adding faces. |
| Yaw | Integer | Horizontal offset; [-30,30]. If NeedFaceAttributes is not 1 or more than 5 faces are detected, this parameter is still returned but meaningless. <br/>It is recommended to select images in the [-10,10] range for adding faces. |
| Roll | Integer | Horizontal rotation, [-180,180]. If NeedFaceAttributes is not 1 or more than 5 faces are detected, this parameter is still returned but meaningless.  <br/>It is recommended to select images in the [-20,20] range for adding faces. |
| Beauty | Integer | Beauty; [0-100]. If NeedFaceAttributes is not 1 or more than 5 faces are detected, this parameter is still returned but meaningless. |
| Hat | Boolean | Whether hat is present; [true,false]. If NeedFaceAttributes is not 1 or more than 5 faces are detected, this parameter is still returned but meaningless. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Mask | Boolean | Whether mask is present; [true,false]. If NeedFaceAttributes is not 1 or more than 5 faces are detected, this parameter is still returned but meaningless. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Hair | [FaceHairAttributesInfo](#FaceHairAttributesInfo) | Hair information, including length, bang and color. If NeedFaceAttributes is not 1 or more than 5 faces are detected, this parameter is still returned but meaningless. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| EyeOpen | Boolean | Whether the eyes are open; [true,false]. As long as there is more than one eyes closed, false is returned. If NeedFaceAttributes is not 1 or more than 5 faces are detected, this parameter is still returned but meaningless. <br/>Note: This field may return null, indicating that no effective values can be obtained. |

## FaceHairAttributesInfo

Hair information in the face attributes.

Referenced by: DetectFace.

| Name | Type | Description |
|------|------|-------|
| Length | Integer | 0 - shaved head; 1 - short hair; 2 - medium hair; 3 - long hair; 4 - braid <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Bang | Integer | 0 - with bangs, 1 - no bangs <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Color | Integer | 0 - black, 1 - golden, 2 - brown, 3 - gray <br/>Note: This field may return null, indicating that no effective values can be obtained. |

## FaceInfo

Face information list.

Referenced by: DetectFace.

| Name | Type | Description |
|------|------|-------|
| X | Integer | Horizontal coordinate of the upper left corner of the face frame. <br/>The face frame encompasses the facial features and is extended accordingly. If it is larger than the image, the coordinates will be negative. <br/>If you want to capture a complete face, you can set the negative coordinates to 0 if the completeness score meets the requirement. |
| Y | Integer | Vertical coordinate of the upper left corner of the face frame. <br/>The face frame encompasses the facial features and is extended accordingly. If it is larger than the image, the coordinates will be negative. <br/>If you want to capture a complete face, you can set the negative coordinates to 0 if the completeness score meets the requirement. |
| Width | Integer | Face frame width. |
| Height | Integer | Face frame height. |
| FaceAttributesInfo | [FaceAttributesInfo](#FaceAttributesInfo) | Face attributes, including gender, age, expression, <br/>beauty, glass, mask, hair, and pose (pitch, roll, yaw). Valid information is returned only when NeedFaceAttributes is set to 1. |
| FaceQualityInfo | [FaceQualityInfo](#FaceQualityInfo) | Face quality information, including score, sharpness, brightness, and completeness. Valid information is returned only when NeedFaceDetection is set to 1. <br/>Note: This field may return null, indicating that no effective values can be obtained. |

## FaceQualityCompleteness

Completeness of the facial features, which assesses the completeness of the eyebrows, eyes, nose, cheeks, mouth, and chin.

Referenced by: DetectFace.

| Name | Type | Description |
|------|------|-------|
| Eyebrow | Integer | Completeness of the eyebrows; [0,100]; the higher the score, the more complete the eyebrows. <br/>Reference range: [0,80] - incomplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Eye | Integer | Completeness of the eyes; [0,100]; the higher the score, the more complete the eyes. <br/>Reference range: [0,80] - incomplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Nose | Integer | Completeness of the nose; [0,100]; the higher the score, the more complete the nose. <br/>Reference range: [0,60] - incomplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Cheek | Integer | Completeness of the cheeks; [0,100]; the higher the score, the more complete the cheeks. <br/>Reference range: [0,70] - incomplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Mouth | Integer | Completeness of the mouth; [0,100]; the higher the score, the more complete the mouth. <br/>Reference range: [0,50] - incomplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Chin | Integer | Completeness of the chin; [0,100]; the higher the score, the more complete the chin. <br/>Reference range: [0,70] - incomplete. <br/>Note: This field may return null, indicating that no effective values can be obtained. |

## FaceQualityInfo

Face quality information, including score, sharpness, brightness, and completeness. Valid information is returned only when NeedFaceDetection is set to 1.

Referenced by: DetectFace.

| Name | Type | Description |
|------|------|-------|
| Score | Integer | Quality score; [0,100]; it comprehensively evaluates whether the image quality is suitable for face recognition; the higher the score, the higher the quality. <br/>Reference range: [0,40] - poor; [40,60] - fine; [60,80] - good; [80,100] - excellent. <br/>It is recommended to select images with a score above 70 for adding faces. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Sharpness | Integer | Sharpness; [0,100]; it evaluates the sharpness of the image; the higher the score, the sharper the image. <br/>Reference range: [0,40] - very blurry; [40,60] - blurry; [60,80] - fine; [80,100] - sharp. <br/>It is recommended to select images with a score above 80 for adding faces. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Brightness | Integer | Brightness; [0,100]; the brighter the image, the higher the score. <br/>Reference range: [0,30] - dark; [30,70] - normal; [70,100] - bright. <br/>It is recommended to select images in the [30,70] range for adding faces. <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Completeness | [FaceQualityCompleteness](#FaceQualityCompleteness) | Completeness score of the facial features, which assesses the completeness of the eyebrows, eyes, nose, cheek, mouth, and chin. <br/>Note: This field may return null, indicating that no effective values can be obtained. |

## FaceRect

Position of the detected face frame.

Referenced by: SearchFaces.

| Name | Type | Description |
|------|------|-------|
| X | Integer | Horizontal coordinate of the upper left corner of the face frame. <br/>The face frame encompasses the facial features and is extended accordingly. If it is larger than the image, the coordinates will be negative. <br/>If you want to capture a complete face, you can set the negative coordinates to 0 if the completeness score meets the requirement. |
| Y | Integer | Vertical coordinate of the upper left corner of the face frame. <br/>The face frame encompasses the facial features and is extended accordingly. If it is larger than the image, the coordinates will be negative. <br/>If you want to capture a complete face, you can set the negative coordinates to 0 if the completeness score meets the requirement. |
| Width | Integer | Face width |
| Height | Integer | Face height |

## FaceShape

Specific information of facial feature localization (facial key points).

Referenced by: AnalyzeFace.

| Name | Type | Description |
|------|------|-------|
| FaceProfile | Array of [Point](#Point) | 21 points that describe the face contour. |
| LeftEye | Array of [Point](#Point) | 8 points that describe the left eye. |
| RightEye | Array of [Point](#Point) | 8 points that describe the right eye. |
| LeftEyeBrow | Array of [Point](#Point) | 8 points that describe the left eyebrow. |
| RightEyeBrow | Array of [Point](#Point) | 8 points that describe the right eyebrow. |
| Mouth | Array of [Point](#Point) | 22 points that describe the mouth. |
| Nose | Array of [Point](#Point) | 13 points that describe the nose. |
| LeftPupil | Array of [Point](#Point) | 1 point that describes the left pupil. |
| RightPupil | Array of [Point](#Point) | 1 point that describes the right pupil. |

## GroupExDescriptionInfo

Custom description field of the group to be modified; key-value.

Referenced by: ModifyGroup.

| Name | Type | Required | Description |
|------|------|----------|------|
| GroupExDescriptionIndex | Integer | Yes | Custom group description field index, starting from 0 |
| GroupExDescription | String | Yes | Content of the custom group description field to be updated |

## GroupInfo

Returned group information.

Referenced by: GetGroupList.

| Name | Type | Description |
|------|------|-------|
| GroupName | String | Group name |
| GroupId | String | Group ID |
| GroupExDescriptions | Array of String | Custom group description field <br/>Note: This field may return null, indicating that no effective values can be obtained. |
| Tag | String | Group tag <br/>Note: This field may return null, indicating that no effective values can be obtained. |

## PersonExDescriptionInfo

Content of the person description field to be modified; key-value.

Referenced by: CreatePerson, ModifyPersonGroupInfo.

| Name | Type | Required | Description |
|------|------|----------|------|
| PersonExDescriptionIndex | Integer | Yes | Person description field index, starting from 0 |
| PersonExDescription | String | Yes | Content of the person description field to be updated |

## PersonGroupInfo

List of groups containing this person and their description fields.

Referenced by: GetPersonGroupInfo.

| Name | Type | Description |
|------|------|-------|
| GroupId | String | ID of group that contains this person |
| PersonExDescriptions | Array of String | Content of the person description field |

## PersonInfo

Returned person information.

Referenced by: GetPersonList.

| Name | Type | Description |
|------|------|-------|
| PersonName | String | Person name |
| PersonId | String | Person ID |
| Gender | String | Person gender |
| PersonExDescriptions | Array of String | Content of the person description field |
| FaceIds | Array of String | List of contained face images |

## Point

Coordinates.

Referenced by: AnalyzeFace.

| Name | Type | Description |
|------|------|-------|
| X | Integer | X coordinate |
| Y | Integer | Y coordinate |

## Result

Face recognition result.

Referenced by: SearchFaces.

| Name | Type | Description |
|------|------|-------|
| Candidates | Array of [Candidate](#Candidate) | Most matching candidates recognized |
| FaceRect | [FaceRect](#FaceRect) | Position of the detected face frame |


