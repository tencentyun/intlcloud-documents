The log query and offline log features can be used normally only after logs are reported. This document describes how to report logs to RUM.

## Prerequisites
Install and initialize the Aegis SDK in any method as detailed in [Installation and Initialization](https://intl.cloud.tencent.com/document/product/1131/44519).

## Log Reporting
Pass in the following parameters to configure the SDK and report logs:
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

