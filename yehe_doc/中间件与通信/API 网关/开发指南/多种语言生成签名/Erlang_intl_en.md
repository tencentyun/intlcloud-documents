## Overview

This document describes how to authenticate and manage your APIs through key pair authentication in Erlang.

## Directions

1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the authentication type as "key pair authentication" (for more information, please see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795)).
2. Publish the service where the API resides to the release environment (for more information, please see [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809)).
3. Create a key pair on the key management page in the console.
4. Create a usage plan on the usage plan page in the console and bind it to the created key pair (for more information, please see [Sample Usage Plan](https://intl.cloud.tencent.com/document/product/628/11816)).
5. Bind the usage plan to the API or the service where the API resides.
6. Generate signing information in Erlang by referring to the [Sample Code](#example).

## Notes

- The eventually delivered HTTP request contains at least two headers: `Date` or `X-Date` and `Authorization`. More optional headers can be added in the request. If `Date` is used, the server will not check the time; if `X-Date` is used, the server will check the time.
- The value of the `Date` header is the construction time of the HTTP request in GMT format, such as Fri, 09 Oct 2015 00:00:00 GMT.
- The value of the `X-Date` header is the construction time of the HTTP request in GMT format, such as Mon, 19 Mar 2018 12:08:40 GMT. The construction time of the HTTP request cannot deviate from the current time by more than 15 minutes.
- If it is a microservice API, you need to add two fields in the header: `X-NameSpace-Code` and `X-MicroService-Name`. They are not needed for general APIs and are excluded in the demo.

<span id="example"></span>

## Sample Code

```erl
-module(apigateway_erlang_demo).

%% API
-export([request_api/0]).

%% request_api()
request_api() ->

%%      Start the inets service. If the project has already started this service, remove this parameter
        inets:start(),

        Url = "http://service-xxxxxxxx-1234567890.ap-beijing.apigateway.myqcloud.com/release/xxxxx",
        Source = "xxxxxx",
        GMTDate = now_to_utc_string(),
        SecretId = "xxxDf4estwodtdzoke1234567890i3j9jv18wt9u",
        SecretKey = "xxxSNF0CEp3OhN4t91234567890AWrct960X9192",
        Sign = simple_sign(Source, GMTDate, SecretId, SecretKey),
        Header = [
                {"Source", Source},
                {"x-Date", GMTDate},
                {"Authorization", Sign},
                {"Content-Type", "application/x-www-form-urlencoded"}
        ],

        case httpc:request(get, {Url, Header}, [], []) of
                {ok, {_StatusLine, _Header, Result}} ->
                        Result;

%% %%                Result -> need decode

                Error ->
                        Error
        end.

simple_sign(Source, GMTDate, SecretId, SecretKey) ->
        Auth = "hmac id=\"" ++ SecretId ++ "\", algorithm=\"hmac-sha1\", headers=\"x-date source\", signature=\"",
        SecretKey = "xxxSNF0CEp3OhN4t91234567890AWrct960X9192",
        Source = "xxxxxx",
        SignStr = "x-date: " ++ GMTDate ++ "\n" ++ "source: " ++ Source,
        Mac = crypto:hmac(sha, SecretKey, SignStr),
        Sign = base64:encode(Mac),
        Sign2 = binary_to_list(Sign),
        Sign3 = Auth ++ Sign2 ++ "\"",
        Sign3.

%% Get the current time and convert it into the format of "Mon, 02 Jan 2006 15:04:05 GMT"
now_to_utc_string() ->
        {{Year, Month, Day}, {Hour, Minute, Second}} = calendar:universal_time(),
        WeekNum = week_num(),
        Month1 = month_to_english(Month),
        WeekNum1 = week_to_english(WeekNum),
        Day1 = lists:flatten(io_lib:format("~2..0w", [Day])),
        Date1 = WeekNum1 ++ ", " ++ Day1 ++ " " ++ Month1,
        Date2 = lists:flatten(
                io_lib:format(" ~4..0w ~2..0w:~2..0w:~2..0w GMT",
                        [Year, Hour, Minute, Second])),
        Date1 ++ Date2.

week_num() ->
        {Date, _} = calendar:local_time(),
        calendar:day_of_the_week(Date).

%% day_of_the_week
week_to_english(1) ->
        "Mon";
week_to_english(2) ->
        "Tue";
week_to_english(3) ->
        "Wed";
week_to_english(4) ->
        "Thu";
week_to_english(5) ->
        "Fri";
week_to_english(6) ->
        "Sat";
week_to_english(7) ->
        "Sun".

month_to_english(1) ->
        "Jan";
month_to_english(2) ->
        "Feb";
month_to_english(3) ->
        "Mar";
month_to_english(4) ->
        "Apr";
month_to_english(5) ->
        "May";
month_to_english(6) ->
        "Jun";
month_to_english(7) ->
        "Jul";
month_to_english(8) ->
        "Aug";
month_to_english(9) ->
        "Sept";
month_to_english(10) ->
        "Oct";
month_to_english(11) ->
        "Nov";
month_to_english(12) ->
        "Dec".
```
