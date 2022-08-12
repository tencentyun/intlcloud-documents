## Feature description
Index optimization is an important part of database optimization. An optimal index can improve the query efficiency of the entire database. In view of the Ops characteristics of TencentDB for MongoDB, DBbrain offers the index recommendation feature to help you easily increase the global indexing efficiency of your instance.

After collecting and automatically analyzing slow logs in real time, the index recommendation feature proposes globally optimal indexes and rank them by their impact on the performance. An index that has a greater recommendation value will increase the performance more significantly. In addition, this feature also displays the slow queries and performance metrics associated with the recommended indexes, as well as invalid and duplicate indexes and their causes.

You only need to perform one operation based on the recommended indexes, and you can easily check the operation progress.

## Enabling index recommendation
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain) and select **Performance Optimization** on the left sidebar. On the displayed page, select the target TencentDB for MongoDB instance at the top and select the **Index Recommendation** tab.
2. Read the note on data privacy risk and feature, indicate your consent, and click **Enable Now** as shown below.
> ?
> - When you enable index recommendation for the first time, all data may not be obtained immediately as the calculation starts from the current time point. Data will be complete after a period of time.
> - The index recommendation feature basically has no impact on the database performance; for example, in a 4-core 8GB MEM database, it consumes only 0.3 CPU cores after sampling for 10 minutes in a large table with 100 million data records.
> 

## Viewing recommended indexes
1. View the overall optimization level of the instance.
   DBbrain assesses the index data of the source instance and presents one of four recommended SQL optimization levels: S > A > B > C. Level S indicates the optimal database performance, while level C indicates the worst database performance (the database requires urgent optimization).
2. View the recommended index sets.
   DBbrain aggregates the recommendations based on the detected index data and sorts the indexes by recommendation value. A greater value indicates that the index set contains indexes that require urgent optimization, and their optimization will most significantly improve the database performance. 
3. Click the name of an index set, and the recommendation details of indexes in it will be displayed on the right.
   - The **Recommended Indexes** tab displays indexes that need to be added as there are many slow queries. Similarly, indexes that have a greater recommendation value will more significantly enhance the performance after being added.   
   - The **Invalid Indexes** tab displays indexes that are recommended to be deleted.

## Adding a recommended index 
1. On the **Recommended Indexes** tab, click an index, and the corresponding slow query analysis and records will be displayed on the right.
2. Click the icon in the red box as shown below to zoom in the slow query window for clearer information display. You can also download the slow query information.
3. In the **Auto-Generate Execution Statement** module, click **Create Index**.
   To perform index operations, you need to log in to your database for authentication first.
4. You can select **Default** or **Specify options** as the creation method as needed, and DBbrain will automatically generate a creation statement accordingly.  
5. You can view the index creation progress. You can also view the index set's operations in its **Operation Records**.
   In the operation list, you can view the historical addition or deletion details of indexes in the index set and terminate the indexes being processed.  
> !To ensure the stability of your production database, when an index in the index set is being created or deleted, you cannot add or delete another index in the index set, and the system will report an error if you do so.

## Deleting an invalid index based on recommendation
On the **Invalid** tab, view and delete invalid indexes. When your database contains an invalid index, the index recommendation system will display the reason for its invalidity and generate a deletion command. You can delete the index as prompted.

## Viewing the index history and index adding effect
1. Click **History** on the right of **Recommended Index Sets** or click **View Details** below **Optimization Statistics** to view the historical index optimization records of the current instance. 
2. After clicking **History**, click **Comparison** in the **Operation** column to view the effect before and after optimization.
