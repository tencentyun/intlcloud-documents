Automatic unit conversion is available in charts. When you select an original unit, the value is automatically converted to the next higher unit if it meets the conversion factor. Units can be configured to display decimal places.

## Overview

The results of SQL aggregation are unitless values by default. In the following cases, you need to use unit conversion to make the data more readable.


### Selecting a unit and automatically converting it

In CLS chart analysis, SQL aggregation results are unitless raw values by default, and you need to specify a basic unit, such as byte in the example. After a basic unit is selected, if a value is great enough to be converted to a value with a higher-level unit, it will be automatically converted. In this example, the value in bytes is automatically converted to a value in GiB.

In unit configuration, the precision decides the number of decimal places. By default, if `Auto` is selected, two decimal places will be retained. You can modify the precision as needed.



### Manually entering a unit

If data has a special unit that cannot be found in the unit configuration options, you can manually add a custom unit with the `custom` prefix. However, note that the custom unit is fixed and cannot be automatically converted. Therefore, if you want to use the raw unit in a unified manner without triggering automatic unit conversion, you can manually add a fixed unit.



