### How many groups and faces can be created for face search?
A maximum of 20,000 groups can be created under one APPID, and a single group can contain up to one million faces, which can be adjusted based on actual needs.

### Can the same PersonId be created in different groups?
No. PersonIds are differentiated based on APPID but not group. Therefore, if you want the same person to belong to different groups, you can directly copy the person.

### How many groups can be searched simultaneously?
The recommended maximum quantity is 100.

### If a person belongs to multiple groups, will they be deleted when a group is deleted?
No. If a person exists in multiple groups at the same time, deleting a group will not delete the person, but the custom description field information in the group will be deleted.

### If a person belongs to multiple groups, will they be deleted from all groups when they are deleted from one group?
Yes. Deleting this person from one group will cause them to be deleted from all groups.

### What is the recommended threshold for face search?
Take a face library of 100,000 images as an example:
- If the face images are snapshots (with poor face quality), the 1%, 0.1%, and 0.01% FARs correspond to scores of 70, 80, and 90 points, respectively.
- If the face images are selfies (with high face quality), the 1%, 0.1%, and 0.01% FARs correspond to scores of 60, 70, and 80 points, respectively.
 
It is recommended to choose an appropriate score based on the actual situation, preferably no more than 90 points.


### How many images can the face search feature process per second?
Generally, it can process one million face images within one second, subject to the network environment and face library size.

### Does face search support cross-library search?
Yes.

### How does the face search charge?
Face search is billed on the basis of API calls. For example, if there are N persons in a group and each person has M photos, no matter how many faces in the library are retrieved, the fees will be calculated based on the number of API calls.
