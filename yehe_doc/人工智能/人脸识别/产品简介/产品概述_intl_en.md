# Overview

Tencent Cloud Face Recognition leverages Tencent YouTu's world-leading face recognition and analysis technologies to provide individual and corporate developers with a full set of high-performance and high-availability face recognition features such as detection, analysis, facial feature localization, search, comparison, verification, duplicate person check, and liveness detection. It is ideal for a wide variety of use cases such as smart retail, smart community, online entertainment, smart buildings, and online identity verification, meeting face recognition and identity verification demands from various industries.

## Features
### Face detection and analysis
Face Recognition can analyze a given image to determine whether it contains a face, and if so, return the position, attributes, and quality information of the face. The returned information includes gender, age, expression, charm, glasses, hair, mask, posture, and quality ranking. For more information, please see [Face Detection and Analysis](https://intl.cloud.tencent.com/document/product/1059/36979).

### Facial feature localization
Face Recognition can perform facial feature localization on a given image and calculate 90 facial keypoints that make up the contour of the face, including eyebrows (8 points on the left and 8 on the right), eyes (8 points on the left and 8 on the right), nose (13 points), mouth (22 points), face contour (21 points), and eyeballs or pupils (2 points). For more information, please see [Facial Feature Localization](https://intl.cloud.tencent.com/document/product/1059/36981).

### Face comparison
Face Recognition can calculate the similarity of faces in two images and return the face similarity score. for more information, please see [Face Comparison](https://intl.cloud.tencent.com/document/product/1059/36981).
- If you need to judge "whether the person in the image is someone specified" in scenarios such as face login, i.e., checking whether the person in a given image is someone with a known identity, you are recommended to use [Face Verification](https://intl.cloud.tencent.com/document/product/1059/36972).

### Group management
Face Recognition allows you to create a group to store information of people (such as facial features and IDs) for [face verification](https://intl.cloud.tencent.com/document/product/1059/36972) and [face search](https://intl.cloud.tencent.com/document/product/1059/36977). For more information, please see [Group Management APIs](https://intl.cloud.tencent.com/document/product/1059/36967).

### Face verification
Face Recognition can judge whether a person in an image corresponds to a given `PersonId`. For more information on `PersonId`, please see [CreateGroup](https://intl.cloud.tencent.com/document/product/1059/36967). For more information, please see [Face Verification](https://intl.cloud.tencent.com/document/product/1059/36972).
Unlike the [CompareFace](https://intl.cloud.tencent.com/document/product/1059/36981) API that is used to judge the similarity between two faces, this feature is used to judge "whether the person in the given image is the same as the `PersonId`" whose information is stored in a group. This `PersonId` may have multiple face images.

### Face search
Face Recognition can recognize the first N persons in one or more groups who are similar to the person in a given image and rank the similarity in a descending order. Up to 3 million faces in such groups can be supported in one search. Searches can be made on one or more faces in the image. For more information, please see [Face Search](https://intl.cloud.tencent.com/document/product/1059/36977).


### Image-based liveness detection
Image-based liveness detection is used to detect the liveness of a user with a user-uploaded image (i.e., checking whether the person in the image is real). Its difference from video-based liveness detection lies in that the user does not need to speak, shake their head, or wink for detection. This feature should be used only for scenarios where the requirement for attack defense is not high. For more information, please see [Image-based Liveness Detection](https://intl.cloud.tencent.com/document/product/1059/36949).