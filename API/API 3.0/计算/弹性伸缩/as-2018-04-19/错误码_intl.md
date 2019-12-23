
## Feature Description

If the Error field exists in the returned result, it means the API call failed. For example:

```
 {
    "Response": {
        "Error": {
            "Code": "AuthFailure.SignatureFailure",
            "Message": "The provided credentials could not be validated. Please ensure your signature is correct."
        },
        "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
    }
}
```

Code in Error indicates the error code, while Message indicates the specific information of the error.

## Error Code List

### Common Error Codes

| Error Code | Description |
|--------|------|
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA failure |
| AuthFailure.SecretIdNotFound | Key does not exist. Check whether the key has been deleted or disabled in the console, and if not, check whether the key is correctly entered. Note that there shall be no space before or after the key. |
| AuthFailure.SignatureExpire | Signature expired. The difference between the timestamp and the server time cannot exceed 5 minutes. Check whether the local time is synced with the standard time. |
| AuthFailure.SignatureFailure | Invalid signature. Signature computing error. Check the signature computing process by referring to the documentation about API authentication in the calling method. |
| AuthFailure.TokenFailure | Invalid token |
| AuthFailure.UnauthorizedOperation | The request is not authorized. For more information, see the authentication description in the [CAM](https://intl.cloud.tencent.com/document/product/598) documentation. |
| DryRunOperation | DryRun Operation. It means that the request would have succeeded, but the DryRun parameter was used. |
| FailedOperation | Operation failed |
| InternalError | Internal error |
| InvalidAction | API does not exist. |
| InvalidParameter | Incorrect parameter |
| InvalidParameterValue | Invalid parameter value |
| LimitExceeded | Quota limit is exceeded. |
| MissingParameter | A parameter is missing |
| NoSuchVersion | The API version does not exist |
| RequestLimitExceeded | The request rate limit is exceeded |
| ResourceInUse | Resource is occupied |
| ResourceInsufficient | Insufficient resource |
| ResourceNotFound | Resource does not exist |
| ResourceUnavailable | Resource is unavailable |
| UnauthorizedOperation | Unauthorized operation. |
| UnknownParameter | Unknown parameter. |
| UnsupportedOperation | Unsupported operation. |
| UnsupportedProtocol | Unsupported HTTP(S) request protocol. Only GET and POST requests are supported. |
| UnsupportedRegion | Unsupported region |

### Business Error Codes



| Error Code | Description |
|:-------|:-----|
| AccountQualificationRestrictions | The request account failed to pass the eligibility verification |
| CallCvmError | Failed to call the CVM API |
| InternalError | Internal error. |
| InvalidFilter | Invalid filter. |
| InvalidImageId.NotFound | This image cannot be found |
| InvalidLaunchConfiguration | Invalid launch configuration |
| InvalidLaunchConfigurationId | Invalid launch configuration ID |
| InvalidLaunchConfigurationId.InUse | The launch configuration is in use |
| InvalidLaunchConfigurationId.NotFound | The launch configuration is not found |
| InvalidParameter | Incorrect parameter |
| InvalidParameter.Conflict | The specified parameters conflict with each other and thus cannot be both specified |
| InvalidParameter.InScenario | Invalid parameter in specific scenarios |
| InvalidParameter.MustOneParameter | A parameter is missing. One of the two parameters must be specified. |
| InvalidParameterConflict | The two parameters conflict with each other, and cannot be both specified. |
| InvalidParameterValue | Invalid parameter value |
| InvalidParameterValue.CronExpressionIllegal | The Cron expression specified in the scheduled action is invalid |
| InvalidParameterValue.CvmConfigurationError | Exception with CVM parameter validation. |
| InvalidParameterValue.CvmError | Verification exception occurred with CVM parameter |
| InvalidParameterValue.EndTimeBeforeStartTime | The end time set for the scheduled action is earlier than the start time |
| InvalidParameterValue.Filter | Invalid filter |
| InvalidParameterValue.ForwardLb | Invalid application-based load balancer |
| InvalidParameterValue.GroupNameDuplicated | The auto scaling group name already exists. |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | Invalid characters in the scheduled action name |
| InvalidParameterValue.LaunchConfigurationNameDuplicated | The launch configuration name already exists. |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | The specified launch configuration was not found. |
| InvalidParameterValue.LbProjectInconsistent | The load balancer is in a different project. |
| InvalidParameterValue.LbVpcInconsistent | The load balancer and the auto scaling group are in different VPCs. |
| InvalidParameterValue.LifecycleHookNameDuplicated | The lifecycle hook name already exists. |
| InvalidParameterValue.LimitExceeded | The value exceeds the limit. |
| InvalidParameterValue.OnlyVpc | Only VPC is supported for the current account |
| InvalidParameterValue.Range | Parameter value is out of the specified range |
| InvalidParameterValue.ScalingPolicyNameDuplicate | The alarm policy name already exists. |
| InvalidParameterValue.ScheduledActionNameDuplicate | The scheduled action name already exists. |
| InvalidParameterValue.Size | The value of maximum, minimum, or desired number of instances in the auto scaling group is invalid. |
| InvalidParameterValue.StartTimeBeforeCurrentTime | The start time of the scheduled action is before the current time. |
| InvalidParameterValue.SubnetIds | Invalid subnet information. |
| InvalidParameterValue.TimeFormat | Invalid time format. |
| InvalidParameterValue.TooLong | Too many parameter values. |
| InvalidParameterValue.UserGroupIdNotFound | The user group does not exist. |
| InvalidPermission | The account does not support this operation. |
| LaunchConfigurationQuotaLimitExceeded | Launch configuration quota exceeds the limit |
| LimitExceeded | Quota is exceeded. |
| LimitExceeded.AutoScalingGroupLimitExceeded | The number of auto scaling groups exceeds the limit |
| LimitExceeded.DesiredCapacityLimitExceeded | The desired number of instances exceeds the limit |
| LimitExceeded.MaxSizeLimitExceeded | The maximum number of instances exceeds the upper limit |
| LimitExceeded.MinSizeLimitExceeded | The minimum number of instances falls below the lower limit |
| LimitExceeded.ScheduledActionLimitExceeded | The number of scheduled actions exceeds the limit |
| MissingParameter | Missing parameter. |
| MissingParameter.InScenario | A parameter is missing in specific scenarios |
| ResourceInUse.ActivityInProgress | A scaling activity is being executed in the auto scaling group |
| ResourceInUse.InstanceInGroup | Working instances exist in the auto scaling group |
| ResourceInsufficient.AutoScalingGroupAboveMaxSize | The maximum number of instances in the auto scaling group is exceeded. |
| ResourceInsufficient.AutoScalingGroupBelowMinSize | The number of instances in the auto scaling group is below the minimum value. |
| ResourceNotFound.AutoScalingGroupIdNotFound | The auto scaling group does not exist |
| ResourceNotFound.AutoScalingNotificationNotFound | The notification does not exist. |
| ResourceNotFound.InstancesNotFound | The specified instance does not exist. |
| ResourceNotFound.InstancesNotInAutoScalingGroup | The target instance is not in the auto scaling group. |
| ResourceNotFound.LifecycleHookInstanceNotFound | The instance corresponding to the lifecycle hook does not exist. |
| ResourceNotFound.LifecycleHookNotFound | The specified lifecycle hook was not found. |
| ResourceNotFound.LoadBalancerNotFound | The specified load balancer is not found |
| ResourceNotFound.ScalingPolicyNotFound | The alarm policy does not exist. |
| ResourceNotFound.ScheduledActionNotFound | The specified scheduled action does not exist. |
| ResourceUnavailable.AutoScalingGroupAbnormalStatus | The auto scaling group is exceptional. |
| ResourceUnavailable.AutoScalingGroupDisabled | The auto scaling group is disabled. |
| ResourceUnavailable.AutoScalingGroupInActivity | The auto scaling group is active. |
| ResourceUnavailable.CvmVpcInconsistent | The instance and the auto scaling group are in different VPCs. |
| ResourceUnavailable.InstancesAlreadyInAutoScalingGroup | The instance already exists in the auto scaling group. |
| ResourceUnavailable.LaunchConfigurationStatusAbnormal | Launch configuration is exceptional |
| ResourceUnavailable.LifecycleActionResultHasSet | The lifecycle action has already been set. |
| ResourceUnavailable.ProjectInconsistent | Inconsistent projects |
