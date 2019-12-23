# Configuring TCCLI

## Operation Scenarios

This document describes how to configure TCCLI International Version.

## Prerequisites

TCCLI has been installed.

## Directions

To use TCCLI, you need to complete its initial configuration to make it meet the prerequisites of using TencentCloud API.

1. You can enter the interactive mode for quick configuration by running the `tccli configure` command:

   ```bash
   $ tccli configure
   TencentCloud API secretId [*afcQ]:AKIDwLw1234MMfPRle2g9nR2OTI787aBCDP
   TencentCloud API secretKey [*ArFd]:OxXj7khcV1234dQSSYNABcdCc1LiArFd
   region: ap-guangzhou
   output[json]:
   ```

   - **secretId**: TencentCloud API key's SecretId.
   - **secretIKey**: TencentCloud API key's SecretKey.
   - **region:** Tencent Cloud product region. Please go to the corresponding product page to get the information on available regions.
   - **output:** Output format of the request return packet, which is optional. Valid values: json, table, text. Default value: json.
     For more information, please run the `ccli configure help` command.

2. In command line mode, you can configure the information in an automated script:

   ```bash
   # The `set` subcommand can set certain configuration items or multiple configurations simultaneously.
   tccli configure set secretId AKIDwLw1234MMfPRle2g9nR2OTI787aBCDP
   tccli configure set region ap-guangzhou  output json
   # The `get` subcommand is used to obtain configuration information.
   tccli configure get secretKey
   secretKey = OxXj7khcV1234dQSSYNABcdCc1LiArFd
   # The `list` subcommand prints out all configuration information.
   tccli configure list
   credential:
   secretId =  AKIDwLw1234MMfPRle2g9nR2OTI787aBCDP
   secretKey =  OxXj7khcV1234dQSSYNABcdCc1LiArFd
   configure:
   region =  ap-guangzhou
   output =  json
   ```

   For more information, please run the following command:

   ```
   tccli configure [list get set] help
   ```

    

3. TCCLI supports multiple accounts, making it easier for you to use multiple configurations at the same time.

   ```sh
   Specify the account name `test` in interactive mode.
   $ tccli configure --profile test
   TencentCloud API secretId [*BCDP]:AKIDwLw1234MMfPRle2g9nR2OTI787aBCDP
   TencentCloud API secretKey [*ArFd]:OxXj7khcV1234dQSSYNABcdCc1LiArFd
   region: ap-guangzhou
   output[json]:
   # Specify the account name `test` for set/get/list subcommands
   tccli configure set region ap-guangzhou  output json  --profile test
   tccli configure get secretKey      --profile test
   tccli configure list      --profile test
   Specify an account when calling an API (e.g., cvm DescribeZones API).
   tccli cvm DescribeZones --profile test
   ```