
## Go Version Selection

Currently, the following versions of Go programming language are supported:

* Go 1.8 and above

You can choose the `Go1` runtime environment when creating a function.

## Notes

Go is used in SCF in a different way from scripting languages such as Python and Node.js, with the following restrictions:

* Code upload is not supported: When Go is used, only developed, compiled, and packaged binary files can be uploaded. The SCF environment does not provide Go compiling capability.
* Online editing is not supported: Because code cannot be uploaded, online editing of code is not supported. The code page of a Go runtime function only lists the ways to upload the code through the page or submit the code file through COS.

