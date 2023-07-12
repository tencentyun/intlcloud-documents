When users use the search page to analyze the logs, the search results may be empty or error messages may appear, such as `QueryError`, `SyntaxError`. The common problems and scenarios are summarized as below:

- [The page displays that the search result is empty](#question1)
- [Error messages appear for the search syntax](#question2)

### The page displays that the search result is empty[](id:question1)


- **Common reason 1:** the log was not collected successfully.
  **Solution:** for more information on troubleshooting, please see [Log Search Failure](https://intl.cloud.tencent.com/document/product/614/38446).

- **Common reason 2**: no wildcard is used when logs that contain only a part of the keyword segment are searched for.
  **Scenario:** you wanted to search for logs whose `user-agent` field contained `Window`, such as `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. After you entered the search statement `user-agent:Window`, the search result was empty. The reason is that `Window` is not a complete segment and cannot be searched separately.
  **Solution:** use wildcard `*` to search for `user-agent:Window*`.


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
<td align="left">Key-value index is not enabled for the query field `xxx`</td>
<td align="left">Enable key-value index for this field. For details, please see <a href="https://intl.cloud.tencent.com/document/product/614/39594">Key-Value Index</a></td>
</tr>
<tr>
<td align="left">QueryError [illegal_argument_exception.Cannot search on Full-Text since it is not indexed.]</td>
<td align="left">Full-text index is not enabled</td>
<td align="left">Enable full-text index for this field. For details, please see <a href="https://intl.cloud.tencent.com/document/product/614/39594">Full-Text Index</a></td>
</tr>
<tr>
<td align="left">QueryError [illegal_argument_exception.syntax error on field [and|or|not], or full text search is closed]</td>
<td align="left">The search condition does not support lowercase logical operators, which will be regarded as normal fields for full-text search</td>
<td align="left">Use the uppercase logical operators <code>AND|OR|NOT</code>. If you do not need to use logical operators but to search for <code>and/or/not</code>, please enable full-text index.</td>
</tr>
<tr>
<td align="left">QueryError [number_format_exception.For input string: "&gt;"]</td>
<td align="left">Syntax error of numerical comparison statement</td>
<td align="left">Check whether there are special symbols such as spaces around the numerical comparison symbols. An example of the correct format: <code>status:>400</code></td>
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
<td align="left">`cast` cannot convert dates in <code>13/Jul/2021:17:04:34</code> format. Only ISO standard format and millisecond-level UNIX timestamp are supported, e.g. <code>yyyy-MM-dd'T'HH:mm:ss.SSSZ</code> or <code>yyyy-MM-dd</code>.</td>
<td align="left">Modify the format of the time field or use the <code>__TIMESTAMP__</code> built-in field</td>
</tr>
<tr>
<td align="left">QueryError [verification_exception.Cannot order by non-grouped column [xxx], expected [xxx] or an aggregate function</td>
<td align="left">The statistics feature is not enabled for the field `xxx` and thus it cannot be used for sorting</td>
<td align="left">Enable statistics for this field. For details, please see <a href="https://intl.cloud.tencent.com/document/product/614/37803">Log Analysis Overview</a></td>
</tr>
<tr>
<td align="left">QueryError [verification_exception.Cannot use non-grouped column [xxx], expected [xxx]]</td>
<td align="left">The statistics feature is not enabled for the query field `xxx`</td>
<td align="left">Enable statistics for this field. For details, please see <a href="https://intl.cloud.tencent.com/document/product/614/37803">Log Analysis Overview</a></td>
</tr>
<tr>
<td align="left">QueryError [verification_exception.Field [xxx] of data type [text] cannot be used for grouping]</td>
<td align="left">The statistics feature is not enabled for the field `xxx` and thus it cannot be used for grouping</td>
<td align="left">Enable statistics for this field. For details, please see <a href="https://intl.cloud.tencent.com/document/product/614/37803">Log Analysis Overview</a></td>
</tr>
<tr>
<td align="left">QueryError [verification_exception.Unknown column [xxx]]</td>
<td align="left">The query field `xxx` does not exist</td>
<td align="left">Check whether the field name is correct</td>
</tr>
<tr>
<td align="left">QueryError [verification_exception.argument of [FUNCNAME(xxx)] must be [numeric], found value [xxx] type [text]]</td>
<td align="left">The type of the input parameter of the `FUNCNAME` function is incorrect. For example, if the `level` field of the `SUM(level)` function is of the text type, an error will be reported</td>
<td align="left">Check whether the field type meets the function requirements</td>
</tr>
<tr>
<td align="left">QueryError [query_shard_exception.Failed to parse query [xxx]]</td>
<td align="left">Syntax error of query statement</td>
<td align="left">Check the error position specified in the error information</td>
</tr>
<tr>
<td align="left">SyntaxError[xxx]</td>
<td align="left">There is a syntax error in part of the SQL statement</td>
<td align="left">Please see the detailed tips in the error message to fix the syntax error, where <code>line x,column x</code> does not contain the search condition part (i.e. "|" and the part before it)</td>
</tr>
<tr>
<td align="left">SearchTimeout</td>
<td align="left">The query timed out</td>
<td align="left">Reduce the scope of data query and SQL complexity as appropriate, or try again later.</td>
</tr>
<tr>
<td align="left">LimitExceeded.LogSearch</td>
<td align="left">The search concurrency exceeds the limit</td>
<td align="left">Try again later</td>
</tr>
</tbody></table>

