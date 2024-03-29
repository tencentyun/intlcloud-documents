>!Since the product logic no longer meets the technical development of game industry, Game Player Matching GPM will be deprecated on June 1st, 2022. Please complete service migration before May 31 , 2022.

This document describes the security mechanism of GPM event notifications to help you identify reliable event messages and improve business security.

## Prerequisites

- You have [created a match](https://intl.cloud.tencent.com/document/product/1072/39203) and obtained a MatchCode.
- When creating or editing a match, you have configured the URL notification address for the MatchCode.

## MatchToken Introduction

MatchToken acts as a key that is used to verify the reliability of MatchCode event notifications. This verification can increase your business security and avoid forged messages.


## MatchToken Generation and Update

You need to call the [`ModifyToken`](https://intl.cloud.tencent.com/document/product/1072/39905) API to manually generate or update a **MatchToken** for a match. When specifying request parameters of this API, you can specify `MatchToken` parameter to customize a token. If this parameter is left empty, a random token will be generated by GPM. You also need to specify `CompatibleSpan`, during which, GPM will send both the old and new MatchTokens.

For a MatchCode, the MatchToken change interval should be at least three minutes.


## MatchToken Query

Call the [`DescribeToken`](https://intl.cloud.tencent.com/document/product/1072/39906) API to query the latest MatchToken of the specified MatchCode.


## MatchToken Verification

You need to record the latest MatchToken after every setting or update. Check whether this MatchToken is the same as that of the event message.

For a MatchCode configured with MatchToken, its **MatchTokens** field of each event message contains all effective MatchTokens (including the latest and all MatchTokens within the specified `CompatibleSpan` period).

​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        

