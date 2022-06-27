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

- PHP 8.0、PHP 7.4
<table>
<tbody>
<td>
<li>Core</li>
<li>runkit7</li>
<li>date</li>
<li>libxml</li>
<li>openssl</li>
<li>pcre</li>
<li>sqlite3</li>
<li>zlib</li>
<li>bcmath</li>
</td>
<td>
<li>calendar</li>
<li>ctype</li>
<li>curl</li>
<li>dom</li>
<li>hash</li>
<li>fileinfo</li>
<li>filter</li>
<li>ftp</li>
</td>
<td>
<li>gd</li>
<li>SPL</li>
<li>iconv</li>
<li>intl</li>
<li>json</li>
<li>mbstring</li>
<li>session</li>
<li>standard</li>
</td>
<td>
<li>mysqlnd</li>
<li>PDO</li>
<li>pdo_mysql</li>
<li>pdo_sqlite</li>
<li>Phar</li>
<li>posix</li>
<li>Reflection</li>
<li>mysqli</li>
</td>
<td>
<li>SimpleXML</li>
<li>soap</li>
<li>exif</li>
<li>tokenizer</li>
<li>xml</li>
<li>xmlreader</li>
<li>xmlwriter</li>
<li>runtime</li>
</td>
</tbody>
</table>



- PHP 7.2
<table>
<tbody>
<td>
<li>Core</li>
<li>runkit7</li>
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
<li>gd</li>
<li>SPL</li>
<li>iconv</li>
<li>json</li>
</td>
<td>
<li>mbstring</li>
<li>session</li>
<li>standard</li>
<li>mysqlnd</li>
<li>PDO</li>
<li>pdo_mysql</li>
<li>pdo_sqlite</li>
<li>Phar</li>
<li>posix</li>
<li>Reflection</li>
</td>
<td>
<li>mysqli</li>
<li>SimpleXML</li>
<li>soap</li>
<li>sockets</li>
<li>exif</li>
<li>tidy</li>
<li>tokenizer</li>
<li>xml</li>
<li>xmlreader</li>
<li>xmlwriter</li>
</td>
<td>
<li>zip</li>
<li>eio</li>
<li>memcached</li>
<li>imagick</li>
<li>mongodb</li>
<li>protobuf</li>
<li>redis</li>
<li>swoole</li>
<li>Zend OPcache</li>
<li>runtime</li>
</td>
</tbody>
</table>



- PHP 5.6
<table>
<tbody>
<td>
<li>Core</li>
<li>runkit</li>
<li>date</li>
<li>ereg</li>
<li>libxml</li>
<li>openssl</li>
<li>pcre</li>
<li>sqlite3</li>
<li>zlib</li>
<li>bcmath</li>
<li>bz2</li>
<li>calendar</li>
</td>
<td>
<li>ctype</li>
<li>curl</li>
<li>dom</li>
<li>hash</li>
<li>fileinfo</li>
<li>filter</li>
<li>ftp</li>
<li>gd</li>
<li>SPL</li>
<li>iconv</li>
</td>
<td>
<li>json</li>
<li>mbstring</li>
<li>session</li>
<li>standard</li>
<li>mysqlnd</li>
<li>PDO</li>
<li>pdo_mysql</li>
<li>pdo_sqlite</li>
<li>Phar</li>
<li>posix</li>
</td>
<td>
<li>Reflection</li>
<li>mysqli</li>
<li>SimpleXML</li>
<li>soap</li>
<li>sockets</li>
<li>exif</li>
<li>tidy</li>
<li>tokenizer</li>
<li>xml</li>
<li>xmlreader</li>
</td>
<td>
<li>xmlwriter</li>
<li>zip</li>
<li>eio</li>
<li>memcached</li>
<li>imagick</li>
<li>mongodb</li>
<li>protobuf</li>
<li>redis</li>
<li>Zend OPcache</li>
<li>runtime</li>
</td>
</tbody>
</table>



