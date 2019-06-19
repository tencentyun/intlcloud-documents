
## Feature Description

If there is an Error field in the returned result, it means that the API call failed. For example:

```
 {
    "Response": {
        "Error": {
            "Code": "AuthFailure.SignatureFailure",
            "Message": "The provided credentials could not be validated. Please check your signature is correct."
        },
        "RequestId": "ed93f3cb-f35e-473f-b9f3-0d451b8b79c6"
    }
}
```

Code in Error indicates the error code, while Message indicates the specific information of the error.

## Error Code List

### Common Error Codes

| Error code | Description |
|--------|------|
| AuthFailure.InvalidSecretId | Invalid key (not TencentCloud API key type). |
| AuthFailure.MFAFailure | MFA error. |
| AuthFailure.SecretIdNotFound | Key does not exist. Please check whether the key has been deleted or disabled in the console. If the status is normal, please check whether the key is entered correctly. Please note that there must be no leading or trailing spaces. |
| AuthFailure.SignatureExpire | Signature expired. Timestamp and server time must not differ by more than five minutes. Please check whether the local time matches the standard time. |
| AuthFailure.SignatureFailure | Signature error. Signature calculation error. Please check the signature calculation process against the API authentication document in Calling Methods. |
| AuthFailure.TokenFailure | Token error. |
| AuthFailure.UnauthorizedOperation | Request not authorized through CAM. |
| DryRunOperation | DryRun operation, which means the request will succeed, but an unnecessary DryRun parameter is passed in. |
| FailedOperation | Operation failed. |
| InternalError | Internal error. |
| InvalidAction | API does not exist. |
| InvalidParameter | Parameter error. |
| InvalidParameterValue | Wrong parameter value. |
| LimitExceeded | Quota limit is exceeded. |
| MissingParameter | Parameter missing. |
| NoSuchVersion | API version does not exist. |
| RequestLimitExceeded | The number of requests exceeds the frequency limit. |
| ResourceInUse | Resource is in use. |
| ResourceInsufficient | Insufficient resource. |
| ResourceNotFound | Resource does not exist. |
| ResourceUnavailable | Resource not available. |
| UnauthorizedOperation | Unauthorized operation. |
| UnknownParameter | Unknown parameter error. |
| UnsupportedOperation | Unsupported operation. |
| UnsupportedProtocol | HTTP(S) request protocol error; only GET and POST requests are supported. |
| UnsupportedRegion | API does not support the passing region. |

### Business Error Codes

| Error code | Description |
|:-------|:-----|
| AccountQualificationRestrictions | The requesting account failed to pass the qualification review. |
| CallCvmError | CVM API call failed. |
| InternalError | Internal error |
| InvalidFilter | Invalid filter. |
| InvalidImageId.NotFound | The image was not found. |
| InvalidLaunchConfiguration | Invalid launch configuration. |
| InvalidLaunchConfiguration.NameDuplicate | The launch configuration name already exists. |
| InvalidLaunchConfigurationId | The launch configuration ID is invalid. |
| InvalidLaunchConfigurationId.InUse | The launch configuration is in use. |
| InvalidLaunchConfigurationId.NotFound | The launch configuration was not found. |
| InvalidParameter.Conflict | Multiple parameters specified conflict and cannot co-exist. |
| InvalidParameter.InScenario | The parameter is invalid in a specific scenario. |
| InvalidParameter.MustOneParameter | A parameter is missing. One of the two parameters must be specified. |
| InvalidParameterConflict | The two parameters specified conflict and cannot co-exist. |
| InvalidParameterValue.CronExpressionIllegal | The cron expression specified for the scheduled task is invalid. |
| InvalidParameterValue.CvmConfigurationError | Exception with CVM parameter validation. |
| InvalidParameterValue.CvmError | Exception with CVM parameter validation. |
| InvalidParameterValue.EndTimeBeforeStartTime | The end time of the scheduled task is before the start time. |
| InvalidParameterValue.Filter | Invalid filter. |
| InvalidParameterValue.ForwardLb | An application load balancer is incorrectly specified. |
| InvalidParameterValue.GroupNameDuplicate | The scaling group name already exists. |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | The scheduled task name contains invalid characters. |
| InvalidParameterValue.InvalidScheduledActionNameIncludeIllegalChar | The specified launch configuration was not found. |
| InvalidParameterValue.LbProjectInconsistent | The load balancer is in a different project. |
| InvalidParameterValue.LbVpcInconsistent | The load balancer and the scaling group are in different VPCs. |
| InvalidParameterValue.LimitExceeded | The value exceeds the limit. |
| InvalidParameterValue.OnlyVpc | The account only supports VPCs. |
| InvalidParameterValue.Range | The value is outside the specified range. |
| InvalidParameterValue.ScheduledActionNameDuplicate | The scheduled task name already exists. |
| InvalidParameterValue.Size | The value of maximum, minimum, or desired number of instances is invalid. |
| InvalidParameterValue.StartTimeBeforeCurrentTime | The start time of the scheduled task is before the current time. |
| InvalidParameterValue.SubnetIds | The subnet information is invalid. |
| InvalidParameterValue.TimeFormat | Wrong time format. |
| InvalidParameterValue.TooLong | Too many values. |
| InvalidPermission | The account does not support this operation. |
| LaunchConfigurationQuotaLimitExceeded | The launch configuration quota is exceeded. |
| LimitExceeded | Quota is exceeded. |
| LimitExceeded.AutoScalingGroupLimitExceeded | The number of scaling groups exceeds the limit. |
| LimitExceeded.DesiredCapacityLimitExceeded | The desired number of instances exceeds the limit. |
| LimitExceeded.MaxSizeLimitExceeded | The maximum number of instances exceeds the limit. |
| LimitExceeded.MinSizeLimitExceeded | The minimum number of instances is below the limit. |
| LimitExceeded.ScheduledActionLimitExceeded | The number of scheduled tasks exceeds the limit. |
| MissingParameter | Missing parameter |
| MissingParameter.InScenario | A parameter is missing in a specific scenario. |
| ResourceInUse.ActivityInProgress | The scaling group is performing a scaling activity. |
| ResourceInUse.InstanceInGroup | There are still normal instances in the scaling group. |
| ResourceInsufficient.AutoScalingGroupAboveMaxSize | The maximum number of instances in the scaling group is exceeded. |
| ResourceInsufficient.AutoScalingGroupBelowMinSize | The number of instances in the scaling group is below the minimum value. |
| ResourceNotFound.AutoScalingGroupIdNotFound | The scaling group does not exist. |
| ResourceNotFound.InstancesNotFound | The specified instance does not exist. |
| ResourceNotFound.InstancesNotInAutoScalingGroup | The target instance is not in the scaling group. |
| ResourceNotFound.LoadBalancerNotFound | The specified load balancer was not found. |
| ResourceNotFound.ScheduledActionNotFound | The specified scheduled task does not exist. |
| ResourceUnavailable.AutoScalingGroupAbnormalStatus | The scaling group is exceptional. |
| ResourceUnavailable.AutoScalingGroupDisabled | The scaling group is disabled. |
| ResourceUnavailable.AutoScalingGroupInActivity | The scaling group is active. |
| ResourceUnavailable.CvmVpcInconsistent | The instance and the scaling group are in different VPCs. |
| ResourceUnavailable.InstancesAlreadyInAutoScalingGroup | The instance already exists in the scaling group. |
| ResourceUnavailable.LaunchConfigurationStatusAbnormal | The launch configuration is exceptional. |
| ResourceUnavailable.ProjectInconsistent | Project inconsistency. |
