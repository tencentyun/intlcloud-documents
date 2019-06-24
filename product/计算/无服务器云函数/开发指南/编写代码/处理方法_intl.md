When you write SCF function code, the first and most important step is to write a handler method that the SCF platform will first execute when calling the function. When creating a handler method, follow a common syntax structure:
```
def method_name(event,context): 
    ...
    return some_value
```
All handler methods of functions can receive two input parameters: `event` and `context`.

## Getting Details of Input Event from `event`
SCF uses `event` to pass event data to the function, which is a `dict` type.

First, you need to know what the function does. Does it respond to an event-triggered request from a cloud service (such as triggering the function by uploading a file to COS)? Is it called by another application (such as implementing a generic module)? Or doesn't it need any input?

The value of `event` varies by actual situations:

- If the function is triggered by a cloud service, the cloud service will pass the event to SCF as the `event` parameter in a platform-predefined, immutable format. You can write code based on this format to get the information you need from the `event` parameter.
For example, when COS triggers a function, the specific information of the bucket and the file will be passed to the `event` parameter in [JSON format](https://cloud.tencent.com/document/product/583/9707#cos-.E8.A7.A6.E5.8F.91.E5.99.A8.E7.9A.84.E4.BA.8B.E4.BB.B6.E6.B6.88.E6.81.AF.E7.BB.93.E6.9E.84).

- If the function is called by another application, you can freely define a parameter of `dict` type between the caller and the function code, where the caller passes in the data in the agreed upon format, and the function code obtains the data in the format.
For example, you can agree upon a data structure of `dict` type: `{"key":"XXX"}`, and when the caller passes in the data `{"key":"abctest"}`, the function code can get the value `abctest` through `event[key]`.

- If the function does not need any input, you can ignore the `event` and `context` parameters in your code.

## Return Value (Optional)

The return value is the returned result of the `return` statement in the code, will be handled differently depending on the type of function call. For more information about the types of function calls, see [Core Concepts](https://cloud.tencent.com/document/product/583/9210):
- If you call the function synchronously, SCF will return the value of the `return` statement in the code to the function caller.
For example, the **Test** button in the console calls functions synchronously, so when you call a function using the console, the console will display the return value. If nothing is returned in the code, a null value will be returned.
- If you call the function asynchronously, this value will be discarded.

For example, you can create a function, copy and paste the following code, and set the execution method to `index.handler`. After the function is created, click **Test** to execute the function and observe the returned message result.
```
def handler(event, context):
    message = 'Hello {} {}!'.format(event['first_name'], 
                                    event['last_name'])  
    return { 
        'message' : message
    } 
``` 

The code receives the input event from the `event` parameter and returns a message containing the data.
For details steps in creating a function, see [Step 1: Create a Hello World function](https://cloud.tencent.com/document/product/583/9204).

### Return Value Structure and Handling

When a specific value is returned in a function, it usually is a specific data structure, such as simple data structure or `dict` data structure in a Python environment, `JSON Object` data structure in a Node.js environment, `Array` data structure in a PHP environment, or simple data structure or `struct` data structure with a JSON description in a Go environment.

After SCF obtains the return value of the function code, it converts the returned data structure to JSON and return it to the caller. Therefore, you need to ensure that the return value of the function is a data structure that can be converted to JSON. If the returned object does not include a method for JSON conversion, SCF will fail when executing JSON conversion and prompt an error. In addition, please do not convert the return value to JSON before returning; otherwise, the outputted string will be converted again.
