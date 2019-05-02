### APK 
APK (Android Package) is the installation package for Android. An app can be installed by transferring its APK file to the Android OS.

### Offline SDK
An offline SDK is a toolkit that implements a certain function of a software product without network connection. The offline SDK of Face Recognition supports real-time processing on the device side.

### QPS/Concurrency
QPS/concurrency is the number of concurrent requests per second. 1 QPS means that 1 request to the API is supported per second, while 50 QPS means 50 requests to the API is supported per second.

### Group
A group is a collection of face libraries of persons with known identities. The [face search](https://cloud.tencent.com/document/product/867/32798) and [face verification](https://cloud.tencent.com/document/product/867/32806) service can only be used with the [group management](https://cloud.tencent.com/document/product/867/32794) service.

### Data Set
A data set is a collection of data. In the field of machine learning, it usually refers to a collection of data that is specifically collected and labeled. Sometimes, it is also called sample set.

### Sample
A sample is an event or object in a data set/sample set. In Face Recognition, a face image is a sample.

### Training Set
A training set is a pre-labeled sample set used to train a model. Test sets and training sets must be strictly differentiated.

### Test Set
A test set is a pre-labeled sample set that is used to test the effects of a trained model.

### Similarity Score/Match Score
The similarity score/match score is the basis for judgment by [face comparison](https://cloud.tencent.com/document/product/867/32802) and [face search](https://cloud.tencent.com/document/product/867/32798) services. The higher the score, the more similar the faces. The recommended false acceptance rate (FAR) is usually 0.1% or 0.01%. If a score is higher than the recommended value, the recommended conclusion is that the two faces are the same person under the corresponding FAR. Otherwise, they are different persons.

### Learning/Training
Learning/training is the process of learning a model from data, which is done by executing a learning algorithm.

### Positive Sample and Negative Sample
Positive and negative samples are relative concepts. Assuming that there are 10 face images in Face Recognition, of which 4 ones are of person A and 6 person B, if the purpose is to identify A, then the number of positive samples is 4 and the number of negative samples is 6; however, if the purpose is to identify B, then the number of positive samples is 6 and the number of negative samples is 4.

### Recall Rate
In Face Recognition, if the number of positive samples (face images from the same person) in the test set is P, the number of negative samples (face images from different persons) is N, the number of positive samples correctly determined by the algorithm is TP and the number of positive samples incorrectly determined by the algorithm is FN (TP + FN = P), and the number of negative samples correctly determined by the algorithm is TN and the number of negative samples incorrectly determined by the algorithm is FP (TN + FP = N), then the recall rate = TP / P * 100%.

### False Acceptance Rate (FAR)
FAR = FP / N * 100%

### Precision Rate
Precision rate = TP / (TP + FP) * 100%

### Top N Hit Rate
In face search, the top N hit rate is the probability that the face with the correct identity is listed in the top N results. If the number of searches is M, and the face with the correct identity is listed in the top N results for TN times, then the top N hit rate = TN / M * 100%.
