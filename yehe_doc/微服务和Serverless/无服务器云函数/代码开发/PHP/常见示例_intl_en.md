These examples provide code snippets based on PHP 7.2 for your reference.

You can click [scf-php-code-snippet](https://github.com/awesome-scf/scf-php-code-snippet) to obtain the relevant code snippets and directly use them for deployment.

## Obtaining Environment Variables

This example shows you how to obtain all or a single environment variable.

```php
<?php
function main_handler($event, $context) {
    print_r($_ENV);
    echo getenv('SCF_RUNTIME');
    return "hello world";
}
?> 
```

## Formatting Local Time

This example shows you how to output date and time in the specified format.

The SCF environment uses the UTC format by default. To output in Beijing time, you can add the `TZ=Asia/Shanghai` environment variable to the function, and use `date_default_timezone_set(getenv('TZ'));` in the function code to set the needed time zone, as shown below:

```php
<?php
function main_handler($event, $context) {
    date_default_timezone_set(getenv('TZ'));
    echo date("Y-m-d H:i:s",time()); 
    return "hello world";
}
?> 
```

## Initiating Network Connections in a Function

```php
<?php
function main_handler($event, $context) {
    $url = 'https://cloud.tencent.com';
    echo file_get_contents($url);
    return "hello world";
}
?> 
```
