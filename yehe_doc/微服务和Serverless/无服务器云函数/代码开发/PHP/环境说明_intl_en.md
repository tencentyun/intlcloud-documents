## PHP Version Selection

Currently, SCF supports the following versions of PHP programming language:

- PHP 8.0
- PHP 7.4
- PHP 7.2
- PHP 5.6

You can choose a desired runtime environment when creating a function, such as PHP 8.0, 7.4, 7.2, or 5.6.

## Environment Variables

The PHP environment variables built in the current PHP 8.0 and 7.4 runtime environments are as shown in the table below:

| Environment Variable Key | Specific Value or Value Source |
| ------------------ | ------------------------------------------ |
| `PHP_INI_SCAN_DIR` | /opt/php_extension:/var/user/php_extension |

The PHP environment variables built in the current PHP 7.2 and 5.6 runtime environments are as shown in the table below:

| Environment Variable Key | Specific Value or Value Source |
| ------------------ | ------------------------------------------ |
| `PHP_INI_SCAN_DIR` | /var/user/php_extension:/opt/php_extension |


For more information on environment variables, see [Environment Variables](https://intl.cloud.tencent.com/document/product/583/32748).

## List of Built-in Extensions

>!
>- For PHP 7.4 and later, the platform no longer has additional built-in dependency libraries. For more information on the dependencies required by code execution, see [Dependency Installation](https://intl.cloud.tencent.com/document/product/583/34879).
>- If the built-in extensions cannot meet your business requirements, you can install custom extensions as instructed in [Dependency Installation](https://intl.cloud.tencent.com/document/product/583/34879).
>You can print and view the installed extensions at any time by using the `print_r(get_loaded_extensions());` code.
>
The currently installed PHP extensions are listed below:



<table>
<tbody>
<td>
<li>date</li>
<li>libxml</li>
<li>openssl</li>
<li>pcre</li>
<li>sqlite3</li>
<li>zlib</li>
<li>bcmath</li>
<li>bz2</li>
<li>calendar</li>
<li>ctype</li>
</td>
<td>
<li>curl</li>
<li>dom</li>
<li>hash</li>
<li>fileinfo</li>
<li>filter</li>
<li>ftp</li>
<li>SPL</li>
<li>iconv</li>
<li>json</li>
<li>mbstring</li></td>
<td>
<li>session</li>
<li>standard</li>
<li>mysqlnd</li>
<li>PDO</li>
<li>pdo_mysql</li>
<li>pdo_sqlite</li>
<li>Phar</li>
<li>posix</li>
<li>Reflection</li>
<li>mysqli</li></td>
<td><li>SimpleXML</li>
<li>soap</li>
<li>sockets</li>
<li>exif</li>
<li>tidy</li>
<li>tokenizer</li>
<li>xml</li>
<li>xmlreader</li>
<li>xmlwriter</li>
<li>zip</li></td>
<td><li>eio</li>
<li>protobuf</li>
<li>Zend OPcache</li>
<li>mongodb</li>
<li>memcached </li>
<li>redis </li>
<li>gd2 </li>
<li>ImageMagick </li>
<li>imagick</li>
<li>swoole (PHP7)</li></td>
</tbody>
</table>



