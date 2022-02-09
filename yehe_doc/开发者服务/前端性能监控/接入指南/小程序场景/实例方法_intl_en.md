RUM provides various instance methods for data reporting. You can use them to modify the instance configuration and customize the events and resources for speed test to be reported.

Currently, RUM provides the following Aegis instance methods:  

| Parameter | Description |
|---------|---------|
| setConfig | Passes in the configuration object, which contains information such as user ID and UIN. |
|info| Is a main reporting field to report allowed logs. <br>A log will be reported to the backend only in the following cases:<br>1. The user who opens the page is in the allowlist.<br>2. The page has an error. |
|infoAll| Is a main reporting field to report allowed logs. The only difference between it and `info` is as follows: <br>`info` reports the logs of only specified users, while `infoAll` reports the logs of all users. |
|error| Is a main reporting field to report the error information. |
|report| Reports the information of a log in any type. |
|reportEvent| Reports a custom event. |
|reportTime| Reports a custom resource for speed test. |
|time| Reports a custom resource for speed test and is used together with `timeEnd` to calculate and report data between two time points. |
|timeEnd| Reports a custom resource for speed test and is used together with `time` to calculate and report data between two time points. |
|destroy| Terminates the Aegis instance. |


## Prerequisites
Install and initialize the Aegis SDK in any method as detailed in [Installation and Initialization](https://intl.cloud.tencent.com/document/product/1131/44531).

## Instance Methods

### setConfig

This method is used to modify the instance configuration in the following use cases:  
1. You can get the user UIN and pass in two instance objects of user ID and UIN at the same time for instantiation:
<dx-codeblock>
:::  js
const aegis = new Aegis({
    id: 'pGUVFTCZyewxxxxx',
    uin: '777'
})
:::
</dx-codeblock>
2. Generally, the `uin` cannot be directly obtained in the beginning. If instantiation cannot be completed during the period when `uin` is obtained, RUM cannot listen on the errors occurring in this period. To solve this, you can pass in the ID first for instantiation and then import `setConfig` to pass in `uin` as follows:
<dx-codeblock>
:::  js
const aegis = new Aegis({
    id: 'pGUVFTCZyewxxxxx'
})

// After `uin` is obtained
aegis.setConfig({
  uin: '6666'
})
:::
</dx-codeblock>

### `info`, `infoAll`, `error`, and `report`

These are the main reporting methods provided by RUM.
<dx-codeblock>
:::  js
// `info` can report any string, number, array, and object, but it reports data only when the user opening the page is in the allowlist
aegis.info('test');
aegis.info('test', 123, ['a', 'b', 'c', 1], {a: '123'});

// You can also report a specified object and pass in the `ext` and `trace` parameters
// You must pass in the `msg` field in this case
aegis.info({
 msg: 'test',
 ext1: 'ext1',
 ext2: 'ext2',
 ext3: 'ext3',
 trace: 'trace',
});

// Different from `info`, `infoAll` reports full data
aegis.infoAll({
 msg: 'test',
 ext1: 'ext1',
 ext2: 'ext2',
 ext3: 'ext3',
 trace: 'trace',
});

// `error` indicates a JavaScript error log, whose full data will also be reported. Generally, it is used to actively get and report JavaScript exceptions
aegis.error({
 msg: 'test',
 ext1: 'ext1',
 ext2: 'ext2',
 ext3: 'ext3',
 trace: 'trace',
});
aegis.error(new Error('Actively report an error'));

// The default log type of `aegis.report` is `report`, but currently you can pass in any log type
aegis.report({
 msg: 'This is an Ajax error log',
 level: Aegis.LogType.AJAX_ERROR,
 ext1: 'ext1',
 ext2: 'ext2',
 ext3: 'ext3',
 trace: 'trace',
});
:::
</dx-codeblock>

### reportEvent

This method can be used to report a custom event, and the system will automatically collect the metrics of the reported event, such as PV and platform distribution.
`reportEvent` supports the string and object data types for the parameters to be reported.

#### String data type
<dx-codeblock>
:::  js
aegis.reportEvent('The XXX request succeeded');
:::
</dx-codeblock>

#### Object data type
`ext1`, `ext2`, and `ext3` use the parameters passed in when you use `new Aegis`. During custom event reporting, you can overwrite their default values.
<dx-codeblock>
:::  js
aegis.reportEvent({
  name: 'The XXX request succeeded', // Required
  ext1: 'Additional parameter 1',
  ext2: 'Additional parameter 2',
  ext3: 'Additional parameter 3',
})
:::
</dx-codeblock>

>! The keys of the three additional parameters are fixed, which can only be `ext1`, `ext2`, and `ext3` currently.

### reportTime

This method can be used to report custom speed test as follows:

<dx-codeblock>
:::  js
// Suppose the time of `onload` is 1 second
aegis.reportTime('onload', 1000);
:::
</dx-codeblock>

If you want to use additional parameters, you can pass them in by using the object type, and they will overwrite the default values of `ext1`, `ext2`, and `ext3`.
<dx-codeblock>
:::  js
aegis.reportTime({
  name: 'onload', // Custom speed test name
  duration: 1000, // Custom speed test duration. Value range: 0–60000
  ext1: 'test1',
  ext2: 'test2',
  ext3: 'test3',
});
:::
</dx-codeblock>

>? `onload` can be renamed.

### `time` and `timeEnd`

These methods can be used to report a custom resource for speed test and are suitable for calculating and reporting a duration between two time points.

<dx-codeblock>
:::  js
aegis.time('complexOperation');
/**
 * .
 * .
 * After complicated operations are performed for a long time
 * .
 * .
 */
 aegis.timeEnd('complexOperation'); /** At this point, the log has been reported**/
 :::
 </dx-codeblock>

>? `complexOperation` can be renamed.
> In custom speed test, you can report any values, and the server will collect and calculate them. As the server cannot process dirty data, we recommend you restrict the statistics values passed in to prevent the system from being affected by dirty data.
> Currently, Aegis can calculate values only between 0 and 60000. If you use a greater value, we recommend you adjust it reasonably. 


### destroy

This method is used to terminate the instance process, after which no data will be reported, and Aegis will stop collecting user data.

<dx-codeblock>
:::  js
aegis.destroy();
:::
</dx-codeblock>

