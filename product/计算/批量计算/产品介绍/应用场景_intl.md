## Gene Sequencing
Bioinformatics companies or laboratories use sequencers to obtain the raw files of gene sequences, upload the information to cloud storage systems such as COS after completing the preliminary analysis of the sequences, and then further process the information using Batch.

![Gene sequencing](https://mc.qcloudimg.com/static/img/810c499a0a74a2fba07fbe439ff6c7b1/image.png)

#### General Steps
1. The bioinformatics expert obtains the raw information from the sequencer or private cloud storage and uploads it to Tencent Cloud storage services such as COS and CFS;
2. The user defines the Batch job used to analyze the information and then submits the job. The storage configuration of the job is associated with the raw information uploaded in the previous step;
3. Batch automatically schedules resources, deploys the user-uploaded custom analysis image to the scheduled CVM instance, and schedules the job to analyze the raw information;
4. After the computation on CVM is completed, Batch will automatically upload the analysis results to the user-specified location,
The raw information to be analyzed will be uploaded to COS.

## Movie, Television and Design Sketch Rendering
In the visual creation industries such as movie, television, advertising and architectural planning, content creators and post-production companies need to use a large number of machines to complete the rendering work related to visual effects, 3D animations and design sketches. Batch gives users the ability to automate content rendering workflows. Users can build their own rendering-dependent processes, while leveraging Batch's abilities to schedule massive volumes of resources and jobs to efficiently complete visual creation work.

![Movie, television and design sketch rendering](https://mc.qcloudimg.com/static/img/c667521cad604d95cd9ef0efe011a361/image.png)

#### General Steps
1. The user prepares the raw rendering material files needed and uploads them to Tencent Cloud storage services such as COS and CFS;
2. The user defines the Batch job used to analyze the information and then submits the job. The storage configuration of the job is associated with the raw information uploaded in the previous step;
3. Batch automatically schedules resources, deploys the user-uploaded custom rendering image to the scheduled CVM instance, and schedules the job to render the videos or design sketches;
4. After the rendering on CVM is completed, Batch will upload the generated videos or sketches to the user-specified location.
