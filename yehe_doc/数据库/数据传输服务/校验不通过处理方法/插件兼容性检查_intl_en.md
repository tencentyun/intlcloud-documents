
## Check Details
- Check requirements: check whether extensions/plugins in the source database also exist in the target database.
Before migration, you don't need to create extensions/plugins in the target database since DTS will create them for you. If an extension/plugin cannot be created in it, or the extension/plugin version in it differs from that in the source database, a verification warning will be reported. The warning will not block the migration task but will affect the business.
  
- Impact on the business: PostgreSQL has many extensions. Most extension compatibility issues don't affect data migration, but those related to the storage engine (such as TimescaleDB, PipelineDB, and PostGIS) will cause the migration task to fail.

## Fix
- For extension/plugin compatibility issues not related to the engine (such as pg_hint_plan, pg_prewarm, tsearch2, hll, rum, and zhparser), you generally can ignore them and fix them by yourself based on your business conditions.
- For extension compatibility issues related to the engine (such as TimescaleDB, PipelineDB, and PostGIS), we recommend you [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

