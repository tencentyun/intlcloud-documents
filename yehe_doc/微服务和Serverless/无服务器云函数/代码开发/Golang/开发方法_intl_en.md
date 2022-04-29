## Function Form

The Go function form is generally as follows:

``` go
package main

import (
    "context"
    "fmt"
    "github.com/tencentyun/scf-go-lib/cloudfunction"
)

type DefineEvent struct {
    // test event define
    Key1 string `json:"key1"`
    Key2 string `json:"key2"`
}

func hello(ctx context.Context, event DefineEvent) (string, error) {
    fmt.Println("key1:", event.Key1)
    fmt.Println("key2:", event.Key2)
    return fmt.Sprintf("Hello %s!", event.Key1), nil
}

func main() {
    // Make the handler available for Remote Procedure Call by Cloud Function
    cloudfunction.Start(hello)
}
```



Pay attention to the following during code development:

- You need to use `package main` to include the `main` function.
- Import the `github.com/tencentyun/scf-go-lib/cloudfunction` library by running `go get github.com/tencentyun/scf-go-lib/cloudfunction` before packaging and compilation.
- 0–2 parameters can be used as the input parameters for the entry function. If parameters are included, `context` needs to be in front, followed by `event`, and the combination of input parameters can be `()`, `(event)`, `(context)`, or `(context, event)`. For more information, see [Input parameters](#Participation).
- 0–2 parameters can be used as the returned values for the entry function. If parameters are included, the returned content `ret` needs to be in front, followed by `error`, and the combination of returned values can be `()`, `(ret)`, `(error)`, or `(ret, error)`. For more information, see [Returned values](#ReturnValue).
- The `event` input parameter and `ret` returned value need to be compatible with the `encoding/json` standard library for Marshal and Unmarshal operations.
- Start the entry function in the `main` function by using the `Start` function inside the package.

## Execution Method

When you create an SCF function, you need to specify an execution method. If the Go programming language is used, the execution method is similar to `main`, where `main` indicates that the executable entry file is the compiled `main` binary file.

When submitting the ZIP code package by uploading the ZIP file locally or through COS, make sure that the root directory of the ZIP package contains the specified binary files; otherwise, function creation or execution will fail as the execution file cannot be found.

### `package` and `main` functions

When developing an SCF function with Go, you need to make sure that the `main` function is in the `main` package. In the `main` function, start the entry function that actually handles the business by using the `Start` function in the `cloudfunction` package.

You can use the `Start` function in the package in the `main` function through `import "github.com/tencentyun/scf-go-lib/cloudfunction"`.

### Entry function

An entry function is the function started by `cloudfunction.Start`, which usually handles the actual business. The input parameters and returned values of the entry function need to be written according to certain specifications.

#### Input parameters

The entry function can have 0–2 input parameters, such as:

```go
func hello()
func hello(ctx context.Context)
func hello(event DefineEvent)
func hello(ctx context.Context, event DefineEvent)
```

If two input parameters are present, you need to make sure that the `context` parameter is before the custom parameter.

The custom parameter can be in Go's own basic data structures (such as `string` or `int`) or custom data structures (such as `DefineEvent` in the sample). If a custom data structure is used, you need to make sure that the data structure is compatible with the `encoding/json` standard library for Marshal and Unmarshal operations; otherwise, an error will occur when the input parameters are passed in.

The JSON structure corresponding to the custom data structure usually corresponds to the input parameters when the function is executed. When the function is invoked, the JSON data structure of the input parameters will be converted to a custom data structure variable and passed to the entry function.

> ! The event structures of input parameters passed in by certain triggers have been defined and can be used directly. You can get and use the Go libraries through the [Cloud Event Definition](https://github.com/tencentyun/scf-go-lib/tree/master/events) by importing "github.com/tencentyun/scf-go-lib/events"` into the code. If you have any questions during use, you can [submit an issue](https://github.com/tencentyun/scf-go-lib/issues/new) or [ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

#### Response

The entry function can have 0–2 returned values, such as:
```go
func hello()()
func hello()(error)
func hello()(string, error)
```

If two returned values are defined, you need to make sure that the custom returned value is before the error value.

The custom returned value can be in Go's own basic data structures (such as `string` or `int`) or custom data structures. If a custom data structure is used, you need to make sure that it is compatible with the `encoding/json` standard library for Marshal and Unmarshal operations; otherwise, an error will occur due to exceptional conversion when the returned values are returned to the external API.

The JSON structure corresponding to the custom data structure is usually converted to the corresponding JSON data structure in the platform as execution response passed to the invoker when the function invocation is completed.

