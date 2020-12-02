The SQL optimization feature provides you with one-click SQL statement optimization and the corresponding execution plan modification and optimization advice. SQL optimization is suitable for scenarios such as slow SQL statement optimization, pre-release code review, and self-check.

This feature provides expert advice about SQL optimization and supports many database management features, including viewing database table structures or executing/modifying SQL statements in the console. It helps you optimize all aspects of SQL statements and allows you to operate databases the same way as you do in a database client tool.

You can manually enter SQL statements and analyze them to get their performance evaluation results and optimization advice.

>?Currently, SQL optimization is supported for TencentDB for MySQL (excluding the Basic Edition) and TencentDB for CynosDB (compatible with MySQL).

## Optimizer Execution
1. Log in to the [DBbrain Console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database at the top and select the **SQL Optimization** tab.
2. On this tab, you can view information about database tables, SQL statements, and SQL execution.
 - The left section displays databases, tables, fields, and indexes. You can filter a database by its name and click **Table Structure** next to a table to show its structure.
 - The right section displays SQL details. You can filter data by "Database", "Table", or "Type", and show data in the "Table" or "DDL" mode.

3. In the execution panel, you can enter or paste SQL statements to execute them, format them, clear them, view their execution plans and optimization advice. You can cancel or redo your actions.

 - Click **Monitoring Details** on the right to view database monitoring details.
 - Click **Settings** on the right to view query settings, including execution timeout period and the maximum number of returned rows.
 - Click **Common Commands** on the right to view OPS SQL templates, including parameter/metric templates. user templates, information_schema templates, and other templates. These templates help you execute common OPS SQL statements easily and quickly.
 - Click **Execute** to execute SQL statements. You can view execution results and history, and clear the history.

 - Select the **Execution History** tab to view the SQL execution history of the current session or all sessions.

 - Click the "Execution Plan" icon to view details about SQL execution plans.

 - Click the "Format" icon to format SQL statements. 

 - Click the "Optimization Advice" icon to view optimization advice for SQL statements.

In the "Optimization Comparison" window, you can view the execution plans and costs of SQL statements, table structures, and advice in indexes and rewriting. You can view the change of SQL costs before and after optimization in a visual chart.
  The costs of optimized SQL statements are estimated based on the analysis of the statistics of database tables related to the statements, the OPTIMIZER_SWITCH configuration, and the index selectivity. A chart is used to visually show the decrease in the costs of optimized SQL statements. You can also compare the execution plans before and after the SQL optimization to further verify the optimization results.


