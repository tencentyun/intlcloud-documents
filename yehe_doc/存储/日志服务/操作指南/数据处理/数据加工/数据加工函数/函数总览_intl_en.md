CLS's data processing functions can be flexibly combined and used to cleanse, structure, filter, distribute, mask log data and more.
The figure below shows how a log containing JSON data is processed: the log data is processed and transformed into structured data, and then a field in the log is masked before the processed log is distributed.
![](https://qcloudimg.tencent-cloud.cn/raw/d4bd1388c816337acb35721847298263.png)

The following is an overview of data processing functions:
- **Key-value extraction functions**: extracting field-value pairs from log text
<table>
<tr><th style="width: 10%">Function</th><th style="width: 30%">Description</th><th style="width: 40%">Syntax Description</th><th style="width: 20%">Return Value Type</th></tr>
<tr><td>ext_sep</td><td>Extracts field value content based on a separator.</td><td>ext_sep("Source field name", "Target field 1,Target field 2,Target field...", sep="Separator", quote="Non-segmentation part"", restrict=False, mode="overwrite")</td><td>Log after extraction (LOG)</td></tr>
<tr><td>ext_sepstr</td><td>Extracts field value content based on specified characters (string).</td><td>ext_sepstr("Source field name","Target field 1,Target field 2,Target field...", sep="abc", restrict=False, mode="overwrite")</td><td>Log after extraction (LOG)</td></tr>
<tr><td>ext_json</td><td>Extracts field values from JSON data.</td><td>Log after extraction (LOG)
	ext_json("Source field name",prefix="",suffix="",format="full",exclude_node="JSON nodes not to expand")</td><td>Log after extraction (LOG)</td></tr>
<tr><td>ext_json_jmes</td><td>Extracts a field value based on a JMES expression.</td><td>ext_json_jmes("Source field name", jmes= "JSON extraction expression", output="Target field", ignore_null=True, mode="overwrite")</td><td>Log after extraction (LOG)</td></tr>
<tr><td>ext_kv</td><td>Extracts field values by using two levels of separators.</td><td>ext_kv("Source field name", pair_sep=r"\s", kv_sep="=", prefix="", suffix="", mode="fill-auto")</td><td>Log after extraction (LOG)</td></tr>
<tr><td>ext_regex</td><td>Extracts field values by using a regular expression.</td><td>ext_regex("Source field name", regex="Regular expression", output="Target field 1,Target field 2,Target field...", mode="overwrite")</td><td>Log after extraction (LOG)</td></tr>
<tr><td>ext_first_notnull</td><td>Returns the first non-null and non-empty result value.</td><td>ext_first_notnull(Value 1,Value 2,...)</td><td>	The first non-null result value</td></tr>
</table>
- **Enrichment functions**: Adding fields to existing fields according to rules
<table>
<tr><th style="width: 10%">Function</th><th style="width: 30%">Description</th><th style="width: 40%">Syntax Description</th><th style="width: 20%">Return Value Type</th></tr>
<tr><td>enrich_table</td><td>Uses CSV structure data to match fields in logs and, when matched fields are found, the function adds other fields and values in the CSV data to the source logs.</td><td>enrich_table("CSV source data", "CSV enrichment field", output="Target field 1,Target field 2,Target field....", mode="overwrite")</td><td>Mapped log (LOG)</td></tr>
<tr><td>enrich_dict</td><td>Uses dict structure data to match a field value in a log. If the specified field and value match a key in the dict structure data, the function assigns the value of the key to another field in the log.</td><td>enrich_dict("JSON dictionary", "Source field name", output=Target field name, mode="overwrite")</td><td>Mapped log (LOG)</td></tr>
</table>
- **Flow control functions**: condition determination
<table>
<tr><th style="width: 10%">Function</th><th style="width: 30%">Description</th><th style="width: 40%">Syntax Description</th><th style="width: 20%">Return Value Type</th></tr>
<tr><td>compose</td><td>Combines multiple operation functions. Providing combination capabilities similar to those of branch code blocks, this function can combine multiple operation functions and execute them in sequence. It can be used in combination with branches and output functions.</td><td>compose("Function 1","Function 2", ...)</td><td>Log (LOG)</td></tr>
<tr><td>t_if</td><td>Executes a corresponding function if a condition is met and does not perform any processing if the condition is not met.</td><td>t_if("Condition", Function)</td><td>Log (LOG)</td></tr>
<tr><td>t_if_not</td><td>Executes a corresponding function if a condition is not met and does not perform any processing if the condition is met.</td><td>t_if_not("Condition",Function)</td><td>Log (LOG)</td></tr>
<tr><td>t_if_else</td><td>Executes a function based on the evaluation result of a condition.</td><td>t_if_else("Condition", Function 1, Function 2)</td><td>Log (LOG)</td></tr>
<tr><td>t_switch</td><td>Executes different functions depending on whether branch conditions are met. If all conditions are not met, the data is deleted.</td><td>t_switch("Condition 1", Function 1, "Condition 2", Function 2, ...)</td><td>Log (LOG)</td></tr>
</table>
- **Row processing functions**: log distribution, deletion, and splitting
<table>
<tr><th style="width: 10%">Function</th><th style="width: 30%">Description</th><th style="width: 40%">Syntax Description</th><th style="width: 20%">Return Value Type</th></tr>
<tr><td>log_output</td><td>Outputs a row of log to a specified log topic. This function can be used independently or together with branch conditions.</td><td>log_output(Log topic alias) (The alias here is the target log topic alias specified when the data processing task is created.)</td><td>No return value</td></tr>
<tr><td>log_split</td><td>Splits a row of log into multiple rows of logs based on the value of a specified field by using a separator and JMES expression.</td><td>log_split(Field name, sep=",", quote="\"", jmes="", output="")</td><td>Log (LOG)</td></tr>
<tr><td>log_drop</td><td>Deletes logs that meet a specified condition.</td><td>log_drop(Condition 1)</td><td>Log (LOG)</td></tr>
<tr><td>log_keep</td><td>Retains logs that meet a specified condition.</td><td>log_keep(Condition 1)</td><td>Log (LOG)</td></tr>
<tr><td>log_split_jsonarray_jmes</td><td>Splits and expands the JSON array in the log according to JMES syntax.</td><td>log_split_jsonarray_jmes("field", jmes="items", prefix="")</td><td>Log (LOG)</td></tr>
</table>
- **Field processing functions**: field Create/Read/Update/Delete/Rename
<table>
<tr><th style="width: 10%">Function</th><th style="width: 30%">Description</th><th style="width: 40%">Syntax Description</th><th style="width: 20%">Return Value Type</th></tr>
<tr><td>fields_drop</td><td>Deletes the fields that meet a specified condition.</td><td>fields_drop(Field name 1, Field name 2, ..., regex=False,nest=False)</td><td>Log (LOG)</td></tr>
<tr><td>fields_keep</td><td>Retains the fields that meet a specified condition.</td><td>fields_keep(Field name 1, Field name 2, ..., regex=False)</td><td>Log (LOG)</td></tr>
<tr><td>fields_pack</td><td>Matches field names based on a regular expression and encapsulates the matched fields into a new field whose value is in JSON format.</td><td>fields_pack(Target field name, include=".*", exclude="", drop_packed=False)</td><td>Log (LOG)</td></tr>
<tr><td>fields_set</td><td>Sets field values or adds fields.</td><td>fields_set(Field name 1, Field value 1, Field name 2, Field value 2, mode="overwrite")</td><td>Log (LOG)</td></tr>
<tr><td>fields_rename</td><td>Renames fields.</td><td>fields_rename(Field name 1, New field name 1, Field name 2, New field name 2, regex=False)</td><td>Log (LOG)</td></tr>
<tr><td>has_field</td><td>If the specified field exists, returns `True`. Otherwise, returns `False`.</td><td>has_field(Field name)</td><td>Condition value (BOOL)</td></tr>
<tr><td>not_has_field</td><td>If the specified field does not exist, returns `True`. Otherwise, returns `False`.</td><td>not_has_field(Field name)</td><td>Condition value (BOOL)</td></tr>
<tr><td>v</td><td>Gets the value of a specified field and returns the corresponding string.</td><td>v(Field name)</td><td>Value string type (STRING)</td></tr>
</table>			
- **Value structuring functions**: JSON data processing
<table>
<tr><th style="width: 10%">Function</th><th style="width: 30%">Description</th><th style="width: 40%">Syntax Description</th><th style="width: 20%">Return Value Type</th></tr>
<tr><td>json_select</td><td>Extracts a JSON field value with a JMES expression and returns the JSON string of the extraction result.</td><td>json_select(v(Field name), jmes="")</td><td>Value string type (STRING)</td></tr>
<tr><td>xml_to_json</td><td>Parses and converts an XML-formatted value to a JSON string. The input value must be an XML string. Otherwise, a conversion exception will occur.</td><td>xml_to_json(Field value)</td><td>Value string type (STRING)</td></tr>
<tr><td>json_to_xml</td><td>Parses and converts a JSON string value to an XML string.</td><td>json_to_xml(Field value)</td><td>Value string type (STRING)</td></tr>
<tr><td>if_json</td><td>Checks whether a value is a JSON string.</td><td>if_json(Field value)</td><td>Condition value (BOOL)</td></tr>
</table>
- **Regular expression functions**: matching and replacing characters in text by using regular expressions				
<table>
<tr><th style="width: 10%">Function</th><th style="width: 30%">Description</th><th style="width: 40%">Syntax Description</th><th style="width: 20%">Return Value Type</th></tr>
<tr><td>regex_match</td><td>Matches data in full or partial match mode based on a regular expression and returns whether the match is successful.</td><td>regex_match(Field value, regex="", full=True)</td><td>Condition value (BOOL)</td></tr>
<tr><td>regex_select</td><td>Matches data based on a regular expression and returns the corresponding partial match result. You can specify the sequence number of the matched expression and the sequence number of the group to return (partial match + sequence number of the specified matched group). If no data is matched, an empty string is returned.</td><td>regex_select(Field value, regex="", index=1, group=1)</td><td>Value string type (STRING)</td></tr>
<tr><td>regex_split</td><td>Splits a string and returns a JSON array of the split strings (partial match).</td><td>regex_split(Field value, regex=\"\", limit=100)</td><td>Value string type (STRING)</td></tr>
<tr><td>regex_replace</td><td>Matches data based on a regular expression and replaces the matched data (partial match).</td><td>regex_replace(Field value, regex="", replace="", count=0)</td><td>Value string type (STRING)</td></tr>
<tr><td>regex_findall</td><td>Matches data based on a regular expression and returns a JSON array of the matched data (partial match).</td><td>regex_findall(Field value, regex="")</td><td>Value string type (STRING)</td></tr>
</table>
- **Date value processing functions**
<table>
<tr><th style="width: 10%">Function</th><th style="width: 30%">Description</th><th style="width: 40%">Syntax Description</th><th style="width: 20%">Return Value Type</th></tr>
<tr><td>dt_str</td><td>Converts a time field value (a date string in a specific format or timestamp) to a target date string of a specified time zone and format.</td><td>dt_str(Value, format="Formatted string", zone="")</td><td>STRING</td></tr>
<tr><td>dt_to_timestamp</td><td>Converts a time field value (a date string in a specified format; time zone specified) to a UTC timestamp.</td><td>dt_to_timestamp(Value, zone="")</td><td>STRING</td></tr>
<tr><td>dt_from_timestamp</td><td>Converts a timestamp field value to a time string in the specified time zone.</td><td>dt_from_timestamp(Value, zone="")</td><td>STRING</td></tr>
<tr><td>dt_now</td><td>Obtains the current datetime of the processing calculation.</td><td>dt_now(format="Formatted string", zone="")</td><td>STRING</td></tr>
</table>
- **String processing functions**
<table>
<tr><th style="width: 10%">Function</th><th style="width: 30%">Description</th><th style="width: 40%">Syntax Description</th><th style="width: 20%">Return Value Type</th></tr>
<tr><td>str_count</td><td>Searches for a substring in a specified range of a value and returns the number of occurrences of the substring.</td><td>str_count(Value, sub="", start=0, end=-1)</td><td>INT</td></tr>
<tr><td>str_len</td><td>Returns the length of a string.</td><td>str_len(Value)</td><td>INT</td></tr>
<tr><td>str_uppercase</td><td>Converts a string to uppercase.</td><td>str_uppercase(Value)</td><td>STRING</td></tr>
<tr><td>str_lowercase</td><td>Converts a string to lowercase.</td><td>str_lowercase(Value)</td><td>STRING</td></tr>
<tr><td>str_join</td><td>Concatenates input values by using a concatenation string.</td><td>str_join(Concatenation string 1, Value 1, Value 2, ...)</td><td>STRING</td></tr>
<tr><td>str_replace</td><td>Replaces an old string with a new string.</td><td>str_replace(Value, old="", new="", count=0)</td><td>STRING</td></tr>
<tr><td>str_format</td><td>Formats strings.</td><td>str_format(Formatting string, Value 1, Value 2, ...)</td><td>STRING</td></tr>
<tr><td>str_strip</td><td>Deletes specified characters from a string concurrently from the start and end of the string, and returns the remaining part.</td><td>str_strip(Value, chars="\t\r\n")</td><td>STRING</td></tr>
<tr><td>str_lstrip</td><td>Deletes specified characters from a string from the start of the string, and returns the remaining part.</td><td>str_strip(Value, chars="\t\r\n")</td><td>STRING</td></tr>
<tr><td>str_rstrip</td><td>Deletes specified characters from a string from the end of the string, and returns the remaining part.</td><td>str_strip(Value, chars="\t\r\n")</td><td>STRING</td></tr>
<tr><td>str_find</td><td>Checks whether a string contains a specified substring and returns the position of the first occurrence of the substring in the string.</td><td>str_find(Value, sub="", start=0, end=-1)</td><td>INT</td></tr>
<tr><td>str_start_with</td><td>Checks whether a string starts with a specified string.</td><td>str_start_with(Value, sub="", start=0, end=-1)</td><td>BOOL</td></tr>
<tr><td>str_end_with</td><td>Checks whether a string ends with a specified string.</td><td>str_end_with(Value, sub="", start=0, end=-1)</td><td>BOOL</td></tr>
</table>
- **Logical expression functions**
<table>
<tr><th style="width: 10%">Function</th><th style="width: 30%">Description</th><th style="width: 40%">Syntax Description</th><th style="width: 20%">Return Value Type</th></tr>
<tr><td>op_if</td><td>Returns a value based on a specified condition.</td><td>op_if(Condition 1, Value 1, Value 2)</td><td>If the condition is `true`, `Value 1` is returned; otherwise, `Value 2` is returned.</td></tr>
<tr><td>op_and</td><td>Performs the AND operation on values. If all the specified parameter values are evaluated to true, `True` is returned; otherwise, `False` is returned. </td><td>op_and(Value 1, Value 2, ...)</td><td>BOOL</td></tr>
<tr><td>op_or</td><td>Performs the OR operation on values. If one or more of the specified parameter values are evaluated to false, `False` is returned; otherwise, `True` is returned.</td><td>op_or(Value 1, Value 2, ...)</td><td>BOOL</td></tr>
<tr><td>op_not</td><td>Performs the NOT operation on values.</td><td>op_not(Value)</td><td>BOOL</td></tr>
<tr><td>op_eq</td><td>Compares two values. If the values are equal, `True` is returned.</td><td>op_eq(Value 1, Value 2)</td><td>BOOL</td></tr>
<tr><td>op_ge</td><td>Compares two values. If `Value 1` is greater than or equal to `Value 2`, `True` is returned.</td><td>op_ge(Value 1, Value 2)</td><td>BOOL</td></tr>
<tr><td>op_gt</td><td>Compares two values. If `Value 1` is greater than `Value 2`, `True` is returned.</td><td>op_gt(Value 1, Value 2)</td><td>BOOL</td></tr>
<tr><td>op_le</td><td>Compares two values. If `Value 1` is less than or equal to `Value 2`, `True` is returned.</td><td>op_le(Value 1, Value 2)</td><td>BOOL</td></tr>
<tr><td>op_lt</td><td>Compares two values. If `Value 1` is less than `Value 2`, `True` is returned.</td><td>op_lt(Value 1, Value 2)</td><td>BOOL</td></tr>
<tr><td>op_add</td><td>Returns the sum of two specified values.</td><td>op_add(Value 1, Value 2)</td><td>Calculation result</td></tr>
<tr><td>op_sub</td><td>Returns the difference between two specified values.</td><td>op_sub(Value 1, Value 2)</td><td>Calculation result</td></tr>
<tr><td>op_mul</td><td>Returns the product of two specified values.</td><td>op_mul(Value 1, Value 2)</td><td>Calculation result</td></tr>
<tr><td>op_div</td><td>Returns the quotient of two specified values.</td><td>op_div(Value 1, Value 2)</td><td>Calculation result</td></tr>
<tr><td>op_sum</td><td>Returns the sum of multiple specified values.</td><td>op_sum(Value 1, Value 2, ...)</td><td>Calculation result</td></tr>
<tr><td>op_mod</td><td>Returns the remainder of a specified value divided by the other specified value.</td><td>op_mod(Value 1, Value 2)</td><td>Calculation result</td></tr>
<tr><td>op_null</td><td>Checks whether a value is `null`. If so, `true` is returned; otherwise, `false` is returned.</td><td>op_null(Value)</td><td>BOOL</td></tr>
<tr><td>op_notnull</td><td>Checks whether a value is not `null`. If so, `true` is returned; otherwise, `false` is returned.</td><td>op_notnull(Value)</td><td>BOOL</td></tr>
<tr><td>op_str_eq</td><td>Compares string values. If they are equal to each other, `true` is returned.</td><td>op_str_eq(Value 1, Value 2, ignore_upper=False)</td><td>BOOL</td></tr>
</table>
- **Type conversion functions**
<table>
<tr><th style="width: 10%">Function</th><th style="width: 30%">Description</th><th style="width: 40%">Syntax Description</th><th style="width: 20%">Return Value Type</th></tr>
<tr><td>ct_int</td><td>Converts a value (whose base can be specified) to a decimal integer.</td><td>ct_int(Value 1, base=10)</td><td>Calculation result</td></tr>
<tr><td>ct_float</td><td>Converts a value to a floating-point number.</td><td>ct_float(Value)</td><td>Calculation result</td></tr>
<tr><td>ct_str</td><td>Converts a value to a string.</td><td>ct_str(Value)</td><td>Calculation result</td></tr>
<tr><td>ct_bool</td><td>Converts a value to a Boolean value.</td><td>ct_bool(Value)</td><td>Calculation result</td></tr>
</table>
- **Encoding/Decoding functions**
<table>
<tr><th style="width: 10%">Function</th><th style="width: 30%">Description</th><th style="width: 40%">Syntax Description</th><th style="width: 20%">Return Value Type</th></tr>
<tr><td>decode_url</td><td>Decodes an encoded URL.</td><td>decode_url(Value)</td><td>STRING</td></tr>
</table>
- **IP parsing functions**
<table>
<tr><th style="width: 10%">Function</th><th style="width: 30%">Description</th><th style="width: 40%">Syntax Description</th><th style="width: 20%">Return Value Type</th></tr>
<tr><td>geo_parse</td><td>Parses the geographical location.</td><td>geo_parse(Field value, keep=("country","province","city"), ip_sep=",")</td><td>JSON string	</td></tr>
</table>

​			
​			
​			
