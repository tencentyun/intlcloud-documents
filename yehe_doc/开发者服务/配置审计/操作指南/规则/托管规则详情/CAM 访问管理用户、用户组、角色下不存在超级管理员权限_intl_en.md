**Description:** Checks whether there are super admin permissions under users, user groups, and roles in CAM.
**Compliance check logic:** If no super admin permission (AdministratorAccess) exists under users, user groups, and roles in CAM, this rule is compliant.
**Rule ID:** `cam-policy-admin-access-bound`
**Risk level:** High
**Supported resource types:** `QCS::CAM::User`, `QCS::CAM::Group`, `QCS::CAM::Role`
**Trigger type:** Periodic, 24 hours
**Keywords:** User, user group, role, policy
**Input parameters:** None

