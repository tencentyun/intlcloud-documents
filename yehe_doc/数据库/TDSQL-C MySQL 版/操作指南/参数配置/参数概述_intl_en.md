This document describes system variables (also known as parameters), which are configurations items used to manage and control a database.

## Use cases
TDSQL-C for MySQL provides a rich set of parameters for you to optimize the database performance. In the console, you can directly modify the default values of database parameters for formats, permissions, feature enablement, character set, execution conditions, cache size, and time/quantity/size limits to better suit your needs.

## Parameter categories
TDSQL-C for MySQL parameters are divided into global parameters and session parameters. Once configured, values of global parameters will take effect for all instances in the cluster, while values of session parameters only apply to the target instance and can be synced to other instances.

## Supported parameter operations
- Select one of many preset templates with default parameter values when creating a TDSQL-C for MySQL cluster to improve the performance while guaranteeing the stability.
- Adjust parameter values individually or in batches based on your business needs to flexibly adapt to different use cases.
- Create custom templates by modifying a default parameter template.
- Generate templates by importing parameters from configuration file `my.conf`.
- Save parameter configurations as templates and apply them to other clusters.
- Use formulas to set the values of certain parameters. When the instance specification is changed, parameter values set with formulas will also be automatically changed accordingly to keep the database in the optimal or most stable status.
- Use global and session parameters.

## References
- For more information on how to modify parameters individually or in batches, modify parameters by importing a parameter template or configuration file, export the parameter configuration file, or query parameter modifications, see [Setting Instance Parameters](https://intl.cloud.tencent.com/document/product/1098/44602).
- For more information on how to create, copy, import, export, or delete parameter templates and modify parameter values in parameter templates, see [Applying Parameter Template](https://intl.cloud.tencent.com/document/product/1098/44601).
- For suggestions on how to set parameters, see [Suggestions on Parameter Configuration](https://intl.cloud.tencent.com/document/product/1098/44600).
