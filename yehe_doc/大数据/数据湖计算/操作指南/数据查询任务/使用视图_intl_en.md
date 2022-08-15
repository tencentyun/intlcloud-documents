In Data Lake Compute, a view is a logical table rather than a physical table. Whenever a view is referenced during a query, the query that defines the view will be executed. You can create a view through `SELECT` and reference it in future queries.

**System restraints**
- A view name is case-insensitive and can contain up to 128 letters and underscores.
- Data Lake Compute doesn't support managing data access permissions through views.

