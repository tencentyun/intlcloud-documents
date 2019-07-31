Currently, the following versions of PHP programming language are supported:

* PHP 5.6
* PHP 7.2

## Function Form

The PHP function form is generally as follows:

```
<?php

function main_handler($event, $context) {
    echo("hello world");
    print_r($event);
    return "hello world";
}

?>

```

## Execution Method

When you create an SCF function, you need to specify an execution method. If the PHP programming language is used, the execution method is similar to `index.main_handler`, where `index` indicates that the executed entry file is `index.php`, and `main_handler` indicates that the executed entry function is `main_handler`. When submitting the zip code package by uploading the zip file locally or through COS, please make sure that the root directory of the package contains the specified entry file, the file contains the entry function specified by the definition, and the names of the file and function match those entered in the trigger; otherwise, execution will fail as the entry file or entry function cannot be found.

## Input Parameters

The input parameters in the PHP environment include $event and $context.

* $event: This parameter is used to pass the trigger event data.
* $context: This parameter is used to pass runtime information to your handler.

## Return and Exception

Your handler can use `return` to return a value. The return value will be handled differently depending on the type of call when the function is called.

* Sync call: When sync call is used, the return value will be serialized and returned to the caller in JSON format. The caller can get the return value for subsequent handling. For example, the calling method of function testing in the console is sync call, which can capture the function return value and display it after the call is completed.
* Async call: When async call is used, since the calling method returns right after the function is triggered, it will not wait for the function to complete execution, and the return value of the function will be discarded.

In addition, the return value will be displayed at the `ret_msg` position in the function log for both sync call and async call.

You can exit the function by calling die(). At this point, the function will be marked as execution failed, and the output from the exit using die() will also be recorded in the log.

## Log
You can use the following statements in the program to output the log:

* echo or echo()
* print or print()
* print_r()
* var_dump()

The output can be viewed at the `log` location in the function log.

## Installed Extensions

The currently installed PHP extensions are listed below for your reference. If you need other extensions, please submit a ticket to contact us.


* date
* libxml
* openssl
* pcre
* sqlite3
* zlib
* bcmath
* bz2
* calendar
* ctype
* curl
* dom
* hash
* fileinfo
* filter
* ftp
* SPL
* iconv
* json
* mbstring
* session
* standard
* mysqlnd
* PDO
* pdo_mysql
* pdo_sqlite
* Phar
* posix
* Reflection
* mysqli
* SimpleXML
* soap
* sockets
* exif
* tidy
* tokenizer
* xml
* xmlreader
* xmlwriter
* zip
* eio
* protobuf
* redis
* Zend OPcache

You can also print and view the installed extensions at any time using the `print_r(get_loaded_extensions());` code.
