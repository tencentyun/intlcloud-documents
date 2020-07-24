# Overview

Tencent Cloud Face Recognition leverages Tencent YouTu's face recognition and analysis technologies to provide developers and enterprises with a full set of high-performance and high-availability face recognition services such as detection, analysis, search, comparison, verification, feature localization, and liveness detection. It is applicable to scenarios such as smart retail, smart community, online entertainment, smart buildings, and online identity verification, meeting the needs for facial attribute recognition and identity verification across industries.

## Features
### Face detection and analysis
Face Recognition can analyze a given image to determine whether it contains a face. If yes, it can return information about the position, attributes, and quality of the face. This includes gender, age, expression, charm, glasses, hair, mask, pose, quality ranking, etc. For more information, please see [Face Detection and Analysis](https://intl.cloud.tencent.com/document/product/1059/36979).

### Facial feature localization
Face Recognition can locate facial features on a given image and calculate 90 facial landmarks. This includes eyebrows (8 points on each side), eyes (8 points on each side), nose (13 points), mouth (22 points), face contour (21 points), and eyeballs or pupils (2 points). For more information, please see [Facial Feature Localization](https://intl.cloud.tencent.com/document/product/1059/36981).

### Face comparison
Face Recognition can compare faces in two images and return the similarity score. For more information, please see [Face Comparison](https://intl.cloud.tencent.com/document/product/1059/36981).
- If you need to check "whether the person is someone" in scenarios such as face log-in, i.e., whether the person in a given image is someone with a known identity, we recommend using [Face Verification](https://intl.cloud.tencent.com/document/product/1059/36972).

### Group management
Face Recognition allows you to create a group to store information about people (such as facial features and IDs) for [face verification](https://intl.cloud.tencent.com/document/product/1059/36972) and [face search](https://intl.cloud.tencent.com/document/product/1059/36977). For more information, please see [Group Management APIs](https://intl.cloud.tencent.com/document/product/1059/36967).

### Face verification
Face Recognition can check whether a person in an image corresponds to a given `PersonId`. For more information on `PersonId`, please see [Group Management APIs](https://intl.cloud.tencent.com/document/product/1059/36967). For more information, please see [Face Verification](https://intl.cloud.tencent.com/document/product/1059/36972).
Unlike the [CompareFace](https://intl.cloud.tencent.com/document/product/1059/36981) API that is used to compare the similarity of two faces, face verification is used to check "whether the person in a given image is the same as the `PersonId`" whose information is stored in a group. This `PersonId` may have multiple face images.

### Face search
Face Recognition can recognize the first N people in one or more groups who are similar to the person in a given image and rank the similarity in descending order. Each search supports up to 3 million faces in such groups. The search can be made on one or more faces in the image. For more information, please see [Face Search](https://intl.cloud.tencent.com/document/product/1059/36977).


### Image-based liveness detection
Image-based liveness detection is used to detect the liveness of faces in images uploaded by the user (i.e., whether the person in the image is real). Compared to video-based liveness detection, image-based detection does not require speaking, shaking heads, winking, etc. It is only suitable for scenarios where requirements for attack defense are not high. For more information, please see [Image-based Liveness Detection](https://intl.cloud.tencent.com/document/product/1059/36949).