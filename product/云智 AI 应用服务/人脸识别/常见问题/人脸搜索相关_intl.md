### How many groups and face files can be created for my face search service?
A maximum of 20,000 groups can be created under one APPID, and one group can contain up to one million face files.

### Can I create the same Person for different groups?
No. The PersonID is unique for each APPID instead of Group. Therefore, if you want to create the same person in different Groups, instead of creating that person individually in each Group, copy the person to the different Groups.

### How many groups can be searched at the same time?
The recommended maximum quantity is 100.

### If I delete a group, will I delete a person in that group who also belongs to other groups?
No. If a person belongs to multiple groups, deleting a group will not affect anything about that person but the description information that is customized for that group.

### If I delete a person who belongs to multiple groups in one of the groups, will the deletion take effect in all other groups?
Yes. 

### What is the recommended threshold for face search?
Take a face library of 100,000 images as an example:
- If the face images are candid shots (with poor face quality), the 1%, 0.1%, and 0.01% FARs correspond to scores of 70, 80, and 90 points, respectively.
- If the face images are selfies (with high face quality), the 1%, 0.1%, and 0.01% FARs correspond to scores of 60, 70, and 80 points, respectively.
 
It is recommended to choose an appropriate score based on the actual situation, preferably no more than 90 points.

### How many images can the face search feature process per second?
Generally, it can process one million face images within one second, subject to the network environment and face library size.

### Does face search support cross-library search?
Yes.

### How is face search billed?
Face search is billed on the basis of API calls. For example, if there are N persons in a group and each person has M photos, no matter how many faces in the library are retrieved, the fees will be calculated based on the number of API calls.
