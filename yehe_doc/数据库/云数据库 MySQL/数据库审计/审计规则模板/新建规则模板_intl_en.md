This document describes how to create a rule template in the console.
>?
>- A rule template can be used to initialize the audit rule for an instance. When a rule template is bound to an instance, the audit rules already applied to the instance remain effective even after the template is modified.
>- A rule template allows up to 5 characteristic strings for a single parameter field, with each string being separated by vertical bar "|".

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/instance).
2. On the left sidebar, click **Database Audit**.
3. Select **Region** and click **Rule Template**.
4. In the template list, click **Create Rule Template**.
5. In the **Create Rule Template** window, set the following configuration items and click **OK**.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Rule Template Name</td>
<td>This field can contain up to 30 letters, digits, and symbols (-_./()[]+=:@) and cannot start with a digit.</td></tr>
<tr>
<td>Rule Content</td>
<td>Set the rule content, including parameter field, operator, and characteristic string. For more information on settings, see <strong>Rule content details and example</strong> below. <blockquote class="rno-document-tips rno-document-tips-notice">    <div class="rno-document-tips-body">        <i class="rno-document-tip-icon"></i>        <div class="rno-document-tip-title">Note</div>        <div class="rno-document-tip-desc"><ul><li>In **Rule Content**, you can click <strong>Add</strong> to add up to 5 parameter fields. </li><li>You can click <strong>Delete</strong> in the <strong>Operation</strong> column to delete an unwanted parameter field and condition. However, you must retain at least one parameter field and condition.</li></ul></div>    </div></blockquote></td></tr>
<tr>
<td>Rule Template Remarks</td>
<td>This field can contain up to 200 letters, digits, and symbols (-_./()[]+=:@) and cannot start with a digit.</td></tr>
</tbody></table>

## Rule content details and examples(id:GZNRXQJSL)
>?
>- You can configure one or multiple rules. Up to 5 rules can be configured.
>- Different rules are in **AND** relationship; that is, they need to be met at the same time.
>- Different characteristic strings in a rule are in **OR** relationship; that is, at least one of them needs to be met.
>- You can add only one operator for the same parameter field; for example, for the database name, the operator can be either **Include** or **Exclude**.

<table>
<thead><tr><th>Parameter Field</th><th>Operator</th><th>Characteristic String</th></tr>
</thead>
<tbody><tr>
<td>Client IP</td>
<td>Include, Exclude, Equal to, Not equal to, Regex</td>
<td>Up to five client IPs can be configured and should be separated by vertical bar "|". When the operator is `Regex`, only one characteristic string can be filled in.</td></tr>
<tr>
<td>Username</td>
<td>Include, Exclude, Equal to, Not equal to, Regex</td>
<td>Up to five usernames can be configured and should be separated by vertical bar "|". When the operator is `Regex`, only one characteristic string can be filled in.</td></tr>
<tr>
<td>Database Name</td>
<td>Include, Exclude, Equal to, Not equal to, Regex</td>
<td>Up to five database names can be configured and should be separated by vertical bar "|". When the operator is `Regex`, only one characteristic string can be filled in.</td></tr>
<tr>
<td>SQL Details</td>
<td>Include, Exclude</td>
<td>Up to five SQL commands can be configured and should be separated by vertical bar "|". When the operator is `Regex`, only one characteristic string can be filled in.</td></tr>
<tr>
<td>SQL Type</td>
<td>Equal to, Not equal to</td>
<td>Up to five SQL types can be selected. Valid options: ALTER, CHANGEUSER, CREATE, DELETE, DROP, EXECUTE, INSERT, LOGIN, LOGOUT, REPLACE, SELECT, SET, UPDATE, Other.</td></tr>
<tr>
<td>Affected Rows</td>
<td>Greater than, Less than</td>
<td>Select the number of affected rows</td>
<tr>
<td>Returned Rows</td>
<td>Greater than, Less than</td>
<td>Select the number of returned rows</td></tr>
<tr>
<td>Scanned Rows</td>
<td>Greater than, Less than</td>
<td>Select the number of scanned rows</td></tr>
<tr>
<td>Execution Time</td>
<td>Greater than, Less than</td>
<td>Select the execution time in microseconds</td>
</tbody></table>
<b>Example</b>: If the following rule content is set: the database name should include `a`, `b`, or `c`, and the client IP should include IP1, 2 or 3, then the audit logs filtered by the rule are those where the database name includes `a`, `b`, or `c` and the client IP includes IP1, 2, or 3.
