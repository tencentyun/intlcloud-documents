Currently, the following versions of Go are supported:
* Go 1.8 and above


## Function Format

The Go function format is generally as follows:

<dx-codeblock>
:::  golang
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
:::
</dx-codeblock>

Pay attention to the following during code development:

- You need to use `package main` to include the `main` function.
- Import the `github.com/tencentyun/scf-go-lib/cloudfunction` library by running `go get github.com/tencentyun/scf-go-lib/cloudfunction` before packaging and compilation.
- 0–2 parameters can be used as the input parameters for the entry function. If parameters are included, `context` needs to be in front, followed by `event`, and the combination of input parameters can be `()`, `(event)`, `(context)`, or `(context, event)`. For more information, please see [Input parameters](#Participation).
- 0–2 parameters can be used as the returned values for the entry function. If parameters are included, the returned content `ret` needs to be in front, followed by `error`, and the combination of returned values can be `()`, `(ret)`, `(error)`, or `(ret, error)`. For more information, please see [Returned values](#ReturnValue).
- The `event` input parameter and `ret` returned value need to be compatible with the `encoding/json` standard library for Marshal and Unmarshal operations.
- Start the entry function in the `main` function by using the `Start` function inside the package.


## Notes on Development Specifications

### package and main functions

When developing an SCF function with Go, you need to make sure that the `main` function is in the `main` package. In the `main` function, start the entry function that actually handles the business by using the `Start` function in the `cloudfunction` package.

You can use the `Start` function in the package in the `main` function through `import "github.com/tencentyun/scf-go-lib/cloudfunction"`.

### Entry function

An entry function is the function started by `cloudfunction.Start`, which usually handles the actual business. The input parameters and returned values of the entry function need to be written according to certain specifications.

[](id:Participation)

#### Input parameters

The entry function can have 0–2 input parameters, such as:

```
func hello()
func hello(ctx context.Context)
func hello(event DefineEvent)
func hello(ctx context.Context, event DefineEvent)
```

If two input parameters are present, you need to make sure that the `context` parameter is before the custom parameter.

The custom parameter can be in Go's own basic data structures (such as `string` or `int`) or custom data structures (such as `DefineEvent` in the sample). If a custom data structure is used, you need to make sure that the data structure is compatible with the `encoding/json` standard library for Marshal and Unmarshal operations; otherwise, an error will occur when the input parameters are passed in.

The JSON structure corresponding to the custom data structure usually corresponds to the input parameters when the function is executed. When the function is invoked, the JSON data structure of the input parameters will be converted to a custom data structure variable and passed to the entry function.

>! The event structures of input parameters passed in by certain triggers have been defined and can be used directly. You can get and use the Go libraries through the [Cloud Event Definition](https://github.com/tencentyun/scf-go-lib/tree/master/events) by importing "github.com/tencentyun/scf-go-lib/events"` into the code. If you have any questions during use, you can [submit an issue](https://github.com/tencentyun/scf-go-lib/issues/new) or [ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

[](id:ReturnValue)
#### Returned values

The entry function can have 0–2 returned values, such as:

```
func hello()()
func hello()(error)
func hello()(string, error)
```

If two returned values are defined, you need to make sure that the custom returned value is before the error value.

The custom returned value can be in Go's own basic data structures (such as `string` or `int`) or custom data structures. If a custom data structure is used, you need to make sure that it is compatible with the `encoding/json` standard library for Marshal and Unmarshal operations; otherwise, an error will occur due to exceptional conversion when the returned values are returned to the external API.

The JSON structure corresponding to the custom data structure is usually converted to the corresponding JSON data structure in the platform as execution response passed to the invoker when the function invocation is completed.

## Log

You can use methods such as `fmt.Println` or `fmt.Sprintf` in the program to output a log. For example, the function in the sample can output the values of `Key1` and `Key2` in the input parameters to the log.

The output can be viewed at the `log` position in the function log.


## Compilation and Packaging

A function in the Go environment can only be uploaded as a zip package. You can choose to upload the local zip package or use COS to import the package. The package should include the compiled executable binary file.

Cross-platform Go compilation can be achieved by specifying OS and ARCH on any platform, so it can be done on Linux, Windows, or macOS.

- Compile and package on Linux or macOS as follows:
```
GOOS=linux GOARCH=amd64 go build -o main main.go
zip main.zip main
```
- Compile and package on Windows as follows:
  1. Press **Windows + R** to open the "Run" window, enter **cmd**, and press **Enter**.
  2. Run the following command to compile: 
```
set GOOS=linux
set GOARCH=amd64
go build -o main main.go
```
  3. Use a packaging tool to package the output binary file, which should be placed in the root directory of the zip package.

## Creating Function

When creating a function, you can select "Go1" as the runtime environment to create a function for the Go environment.

### Execution method

When you create an SCF function, you need to specify an execution method. If the Go programming language is used, the execution method is similar to `main`, where `main` indicates that the executable entry file is the compiled `main` binary file.

### Code package

The Go programming language only supports submitting the code package by uploading a local zip package or uploading it through COS. When uploading the zip package, please make sure that the root directory of the package contains the specified entry file, and the filename matches that entered in the trigger; otherwise, execution will fail as the entry file cannot be found.


## Testing Function

You can click the test button in the top-right corner on the console to open the testing page, trigger a function synchronously, and view the execution result. For the sample code, as the input parameters are in `DefineEvent` data structure, the corresponding JSON structure is similar to `{"key1":"value1"," key2":"value2"}`, when the testing page is used for function triggering, the test template that can be entered is in a data structure like `{"key1":"value1"," key2":"value2"}`. If you need to use other data structures to test a function, or the function input parameters are in other custom data structures, the function can be successfully executed only if the data structure of the function input parameters corresponds to the JSON data structure of the test template.


## Related Documents
For more information on how to use relevant features, please see the following documents:
- [Network Configuration Management](https://intl.cloud.tencent.com/document/product/583/38377)
- [Role and Authorization](https://intl.cloud.tencent.com/document/product/583/38176)
