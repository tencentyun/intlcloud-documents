The SQL optimization feature provides you with one-click SQL statement optimization and the corresponding execution plan modification and optimization suggestions. SQL optimization is suitable for scenarios such as slow SQL statement business optimization, pre-release code review, and self-check. The optimizer uses a command line-style text input page to provide you with visualization platform component services and recover your database usage habits as much as possible.

You can manually enter SQL statements and analyze them to get their performance evaluation results and optimization suggestions.

>Currently, SQL optimization is supported only for TencentDB for MySQL (excluding the Basic Edition).

## Optimizer Execution
1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/analysis), select **Diagnosis and Optimization** on the left sidebar, and select **SQL Optimization** at the top.
2. Select the target instance and name of the target database.
3. Enter (or paste) the specific SQL statements to be optimized in the input box and click **Format** to optimize the format.
4. Click **Diagnosis and Optimization** to view the SQL pre-execution details and optimization plan.
>
>- Make sure that the entered SQL statement is syntactically correct and the corresponding table exists in the target database.
>- The analysis does not actually execute the SQL statement and has no affect on the actual data in the database.
>- Currently, optimization plans are provided only for SELECT statements.
>
![](https://main.qcloudimg.com/raw/0972cc3a907812dfa899fcf61e2701ca.png)


## Optimization Suggestions
Professional optimization suggestions are provided for the entered SQL statement, including but not limited to index suggestions and SQL rewrite suggestions. You can optimize the SQL statement with performance problems using the optimization suggestions provided by DBbrain.
![](https://main.qcloudimg.com/raw/348644568ec5a739afad34c65b0d6ab7.png)
