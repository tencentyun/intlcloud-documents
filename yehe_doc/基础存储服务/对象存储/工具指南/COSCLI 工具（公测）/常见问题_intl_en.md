### What’s the difference between COSCLI and COSCMD?

1. COSCLI is a binary package compiled using Golang. It is ready-to-use and does not require installing any dependency before the installation and deployment. However, COSCMD is compiled in Python and requires installing the Python environment and dependency packages.
2. COSCLI supports setting an alias for a bucket, meaning that you can use a short string to represent `<BucketName-APPID>` for convenience. However, COSCMD does not support setting aliases and requires using `<BucketName-APPID>` to specify a bucket, making the commands harder to use and read.
3. COSCLI supports configuring multiple buckets in the configuration file and supports cross-bucket operations. However, with COSCMD, you can only configure one bucket in the configuration file and the commands for cross-bucket operations are long.



