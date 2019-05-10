## Overview
Powered by Tencent YouTu's world-leading facial analysis technology, Tencent Cloud Face Recognition features facial detection and analysis, feature localization, search, comparison, verification, and face liveness detection. It can be accessed via APIs and offline SDKs. It is well-suited for various use cases including smart retailing and smart building, meeting facial recognition and customer identity verification demands from different industries.

## Features
Face Recognition provides the following facial recognition services.

#### Face Detection and Analysis
Face Recognition can analyze an image and determine if the image contains a face, and return the position, attributes and quality if it contains a face. Information returned include gender, age, expression, attractiveness, glasses, hair, mask, posture and quality scores. For more information, see [Face Detection and Analysis](https://cloud.tencent.com/document/product/867/32800).

#### Facial Feature Localization
Face Recognition can perform facial feature localization on a given image and calculate 90 facial key points that make up the contour of the face, including eyebrows (8 points on the left and 8 on the right), eyes (8 points on the left and 8 on the right), nose (13 points), mouth (22 points), face contour (21 points), and eyeballs or pupils (2 points). For more information, see [Facial Feature Localization](https://cloud.tencent.com/document/product/867/32779).

#### Face Comparison
Face Recognition can calculate the similarity of faces in two images and return the face similarity score. For more information, see [Face Comparison](https://cloud.tencent.com/document/product/867/32802).
- If you need to determine whether the person in the image is someone specified in use cases such as face login, i.e., checking whether the person in a given image is someone with a known identity, it is recommended to use [Face Verification](https://cloud.tencent.com/document/product/867/32806).
- If you need to determine the specific identity of a person in an image, such as checking whether a person is the one on an identity card, it is recommended to use [Faceid](https://cloud.tencent.com/product/faceid).

#### Group Management (Formerly Known as Individual Information Management)
Face Recognition allows you to create a library of people to store information about them (such as facial features and IDs) for [face verification](https://cloud.tencent.com/document/product/867/32806) and [face search](https://cloud.tencent.com/document/product/867/32798). For more information, see [APIs related to group management](https://cloud.tencent.com/document/product/867/32780).

#### Face Verification
Face Recognition can determine whether a person in an image corresponds to a given PersonId. For details about PersonId, see APIs related to group management. For more information, see [Face Verification](https://cloud.tencent.com/document/product/867/32806).
Face comparison is used to determine the similarity of two faces. Unlike the [face comparison](https://cloud.tencent.com/document/product/867/32802) API, face verification is used to determine whether the person in the image is someone specified. The specific person's information is stored in the group and he or she may have multiple face images. 

#### Face Search (Formerly Known as Face Retrieval)
Face Recognition can identify similar persons in one or multiple groups for a given image and rank them by similarity in a descending order. It supports up to one million faces in one single search. Additionally, it can search for one or more faces in one single image. For more information, see [Face Search](https://cloud.tencent.com/document/product/867/32798).

#### Image-based Liveness Detection
Image-based liveness detection can detect the liveness of a user with an user-uploaded image. Compared to from video-based liveness detection, image-based liveness detection users do not need to speak, shake head, or wink for detection. This feature should be only used for use cases with low attack defense requirements. For more information, see [Image-based Liveness Detection](https://cloud.tencent.com/document/product/867/32804).

