### Automatic Database Capacity Management
PostgreSQL for Serverless can automatically respond to resources based on the busyness of business requests, so you don't need to pay for the database during idle time; instead, you only need to pay for the actually used data capacity and response resources when the database is active, which helps your save database costs. If there are no user requests to the database, the database will automatically close all resource responses.

### High Availability
PostgreSQL for Serverless supports the architecture of one primary instance and one secondary instance for high availability. When the primary instance becomes unavailable due to an exception, the database will automatically start the secondary instance, to which business connections will be transferred so as to prevent business interruption.

### Automatic Backup
PostgreSQL for Serverless automatically backs up the entire database at 1:00 AM every day and backs up database logs once every 15 minutes or when the number of log files reaches 60. All backups are retained for 7 days.
Backup is automatically performed on the backend. Currently, you cannot view, download, or restore data from backups.

### Cost Savings
With PostgreSQL for Serverless, you can create a database instance for easy use without caring about the instance specifications. You only need to pay for the actual usage when the database is active.

### Support for Features of PostgreSQL
In addition to supporting the serverless architecture, PostgreSQL for Serverless also enjoys the functional advantages of standard PostgreSQL database instances, such as rich extensions, backup and restoration, and high availability.
