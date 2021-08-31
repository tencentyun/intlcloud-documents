When users use the search page to analyze the logs, the search results may be empty or error messages may appear, such as `QueryError`, `SyntaxError`. The common problems and scenarios are summarized as below:

- [The page displays that the search result is empty](#question1)
- [Error messages appear for the search syntax](#question2)

### The page displays that the search result is empty[](id:question1)



- **Common reason 1:** the log was not collected successfully.
  **Solution:** for more information on troubleshooting, please see [Log Search Failure](https://intl.cloud.tencent.com/document/product/614/38446).

- **Common reason 2**: no wildcard is used when logs that contain only a part of the keyword segment are searched for.
  **Scenario:** you wanted to search for logs whose `user-agent` field contained `Window`, such as `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. After you entered the search statement `user-agent:Window`, the search result was empty. The reason is that `Window` is not a complete segment and cannot be searched separately.
  **Solution:** use wildcard `*` to search for `user-agent:Window*`.

- **Common reason 3:** an SQL statement is used to analyze log data, but spaces are not added before and after the pipe symbol.
  **Scenario:** the SQL statement you entered was `*|SELECT * `. As you didn't add spaces before and after the pipe symbol, CLS used the entire statement as a keyword for full-text search for log data containing "`*|SELECT *`".
  **Solution:** Add a space before and after the pipe character, e.g. `*|SELECT *`.

### Query statement with error message [](id:question2)

Common error messages, causes and solutions are as follows:


<table>
<thead>
<tr>
<th align="left">Error Message</th>
<th align="left">Cause</th>
<th align="left">Solution</th>
</tr>
</thead>
<tbody><tr>
<td align="left">QueryError [illegal_argument_exception.Cannot search on field [xxx] since it is not indexed</td>
<td align="left">The index is not enabled for the queried field `xxx`</td>
<td align="left">Enable the index for this field. For details, please see <a href="https://intl.cloud.tencent.com/document/product/614/39594#.E9.94.AE.E5.80.BC.E7.B4.A2.E5.BC.95">Configuring Index</a></td>
</tr>
<tr>
<td align="left">QueryError [illegal_argument_exception.Cannot search on Full-Text since it is not indexed.]</td>
<td align="left">Full-text index is not enabled</td>
<td align="left">Enable the full-text index. For details, please see <a href="https://intl.cloud.tencent.com/document/product/614/39594#.E9.94.AE.E5.80.BC.E7.B4.A2.E5.BC.95">Full-Text Index</a></td>
</tr>
<tr>
<td align="left">QueryError [illegal_argument_exception.syntax error on field [and|or|not], or full text search is closed]</td>
<td align="left">The search condition does not support lowercase logical operators, which will be regarded as normal fields for full-text search</td>
<td align="left">Use the upper-case logical operators <code>AND|OR|NOT<code>. If you do not need to use logical operators but to search for <code>and/or/not</code>, please enable full-text index.</td>
</tr>
<tr>
<td align="left">QueryError [number_format_exception.For input string: "&gt;"]</td>
<td align="left">Syntax error of numerical comparison statement</td>
<td align="left">Check whether there are special symbols such as spaces around the numerical comparison symbols. An example of correct format: <code>status:>400</code></td>
</tr>
<tr>
<td align="left">QueryError [parent_circuit_breaking_exception.[parent] Data too large, data for [<transport_request>] would be [xxx/xxxgb]</transport_request></td>
<td align="left">The query data volume is too large</td>
<td align="left">Reduce the query time range as appropriate, and specify more precise query conditions</td>
</tr>
<tr>
<td align="left">QueryError [parse_exception.parse_exception: Cannot parse 'xxx': '*' or '?' not allowed as first character in WildcardQuery</td>
<td align="left">Fuzzy query by prefix is not allowed, e.g. content:*example<code>content:*example</code></td>
<td align="left">We recommend using separators to split a field into multiple ones. For details, please see <a href="https://intl.cloud.tencent.com/document/product/614/39594">Configuring Index</a></td>.
</tr>
<tr>
<td align="left">QueryError [sql_illegal_argument_exception.cannot cast [13/Jul/2021:17:04:34] to [datetime]: failed to parse date field [13/Jul/2021:17:04:34] with format [date_optional_time]]</td>
<td align="left">`cast` cannot convert dates in `13/Jul/2021:17:04:34` format. Only ISO standard format and millisecond-level Unix timestamp are supported, e.g. <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code> or <code>yyyy-MM-dd</code>.
<td align="left">Modify the format of the time field or use the <code>__TIMESTAMP__</code> built-in field</td>
</tr>
<tr>
<td align="left">QueryError [verification_exception.Cannot order by non-grouped column [xxx], expected [xxx] or an aggregate function</td>
<td align="left">Statistics is not enabled for the field `xxx` and thus it cannot be used for sorting</td>
<td align="left">Enable statistics for this field. For details, please see <a href="https://intl.cloud.tencent.com/document/product/614/37803">Log Analysis Overview</a></td>
</tr>
<tr>
<td align="left">QueryError [verification_exception.Cannot use non-grouped column [xxx], expected [xxx]]</td>
<td align="left">Statistics is not enabled for the query field `xxx`</td>
<td align="left">Enable statistics for this field. For details, please see <a href="https://intl.cloud.tencent.com/document/product/614/37803">Log Analysis Overview</a></td>
</tr>
<tr>
<td align="left">QueryError [verification_exception.Field [xxx] of data type [text] cannot be used for grouping]</td>
<td align="left">Statistics is not enabled for the field `xxx` and thus it cannot be used for grouping</td>
<td align="left">Enable statistics for this field. For details, please see <a href="https://intl.cloud.tencent.com/document/product/614/37803">Log Analysis Overview</a></td>
</tr>
<tr>
<td align="left">QueryError [verification_exception.Unknown column [xxx]]</td>
<td align="left">The query field `xxx` does not exist</td>
<td align="left">Check whether the field name is correct</td>
</tr>
<tr>
<td align="left">SyntaxError[xxx]</td>
<td align="left">There is a syntax error in part of the SQL statement</td>
<td align="left">Please see the detailed tips in the error message to fix the syntax error, where <code>line x,column x</code> does not contain the search condition part (i.e. "|" and the part before it)
</tr>
<tr>
<td align="left">SearchTimeout</td>
<td align="left">The query is timed out</td></tr>
<td align="left">Reduce the scope of data query and SQL complexity as appropriate, or try again later.</td>
</tr>
<tr>
<td align="left">LimitExceeded.LogSearch</td>
<td align="left">The search concurrency exceeds the limit</td>
<td align="left">Try again later</td>
</tr>
</tbody></table>

