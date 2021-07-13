Based on the features of SCF, we recommend you:
- Write function code in a stateless style to ensure that your code will not undergo any state maintenance. Both local storage and memory results may be lost; therefore, services such as COS and Redis/Memcached should be used to cache intermediate information and store the final computation results.
- Instantiate any objects that may be reused (such as database connections) other than execution methods.
- Configure +rx (read and execution) permission to your file in the uploaded ZIP package to ensure successful code execution.
- Maximize the use of `log/print` statements in your code to provide sufficient information for debugging.
- You can use external code management services (such as Git) for the purpose of version and audit management of core code, so as to ensure the code completeness (the version management feature will be available in the future).

>? In the subsequent specific practices, most of the functions are deployed in the form of function template. You can download the function templates and code for analysis and research.

