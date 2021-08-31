You can use API Gateway to design your businesses as APIs for service provision. You are recommended to design APIs in compliance with the following rules for easier future use:

- Do not add a slash (`/`) at the end of the URI. A resource whose URL has an ending slash may be mistaken as a directory, causing errors in calls.
- Use a hyphen (`-`) to improve the readability of the URI. Connect words with hyphens so that the URI can be easily understood.
- It is not allowed to use the underscore (`_`) in the URL, as it may be covered by the underline effect in the text viewer and thus less readable.
- Avoid using uppercase letters which are not aesthetically pleasing and error-prone.
- Do not include an extension in the URI. REST API clients are recommended to use the format selection mechanism "Accept request header" provided by HTTP.
