## Deployment Methods

A function in the Go environment can only be uploaded as a zip package. You can choose to upload the local zip package or use COS to import the package. The package should include the compiled executable binary file.

## Compiling and Packaging

Cross-platform Go compilation can be achieved by specifying OS and ARCH on any platform, so it can be done on Linux, Windows, or macOS.

- Compile and package on Linux or macOS as follows:
```shell
GOOS=linux GOARCH=amd64 go build -o main main.go
zip main.zip main
```

- Compile and package on Windows as follows:
  1. Press **Windows + R** to open the "Run" window, enter **cmd**, and press **Enter**.
  2. Run the following command to compile: 
```shell
set GOOS=linux
set GOARCH=amd64
go build -o main main.go
```
 3. Use a packaging tool to package the output binary file, which should be placed in the root directory of the zip package.

