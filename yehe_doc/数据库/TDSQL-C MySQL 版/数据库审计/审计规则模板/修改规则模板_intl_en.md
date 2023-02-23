This document describes how to modify a database audit rule template in the console.
>?
>- A rule template can be used to initialize the audit rule for an instance. When a rule template is bound to an instance, the audit rules already applied to the instance remain effective even after the template is modified.
>- A rule template allows up to 5 characteristic strings for a single parameter field, with each string being separated by vertical bar "|".

## Directions
1. Log in to the [TDSQL-C for MySQL console](https://console.cloud.tencent.com/cynosdb/mysql#/).
2. On the left sidebar, click **Database Audit**.
3. Select a region and click **Rule Template**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/ZKbg949_11.png)
4. Find the target rule template in the rule template list, or search for it by resource attribute in the search box, and click **Edit** in the **Operation** column.
5. In the **Edit Rule Template** window, modify configuration items and click **OK**.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/6i8Q099_12.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Rule Template Name</td>
<td>This field can contain up to 30 letters, digits, and symbols <code>-_./()[]+=:@</code> and cannot start with a digit.</td></tr>
<tr>
<td>Rule Content</td>
<td>Set the rule content, including parameter field, operator, and characteristic string. For more information on settings, see <strong>Rule content details and example</strong> below. <blockquote class="rno-document-tips rno-document-tips-notice">    <div class="rno-document-tips-body">        <i class="rno-document-tip-icon"></i>        <div class="rno-document-tip-title">Note</div>        <div class="rno-document-tip-desc"><ul><li>In **Rule Content**, you can click <strong>Add</strong> to add a parameter field. </li><li>You can click <strong>Delete</strong> in the <strong>Operation</strong> column to delete an unwanted parameter field and condition. However, you must retain at least one parameter field and condition.</li></ul></div>    </div></blockquote></td></tr>
<tr>
<td>Rule Template Remarks</td>
<td>This field can contain up to 200 letters, digits, and symbols <code>-_./()[]+=:@</code> and cannot start with a digit.</td></tr>
</tbody></table>

## Rule content details and examples
>?
>- You can configure one or multiple rules.
>- Different rules are in AND relationship; that is, they need to be met at the same time.
>- Different characteristic strings in a rule are in OR relationship; that is, at least one of them needs to be met.
>- You can add only one operator for the same parameter field; for example, for the database name, the operator can be either **Include** or **Exclude**.

| Parameter Field | Operator | Characteristic String |
|---------|---------|---------|
| Client IP | Include, Exclude, Equal to, Not equal to | Up to five client IPs can be configured and should be separated by vertical bar "|". |
| Username | Include, Exclude, Equal to, Not equal to | Up to five usernames can be configured and should be separated by vertical bar "|". |
| Database Name | Include, Exclude, Equal to, Not equal to | Up to five database names can be configured and should be separated by vertical bar "|". |
| SQL Details | Include, Exclude, Equal to, Not equal to | Up to five SQL commands can be configured and should be separated by vertical bar "|". |
| SQL Type | Include, Exclude | Up to five SQL types can be selected. Valid options: ALTER, CHANGEUSER, CREATE, DELETE, DROP, EXECUTE, INSERT, LOGIN, LOGOUT, REPLACE, SELECT, SET, UPDATE, Other. |

**Example**
If the following rule content is set: the database name should include `a`, `b`, or `c`, and the client IP should include IP1, 2 or 3, then the audit logs filtered by the rule are those where the database name includes `a`, `b`, or `c` and the client IP includes IP1, 2, or 3.

