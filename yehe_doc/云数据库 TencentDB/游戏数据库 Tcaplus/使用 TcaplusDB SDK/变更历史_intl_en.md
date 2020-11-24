## TcaplusDB SDK 3.34.0.191456
Release date: April 21, 2019
New:
- pb index tables can be created, and batch query can be performed on indices.
- `callback` objects can be released for optimization in a self-service manner.
- The async mode of packet sending/receipt is optimized.
- The log feature is optimized.

Fixes:
- The `init` failure of multithreaded API objects is fixed.
- The error where GET requests couldn't support the default GET version is fixed.
- The error where repeated reconnections were made after disconnection between API and `dir` is fixed.
- The error where large `dir` return packets couldn't be called back is fixed.

## TcaplusDB SDK 3.32.0.185732
Release date: November 22, 2018
Fixes:
- The multithreaded traversal issue is fixed.

## TcaplusDB SDK 3.32.0.174230 
Release date: June 6, 2018
Fixes:
- The `RegistAllTable` error is fixed.

