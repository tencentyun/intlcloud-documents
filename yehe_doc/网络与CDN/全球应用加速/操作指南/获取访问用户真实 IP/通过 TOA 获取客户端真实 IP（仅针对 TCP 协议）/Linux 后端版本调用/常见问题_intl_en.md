### A signature error occurred "module verification failed: signature and/or required key missing - tainting kernel"

- Module signature verification is a kernel feature, which needs to be enabled through the Linux kernel compilation. 
- Solution 1: When compiling the kernel, add `CONFIG_MODULE_SIG=n`.
- Solution 2: Sign the kernel module with the certificate, as shown below:
  /usr/src/linux-4.9.61/scripts/sign-file sha512/usr/src/linux-4.9.61/certs/signing_key.pem /usr/src/linux-4.9.61/certs/signing_key.x509 toa.ko

  

### The /lib/modules directory is missing during compilation

- This error is often associated with the following situations:
- The kernel package is not installed.
- When the directory is modified, you need to correct it by yourself.
- When the kernel does not have the build directory, you need to manually create a soft link to the exact version of the kernel header.
cd /lib/modules/4.9.0-13-amd64 && ln -s /usr/src/linux-headers-4.9.0-13-amd64 build
