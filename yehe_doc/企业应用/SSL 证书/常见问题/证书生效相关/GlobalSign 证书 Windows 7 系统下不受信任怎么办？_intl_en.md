## Background
As of May 27, 2019, GlobalSign officially started using a new intermediate CA to sign SSL certificates. Because there is no new root certificate support for Windows 7, websites whose GlobalSign certificates were issued (including updated or reissued certificates) after May 27, 2020 are not trusted when being accessed using Windows 7. For details, see [GlobalSign SSL Products Intermediate and Root Migration](https://support.globalsign.com/ca-certificates/root-certificates/globalsign-ssl-products-intermediate-and-root-migration).

## Solution
Use a text editor to open the CRT file in the Nginx directory of the downloaded certificate, and copy and paste the cross certificate to the end of the certificate chain. Then, restart the Nginx service for the certificate to work properly.
**To download the cross certificate,** [click here](https://da.do/t6za).
