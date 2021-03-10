When you use the search page to search for and analyze logs, you may encounter error messages, such as "An error occurred while parsing the query statement. Please check the syntax and enter the correct statement.", or may fail to query the correct log information for configuration or syntax reasons. CLS summarizes the following common problems and provides solutions in specified use cases:

- [Page display: The current search result is empty.](#question1)
- [Error message: The query statement failed to run. Please check the index configuration and query statement.](#question2)
- [Error message: An error occurred while parsing the query statement. Please check the syntax and enter the correct statement.](#question3)

<span id="question1"></span>

### What should I do if the current search result is empty?

- **Common reason 1:** the log was not collected successfully.
  **Solution:** for more information on troubleshooting, please see [Log Search Failure](https://intl.cloud.tencent.com/document/product/614/38446).

- **Common reason 2**: no wildcard is used when logs that contain only a part of the keyword segment are searched for.
  **Scenario:** you wanted to search for logs whose `user-agent` field contained `Window`, such as `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`. After you entered the search statement `user-agent:Window`, the search result was empty. The reason is that `Window` is not a complete segment and cannot be searched separately.
  **Solution:** use wildcard `*` to search for `user-agent:*Window*`.

- **Common reason 3:** an SQL statement is used to analyze log data, but spaces are not added before and after the pipe symbol.
  **Scenario:** the SQL statement you entered was `*|Select * `. As you didn't add spaces before and after the pipe symbol, CLS used the entire statement as a keyword for full-text search for log data containing "`*|Select *`".
  **Solution:** add spaces before and after the pipe symbol.

<span id="question2"></span>

### What should I do if the query statement failed to run?

- **Common reason 1:** during key-value search, the field value to be searched is not configured with a key-value index.
  **Scenario:** when you searched for logs with an IP of 10.8.1.1 in the IP field by using the search statement `remote_addr:10.8.1.1`, an error was reported. The reason is that when key-value search is used, the corresponding field needs to be configured with a key-value index.
  **Solution:** go to the key-value index configuration at the top-right of the search page and change the key value.

- **Common reason 2:** the field value contains special characters such as `+ - && || ! ( ) { } [ ] ^ " ~ * ? : \`.
  **Scenario:** you filtered logs by the client version `user-agent` with the search statement `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1)`.
  **Solution:** use double quotation marks to search for the field value as a complete phrase, such as `"Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1)"`.

<span id="question3"></span>

### What should I do if an error occurred while parsing the query statement?

- **Common reason 1:** the SQL statement syntax is incorrect, or syntactically reserved words (such as `select` and `order`) are misspelled. For more information on the reserved words, please see [Overview](https://intl.cloud.tencent.com/document/product/614/37803).
- **Common reason 2:** when the SELECT statement is performed on fields, the fields are not separated by comma, such as `select ip  count(*) group by ip`. `ip` and `count(\*)` should be separated by comma, and the correct statement should be `select ip ,count(*) group by ip`.













