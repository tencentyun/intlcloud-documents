## Overview
Thank you for using Tencent Cloud Game Multimedia Engine SDK. This document provides project configuration that makes it easy for Nintendo Switch developers to debug and access the APIs for Game Multimedia Engine.

## SDK Import GME Static Library

### 1. Import SDK Files
Import the GME header files and library functions into the directory where the project is located.

### 2. Import SDK Heard Files
Introducing GME header files "tmg_sdk.h" into your project.

```
#include "tmg_sdk.h"
```

### 3. Init the network module
In the project code, add the following lines to init the network module:

```
nn::nifm::Initialize();
nn::ssl::Initialize();
nn::socket::Initialize();
curl_global_init(CURL_GLOBAL_DEFAULT);
```

### 4. Execute Code
Use the GME SDK feature to call the corresponding function, please refer to the GME Sample Code.
