To make it easier for users experienced in Java to connect to iPaaS, the Dataway code mode supports Java scripts.

## Use of IDE

1. Hover over any Dataway textbox, and the mode selection buttons will pop up automatically. Click **Code** to enter the code mode.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/YS74534_1.png)
2. Click the textbox, and the code editor will pop up. Click **Java** to enter the Java script editor.
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/tpiD574_2.png" alt="" style="zoom:50%;" />
3. After editing the script, click **Confirm**.

The Java code mode supports data reference on the [flow data panel](https://www.tencentcloud.com/document/product/1165/51655).

## Script Structure
A Java script must be in compliance with JDK 8 syntax.

The class name must be `Handler`, and you must define a function with the signature `Object eval(Message msg)` as the entry function.
```java
import com.tencent.ipaas.dataway.common.message.Message; 
import com.tencent.ipaas.dataway.common.message.DataRef; 
```

You can add other `import` statements based on required data types.
```java
// The following `import` statements are fixed and cannot be deleted.
import com.tencent.ipaas.dataway.common.message.Message;
import com.tencent.ipaas.dataway.common.message.DataRef; 

/**
 * Entry class of `dataway-java`, which must be named `Handler`
 */
public class Handler {
    /**
     * Entry function, whose signature must be `Object eval(Message msg)`
     * @param msg Input a `Message` object
     * @return Any data object supported by Dataway
     */
    public Object eval(Message msg) {
        return msg.getPayload();
    }
}
```

## Data Types
The Java code mode supports various data types, making it easy for you to manipulate different data.

<table>
    <tr>
        <th>Type</th>
        <th>Description</th>
        <th>Corresponding Python Type</th>
        <th>Example</th>
        <th>Method</th>
    </tr>
    <tr>
        <td>null</td>
        <td>`null` in Java.</td>
        <td>None</td>
        <td>null</td>
        <td>-</td>
    </tr>
    <tr>
        <td>String</td>
        <td>String, i.e., native `String` type in Java.</td>
        <td>str</td>
        <td>"abc"</td>
        <td>-</td>
    </tr>
    <tr>
        <td>Boolean</td>
        <td>Boolean, i.e, native `bool` type in Java.</td>
        <td>bool</td>
        <td>true/false</td>
        <td>-</td>
    </tr>
    <tr>
        <td>float/Float</td>
        <td>Float, i.e., native `float` type in Java.</td>
        <td>float</td>
        <td>123.456</td>
        <td>-</td>
    </tr>
    <tr>
        <td>int/Integer</td>
        <td>Integer, i.e., native `int` type in Java.</td>
        <td rowspan="3">int</td>
        <td>123</td>
        <td>-</td>
    </tr>
    <tr>
        <td>long/Long</td>
        <td>Long integer, i.e., native `Long` type in Java.</td>
        <td>123L</td>
        <td>-</td>
    </tr>
    <tr>
        <td>short/Short</td>
        <td>Short integer, i.e., native `Short` type in Java.</td>
        <td>123</td>
        <td>-</td>
    </tr>
    <tr>
        <td>byte[]</td>
        <td>Byte array, i.e., `byte[]` type in Java.</td>
        <td>bytes</td>
        <td>byte[]{1,2,3}</td>
        <td>-</td>
    </tr>
    <tr>
        <td>java.util.List</td>
        <td>List (a sequence container), i.e., native `List` type in Java.</td>
        <td>list</td>
        <td>new java.util.ArrayList&lt;&gt;()</td>
        <td>For more information, see <a href="https://docs.oracle.com/javase/8/docs/api/java/util/List.html">Interface List<E></a>.</td>
    </tr>
    <tr>
        <td>java.util.Map</td>
        <td>Dictionary (a key-value pair container), i.e., native `Map` type in Java.</td>
        <td>dict</td>
        <td>new java.util.HashMap&lt;&gt;()</td>
        <td>For more information, see <a href="https://docs.oracle.com/javase/8/docs/api/java/util/Map.html">Interface Map<K,V></a>.</td>
    </tr>
    <tr>
        <td>java.time.OffsetDateTime</td>
        <td>Time, i.e., native `OffsetDateTime` type in Java.</td>
        <td>datetime.datetime</td>
        <td>java.time.OffsetDateTime.now()</td>
        <td>For more information, see <a href="https://docs.oracle.com/javase/8/docs/api/java/time/OffsetDateTime.html">Class OffsetDateTime</a>.</td>
    </tr>
    <tr>
        <td>java.time.LocalDate</td>
        <td>Date, i.e., native `LocalDate` type in Java.</td>
        <td>datetime.date</td>
        <td>java.time.LocalDate.now()</td>
        <td>For more information, see <a href="https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html">Class LocalDate</a>.</td>
    </tr>
    <tr>
        <td>java.time.OffsetTime</td>
        <td>Time, i.e., native `OffsetTime` type in Java.</td>
        <td>datetime.time</td>
        <td>java.time.OffsetTime.now()</td>
        <td>For more information, see <a href="https://docs.oracle.com/javase/8/docs/api/java/time/OffsetTime.html">Class OffsetTime</a>.</td>
    </tr>
    <tr>
        <td>java.math.BigDecimal</td>
        <td>Decimal number, i.e., native `BigDecimal` type in Java.</td>
        <td>decimal.Decimal</td>
        <td>new java.math.BigDecimal("1") </td>
        <td>For more information, see <a href="https://docs.oracle.com/javase/8/docs/api/java/math/BigDecimal.html">Class BigDecimal</a>.</td>
    </tr>
    <tr>
        <td>com.tencent.ipaas.dataway.common.message.Entity (data type unique to iPaaS)</td>
        <td>Entity data in iPaaS, which represents a binary object and is accessed as an `Entity` object. It contains information such as `blob`, `mimeType`, and `encoding`.</td>
        <td>Entity</td>
        <td>`payload` in a message constructed by the HTTP Listener component.</td>
        <td>For more information, see Using an `Entity` Object.</td>
    </tr>
    <tr>
        <td rowspan="6">com.tencent.ipaas.dataway.common.message.Multimap (data type unique to iPaaS)</td>
        <td rowspan="6">Multi-value map. Like `xml` but unlike `dict`, this type supports duplicate `key` values. It is inherited from `HashMap&lt;String, List&gt;`.</td>
        <td rowspan="6">MultiMap</td>
        <td rowspan="6">Object obtained after data in `application/www-form-urlencoded` format is parsed</td>
        <td>Constructor: Multimap(Map dict)</td>
    </tr>
    <tr>
        <td>Static constructor: Multimap fromSetEntry(Set&lt;Map.Entry&gt; set)</td>
    </tr>
    <tr>
        <td>Gets the first value of the specified key: Object getFirst(Object key)</td>
    </tr>
    <tr>
        <td>Gets the list of all values of the specified key: List getAll(Object key)</td>
    </tr>
    <tr>
        <td>Gets the key-value pair set: Set&lt;Map.Entry&gt; toSetEntry()</td>
    </tr>
    <tr>
        <td>It is inherited from the `HashMap` method.</td>
    </tr>
    <tr>
        <td rowspan="3">com.tencent.ipaas.dataway.common.message.FormDataParts (data type unique to iPaaS)</td>
        <td rowspan="3">Array + list data structure, which is similar to `orderDict` in Python. It is inherited from `LinkedHashMap&lt;String, Object&gt;`.</td>
        <td rowspan="3">FormDataParts</td>
        <td rowspan="3">Object obtained after data in `multipart/form-data` format is parsed</td>
        <td>Constructor: FormDataParts(String boundary)</td>
    </tr>
    <tr>
        <td>Gets the value of the specified keyword (if the keyword is `int` or `long`, the keyword will be used as the key number; otherwise, the keyword will be the key): Object get(Object key)</td>
    </tr>
    <tr>
        <td>It is inherited from the `LinkedHashMap` method.</td>
    </tr>
    <tr>
        <td rowspan="4">com.tencent.ipaas.dataway.common.message.Message (data type unique to iPaaS, which cannot be constructed in Dataway)</td>
        <td rowspan="4">Flow message in iPaaS, which is accessed as a `Message` object.</td>
        <td rowspan="4">Message</td>
        <td rowspan="4">`msg` parameter in the `public Object eval(Message msg)` entry function</td>
        <td>Gets the payload: Object getPayload()</td>
    </tr>
    <tr>
        <td>Gets attributes: Map getAttrs()</td>
    </tr>
    <tr>
        <td>Gets variables: Map&lt;Object, Object&gt; getVars()/Object getVar(String name)</td>
    </tr>
    <tr>
        <td>Gets the error: DataWayError getError()</td>
    </tr>
    <tr>
        <td rowspan="3">com.tencent.ipaas.dataway.common.message.DataSet (data type unique to iPaaS, which cannot be constructed in Dataway)</td>
        <td rowspan="3">Data set in data integration, which is generated by the data integration component.</td>
        <td rowspan="3">RecordSet</td>
        <td rowspan="3">Output of the **Builder** component</td>
        <td>Gets the ID: Long getId()</td>
    </tr>
    <tr>
        <td>Gets the schema: Schema getSchema()</td>
    </tr>
    <tr>
        <td>Gets partitions: Long getPartitions()</td>
    </tr>
    <tr>
        <td rowspan="5">com.tencent.ipaas.dataway.common.message.Record (data type unique to iPaaS, which cannot be constructed in Dataway)</td>
        <td rowspan="5">Single data record in data integration, which contains the schema.</td>
        <td rowspan="5">Record</td>
        <td rowspan="5">It can be obtained by using the Foreach component to traverse `DataSet`.</td>
        <td>Gets all data: List getData()</td>
    </tr>
    <tr>
        <td>Gets the schema: Schema getSchema()</td>
    </tr>
    <tr>
        <td>Gets the data of the specified keyword (if the keyword is `int` or `long`, the keyword will be the column number; otherwise, the keyword will be the field name): Object get(Object key)</td>
    </tr>
    <tr>
        <td>Returns whether the field name is contained: boolean contains(String name)</td>
    </tr>
    <tr>
        <td>Gets the field name iterator: Iterator&lt;String&gt; getIterator()</td>
    </tr>
    <tr>
        <td rowspan="3">com.tencent.ipaas.dataway.common.message.Schema (data type unique to iPaaS, which cannot be constructed in Dataway)</td>
        <td rowspan="3">Data dictionary in data integration, which describes the metadata.</td>
        <td rowspan="3">Schema</td>
        <td rowspan="3">It can be obtained through the `getSchema()` method of `Record` and is applicable to each data record.</td>
        <td>Gets all field information: RecordField[] getFields()</td>
    </tr>
    <tr>
        <td>Gets the field information of the specified field name: RecordField getField(String name)</td>
    </tr>
    <tr>
        <td>Converts data into the dictionary format such as `{"Fields":[{"Name":"name","Type":"string"}]}`: Map&lt;?,?&gt; toMap()</td>
    </tr>
    <tr>
        <td rowspan="2">com.tencent.ipaas.dataway.common.message.RecordField (data type unique to iPaaS, which cannot be constructed in Dataway)</td>
        <td rowspan="2">Field information in data integration, which describes the metadata of a single field.</td>
        <td rowspan="2">Schema</td>
        <td rowspan="2">`RecordField` can be obtained through the `getField(name)` method of `Schema`.</td>
        <td>Gets the field name: String getName()</td>
    </tr>
    <tr>
        <td>Gets the field type: String getType()</td>
    </tr>
</table>

## Using an `Entity` Object

### Basic methods
In Java code mode of iPaaS, the `Entity` type is used to represent the entity data in flows. It is an encapsulation object of binary data and contains `blob`, `mimeType`, and `encoding`.

| Field | Description |
|---------|---------|
| blob  |  Raw binary data. |
| mimeType  |  Content format of binary data, such as `application/json`, `application/www-form-urlencoded`, and `multipart/form-data`.  |
| encoding  |  Character encoding type of binary data, such as `utf-8` and `gbk`.  |


You can access content in `Entity` as follows:

| Access Method | Description |
|---------|---------|
|   byte[] getBlob() |  Gets the payload data of the message object. A `byte[]` object will be returned. |
|   String getMimeType() | Gets the MIME type of the message object. A `String` object will be returned.|
|   String getEncoding() | Gets the encoding type of the message object. A `String` object will be returned. |
|   Object getValue() |  Deserializes `blob` in the payload based on the MIME and encoding types and returns the result. This type is defined in the type system in Java code mode. |
|   Object get(Object key) |  Deserializes the content in `message` based on the MIME and encoding types and gets the value of the specified key. |

Currently, the MIME types supported for deserialization and types of the deserialized value are as listed below:
- text/plain → String
- application/json →  Object, which is the same as JSON
- application/x-www-form-urlencoded → Multimap
- application/xml → Map
- application/csv → List&lt;Map&lt;String,String&gt;&gt;, i.e., list of mappings between field names and values
- multipart/form-data → FormDataParts



### Constructor
#### `Entity.fromValue` static method
This method is used to encapsulate the value type `data` into an `Entity` object and return it as follows:
```java
Entity.fromValue(Object value, String mimeType, String encoding)
```
The `fromValue` function tries serializing `value` based on the specified MIME and encoding types to get the data of `byte[]` type, encapsulates it into an `Entity` object, and returns the object.

- The `mimeType` parameter is required. Currently, six MIME types are supported: `text/plain`, `application/json`, `application/x-www-form-urlencoded`, `application/csv`, `application/xml`, and `multipart/form-data`.
- The `encoding` parameter is required and can be any valid encoding type.

#### `Entity.fromBytes` static method
This method is used to encapsulate a `String` or a `byte[]` object into an `Entity` object and return it as follows:
```java
Entity.fromBytes(Object data, String mimeType, String encoding)
```
The verification rules of the MIME type and encoding type parameters in `fromBytes` are similar to those in the `fromValue` function but differ in that the value of the MIME type parameter is not limited and can be any MIME type.

- If the `data` parameter passed to the `fromBytes` function is of `byte[]` type, the function will directly return an `Entity` object consisting of parameters `data`, `mimeType`, and `encoding`.
- If the passed `data` parameter is of `String` type, it will be encoded as a `byte[]` object based on the `encoding` parameter and constructed as an `Entity` object.

### Use limits
An `Entity` object is essentially an encapsulation object of binary data. For ease of use, object content access methods like `entity.get()` are provided. Before using these features, note that for some special operations, the system will try deserializing the binary data in the `Entity` object, and runtime errors will occur if parsing fails. Such special operations include:

- Using `entity.getValue()` to get the structured result after parsing.
- Using `entity.get(key)` to get the content of an element in the structured result.

If you perform the above special operations on a non-compliant `Entity` object, runtime errors will occur.
