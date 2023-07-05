
## Gene Sequencing
Bioinformatics companies or laboratories use sequencers to obtain the raw files of gene sequences, upload the information to cloud storage systems such as COS after completing the preliminary analysis of the sequences, and then further process the information using BatchCompute.
![](https://main.qcloudimg.com/raw/d278dddab5b44da4dfb2fec54e6031b7.png)

#### General Steps
1. The bioinformatics expert gets the raw information from the sequencer or private cloud storage and uploads it to Tencent Cloud storage services such as [COS](https://intl.cloud.tencent.com/zh/document/product/436/6222) and [CFS](https://intl.cloud.tencent.com/zh/document/product/582/9127);
2. The user defines the BatchCompute job used to analyze the information and then submits the job. The storage configuration of the job is associated with the raw information uploaded in the previous step;
3. BatchCompute automatically schedules resources, deploys the user-uploaded custom analysis image to the scheduled CVM instance, and schedules the job to analyze the raw information;
4. After the computation on CVM is completed, BatchCompute will automatically upload the analysis results to the user-specified location;
5. The raw information to be analyzed will be uploaded to COS.

## Movie, Video, and Design Sketch Rendering
In the visual creation industries such as movie, television, advertising, and architectural planning, content creators and post-production companies need to use a large number of machines to complete the rendering work related to visual effects, 3D animations, and design sketches. BatchCompute enables users to automate content rendering workflows. Users can build their own rendering-dependent processes while leveraging BatchCompute's abilities to schedule massive volumes of resources and jobs to efficiently complete visual creation work.
![](https://main.qcloudimg.com/raw/cc1ba1087300bfced93a9f37b09ad253.png)

#### General Steps
1. The user prepares the raw rendering material files needed and uploads them to Tencent Cloud storage services such as COS and CFS;
2. The user defines the BatchCompute job used to analyze the information and then submits the job. The storage configuration of the job is associated with the raw information uploaded in the previous step;
3. BatchCompute automatically schedules resources, deploys the user-uploaded custom rendering image to the scheduled CVM instance, and schedules the job to render the videos or design sketches;
4. After the rendering on CVM is completed, BatchCompute will upload the generated videos or sketches to the user-specified location.
