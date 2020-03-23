## Operation Scenarios
In the Tencent Cloud API Gateway Console, you can view the logs of requests received by API Gateway.


## Directions
1. Log in to the [API Gateway Console](https://console.cloud.tencent.com/apigateway/index) and click **Service** on the left sidebar to enter the service list page.
2. On the service list page, click a service name to enter the service details page.
3. At the top of the service details page, click **Service Log** to open the log page of the service.
4. You can find service logs as needed.

## Time Range
- The real-time service log feature allows you to view real-time logs and logs in the last 3 hours and to customize the time range for log query.
- With the real-time service log feature, you can view logs in the last 30 days.
- The time range for log query cannot exceed one day.

## Query by Criteria
Currently, the Tencent Cloud API Gateway Console allows you to query real-time service logs by `RequestID`, API ID, or keyword.
- RequestID: if you enter the complete `RequestID` of a request, API Gateway will return the logs that correspond to it for the selected time range. You cannot enter a partial `RequestID` for fuzzy match.
- API ID: if you enter the complete API ID of an API under the current service, API Gateway will return all logs for the API for the selected time range. You cannot enter a partial API ID for fuzzy match.
- Keyword: if you enter a keyword, API Gateway will return all logs containing a field that exactly matches the keyword for the selected time range.

>
>- In one single query, you can query by only one of the three query criteria.
>- If you don't select a query criterion, the query will be performed by keyword by default.
