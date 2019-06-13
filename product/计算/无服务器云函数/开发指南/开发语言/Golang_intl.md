Currently, the following versions of Go programming language are supported:
* Go 1.8


## Function Form

The Go function form is generally as follows:

```golang

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

Considerations for code development

1. You need to use `package main` to include the `main` function.
2. Reference the `github.com/tencentyun/scf-go-lib/cloudfunction` library.
3. 0-2 parameters can be used as the input parameters for the entry function. If parameters are included, "context" needs to be in front, followed by "event"; and the combination of input parameters can be (), (event), (context), or (context, event). For more information, see the descriptions of input parameters below.
4. 0-2 parameters can be used as the return values for the entry function. If parameters are included, the return content "ret" needs to be in front, followed by "error"; and the combination of return values can be (), (ret), (error), or (ret, error). For more information, see the descriptions of return values below.
5. The "event" input parameter and "ret" return value need to be compatible with the `encoding/json` standard library for Marshal and Unmarshal operations.
6. Start the entry function in the `main` function using the `Start` function inside the package.


## Notes on Development Specifications

### `package` and `main` functions

When developing an SCF function with Go, you need to make sure that the `main` function is in the `main` package. In the `main` function, start the entry function that actually handles the business by using the `Start` function in the `cloudfunction` package.

You can use the `Start` function in the package in the main function via `import "github.com/tencentyun/scf-go-lib/cloudfunction" `.

### Entry function

The entry function is the function that is started by `cloudfunction.Start`, which usually handles the actual business. The input parameters and return values of the entry function need to be written according to certain specifications.

#### Input parameters

The entry function can have 0-2 input parameters, for example:

```
func hello()
func hello(ctx context.Context)
func hello(event DefineEvent)
func hello(ctx context.Context, event DefineEvent)
```

If two input parameters are present, you need to make sure that the `context` parameter is before the custom parameter.

The custom parameter can be in Go's own basic data structures, such as string or int, or in custom data structures, such as `DefineEvent` in the example. When a custom data structure is used, you need to make sure that the data structure is compatible with the `encoding/json` standard library for Marshal and Unmarshal operations; otherwise, an error will occur when the input parameters are passed in.

The JSON structure corresponding to the custom data structure usually corresponds to the input parameters when the function is executed. When the function is called, the JSON data structure of the input parameters is converted to a custom data structure variable and passed to the entry function.

#### Return values

The entry function can have 0-2 return values, for example:

```
func hello()()
func hello()(string, error)
func hello()(error)
func hello()(string, error)
```

If 2 return values are defined, you need to make sure that the custom return value is before the error value.

The custom return value can be in Go's own basic data structures, such as string or int, or custom data structures. When a custom data structure is used, you need to make sure that the data structure is compatible with the `encoding/json` standard library for Marshal and Unmarshal operations; otherwise, an error will occur due to exceptional conversion when the return values are returned to the external API.

The JSON structure corresponding to the custom data structure is usually converted to the corresponding JSON data structure in the platform as execution response passed to the caller when the function call is completed.

## Log

You can use methods such as `fmt.Println` or `fmt.Sprintf` in the program to output the log. For example, the function in the sample can output the values of Key1 and Key2 in the input parameters to the log.

The output can be viewed at the `log` location in the function log.


## Compiling and Packaging

A function in the Go environment can only be uploaded as a zip package. You can choose to upload the local zip package or use COS to reference the package. The package should include the compiled executable binary file.

Cross-platform Go compilation can be achieved by developing OS and ARCH on any platform, so it can be done on Linux, Windows, or MacOS.

Compile and package on Linux or MacOS as follows:

```
GOOS=linux GOARCH=amd64 go build -o main main.go
zip main.zip main
```

On Windows, you can use the following command for compilation, and then use a packaging tool to package the outputted binary file, which should be placed in the root directory of the zip package.

```
set GOOS=linux
set GOARCH=amd64
go build -o main main.go
```

## Creating a Function

When creating a function, you can select "Go1" for the runtime environment to create a function for the Go environment.

### Execution method

When you create an SCF function, you need to specify an execution method. If the Go programming language is used, the execution method is similar to `main`, where `main` indicates that the executable entry file is the compiled `main` binary file.

### Code package

The Go programming language only supports submitting the code package by uploading a local zip package or uploading it through COS. When uploading the zip package, please make sure that the root directory of the package contains the specified entry file, and the file name matches that entered in the trigger; otherwise, execution will fail as the entry file cannot be found.


## Testing a Function

You can click the test button at the upper right corner in the console to open the testing interface, trigger a function, and view the execution result. For the sample code, since the input parameters are in `DefineEvent` data structure, the corresponding JSON structure is similar to `{"key1":"value1","key2":"value2"}`, when the testing interface is used for function triggering, the test template that can be entered is in a data structure like `{"key1":"value1","key2":"value2"}`. If you need to use other data structures to test a function, or the function input parameters are in other custom data structures, the function can only be successfully executed only if the data structure of the function input parameters corresponds to the JSON data structure of the test template.
