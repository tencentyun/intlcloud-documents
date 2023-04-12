### Common compilation errors

1. The following error information is displayed when the executable program is compiled:
```shell
   PocoCrypto.so.64: undefined reference to `PEM_write_bio_PrivateKey@libcrypto.so.10'
   libPocoNetSSL.so.64: undefined reference to `X509_check_host@libcrypto.so.10'
   ibPocoCrypto.so.64: undefined reference to `ECDSA_sign@OPENSSL_1.0.1_EC'
   libPocoCrypto.so.64: undefined reference to `CRYPTO_set_id_callback@libcrypto.so.10'
   ibPocoCrypto.so.64: undefined reference to `EVP_PKEY_id@libcrypto.so.10'
   libPocoNetSSL.so.64: undefined reference to `SSL_get1_session@libssl.so.10'
   libPocoNetSSL.so.64: undefined reference to `SSL_get_shutdown@libssl.so.10'
   libPocoCrypto.so.64: undefined reference to `EVP_PKEY_set1_RSA@libcrypto.so.10'
libPocoCrypto.so.64: undefined reference to `SSL_load_error_strings@libssl.so.10'
```
This is usually caused by the inconsistency between the project's built-in SSL version on which the POCO library compilation depends and the SSL version on your device. You need to recompile the POCO library again and replace the POCO library in `third_party`.
```shell
wget https://github.com/pocoproject/poco/archive/refs/tags/poco-1.9.4-release.zip
cd poco-poco-1.9.4-release/
./configure --omit=Data/ODBC,Data/MySQL
mkdir my_build
cd my_build
cmake .. 
make -j5
```
2. The PocoNetSSL library failed to be compiled during POCO library compilation. This is usually because the openssl-devel library is not installed.
```shell
yum install -y openssl-devel
```
3. The following error information is displayed when the executable program is compiled:
```shell
undefined reference to `qcloud_cos::CosConfig::CosConfig(std::__cxx11::basic_string<char, std::char_traits<char>, std::allocator<char> > const&)
```
This is usually caused by the inconsistency between the project's built-in GCC version used by the `libcossdk.a` compilation and the GCC version on your device. You need to recompile the POCO library and `libcossdk.a` again.
