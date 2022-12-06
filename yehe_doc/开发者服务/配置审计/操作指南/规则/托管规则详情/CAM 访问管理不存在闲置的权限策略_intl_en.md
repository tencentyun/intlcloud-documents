**Description:** Checks whether there are idle permission policies in CAM.
**Compliance check logic:** If each CAM policy is associated with at least one user, user group, or rule, this rule is compliant.
**Rule ID:** `cam-policy-in-use`
**Risk level:** Low
**Supported resource types:** `QCS::CAM::Policy`
**Trigger type:** Periodic, 24 hours
**Keywords:** User, user group, role, policy
**Input parameters:** None
