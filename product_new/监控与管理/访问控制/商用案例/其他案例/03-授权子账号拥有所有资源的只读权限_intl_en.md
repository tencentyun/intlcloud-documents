
A sub-account, Developer, under the enterprise account, CompanyExample, requires read-only permissions for all resources belonging to the enterprise account.

Solution A:

The enterprise account, CompanyExample, associates the Developer sub-account with the preset policy ReadOnlyAccess. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

Solution B:

Step 1: create the following policy by using policy syntax.
```
{
    "version": "2.0",
    "statement": [
        {
            "action": [
                "cvm:Describe*",
                "cvm:Inquiry*",
                "vpc:Describe*",
                "vpc:Inquiry*",
                "vpc:Get*",
                "clb:Describe*",
                "monitor:Describe*",
                "monitor:Get*",
                "bm:Describe*",
                "bmeip:Describe*",
                "bmlb:Describe*",
                "bmvpc:Describe*",
                "bm:Get*",
                "bmlb:Get*",
                "cos:List*",
                "cos:Get*",
                "cos:Head*",
                "cos:OptionsObject",
                "cas:Describe*",
                "cas:List*",
                "cas:Get*",
                "kms:List*",
                "kms:Get*",
                "ccs:Describe*",
                "ccs:Check*",
                "cam:Get*",
                "cam:List*",
                "cam:Describe*",
                "cam:Query*",
                "cdb:Describe*",
                "batch:Describe*",
                "bgpip:BasicGet*",
                "bgpip:BasicCCGet*",
                "bgpip:BasicDDoSGet*",
                "bgpip:BgpGetFpcDeviceList",
                "bgpip:BGPGetInfo",
                "bgpip:BGPGetServiceStatistics",
                "bgpip:BGPGetServicePacks",
                "bgpip:BGPCCGet*",
                "bgpip:BGPWhitelistGet",
                "bgpip:Get*",
                "bgpip:BGPIPWhitelistGet",
                "bgpip:BGPIPGet*",
                "bgpip:BGPIPDDoSGet*",
                "bgpip:BGPIPCCGet*",
                "bgpip:BgpipGetIdByTran",
                "bgpip:BgpipModifyPrice",
                "bgpip:BgpipRenewPrice",
                "bgpip:BgpipCreatePrice",
                "bgpip:BgpipQueryResources",
                "bgpip:BgpipCheckModify",
                "bgpip:BgpipCheckRenew",
                "bgpip:BgpipCheckCreate",
                "bgpip:BGPDDoSGet*",
                "ccb:ListGitAuth",
                "ccr:pull",
                "ccs:Describe*",
                "ccs:Check*",
                "ckafka:Get*",
                "ckafka:List*",
                "organization:Get*",
                "organization:List*",
                "redis:Describe*",
                "scf:Get*",
                "scf:List*",
                "shield:*Get*",
                "tag:Get*",
                "waf:WafGet*",
                "waf:WAFGetUserInfo",
                "waf:WafDownloadAlerts",
                "waf:WafPackagePrice",
                "waf:WafAreaBanGetAreas",
                "waf:WafFreqGetRuleList",
                "waf:WafAntiFakeGetUrl",
                "waf:WafDNSdetectGet*",
                "waf:BotGet*",
                "wss:CertGetList",
                "cbm:previewProductDetail",
                "cbm:agentInfo",
                "cbm:viewDeals",
                "cbm:rebateInfo",
                "cbm:businessDetail",
                "cbm:inviteClient",
                "cbm:viewClients",
                "cbm:authorize",
                "cbm:viewMessage",
                "cbm:viewMenu",
                "snova:Describe*",
                "gme:Describe*",
                "gme:Download*"
            ],
            "resource": "*",
            "effect": "allow"
        }
    ]
}
```
Step 2: associate the sub-account with the policy. To learn how to associate a policy with a user account, see [Authorization Management](https://intl.cloud.tencent.com/document/product/598/10602).

