![[Pasted image 20221030213328.png]]

## TLDR

AWS IAM is a global service. Its used in nearly all other services to control permissions and interaction boundaries in regards to resources and services in your account. Its also required to manage users in your AWS Account or [[AWSOrganizations]]. Permissions come in the form of groups, role and policies.

### Best Practices

- Dont use your root account for anything but account setup
- One physical users should also be one AWS user
- Assign users to groups and assign permissions to groups
- Use a password policy to prevent weak passwords
- Use and enforce MFA
- Use roles for services
- Use access keys for accessing services 
- Audit permissons with IAM Credential Report
- Never share keys or user 
- Use least privilege principle

## Users

- Real persons.
- Can have multiple or no groups.

## Groups

- Collection of users.
- One group can have multiple users.

## Roles

- Intended to be used by AWS Services.
- Can be used to access cross account resources.

## Permission Boundary

- Maximum permission employees can grant to other entities.
- Uses managed policies.
- Is attached to principal (which is the AWS Account).
- Can only be set on users and roles.

## Policies

- Handles permissions.
- Attached to group, user or role as a json document.
- Should use least privilege principle.
- If a user has multiple groups his permissions will be the composition of all policies of all groups.
- Deny always overwrites any alow.
```json
{
    "Version":"date", //required
    "Id":"string", //optional
    "Statement": [ // atleast 1 required
        {
            "Sid": "", // statement id optional
            "Effect" : "", // Allow | Deny
            "Principal" : "", // which account/user/role this should be applied to (only if used to attach to a resource)
            "Action": [ // list of actions to deny or allow 
                "s3:putObject"
            ],
            "Resource":["mybucket/*"], // list of resource for which the actions are applied to
            "Condition": []//list of conditions for when this policy is applied, optional
        }
    ]
}
```
### IAM Policy Conditions

```json
"Condition": { "NumericLessThanEquals": {"aws:MultiFactorAuthAge": "3600"} }
```
- Restrict by client IP.
- Restrict by target region.
- Restrict by tag(user and ressouce).
- Force mfa.
- Account org.

### Trust Policy

- Defines/Limits which resource an asume the IAM role

## Password Policy

### Password limitations

- Minimum length.
- Include uppercase.
- Include lowercase.
- Include non alphanumeric.
- Numbers.
- No reuse.

### Other Features

- Deny or allow pw change by user himself.
- Expiration date .

## MFA

### Virtual MFA Device

- Google Auth
- Authy

### U2F (Universal 2nd Factor Security Key)

- 3rd Party device.
- Support multiple users for one device.

## IAM Security Tools

### IAM Credentials Report

- Report of all  Accounts Users and credential status (pw, accesskeys, mfa etc)

### IAM Access Advisor

- Target a single user or resource and get the info of all service permissions and when that service was lastly accessed.
- Can be used to revise policies and roles.

## IAM for S3

- **s3:ListBucket** -> **Bucket level permission**. Applies to **arn:aws:s3:::test**.
- **s3:GetObject, s3:PutObject, s3:DeleteObject** -> **Object level permission**. Applies to **arn:aws:s3:::test/***.

## Resource Policies & aws:PrincipalOrgID

- Can be used in any resource policies to restrict access to accounts that are member of an Organization.

## IAM Roles vs Resource Based Policies

- When you assume a role, you give up your original permissions and take the ones assigned to the role. When using resource-based policies, you don't give up your original permissions.
- Cross account:
  - Attach a resouce-based policy to a resource.
  - OR using a role as proxy.

## Permission Boundaries

- Use a managed policy to set the **maximum permissions** an IAM entity can get.
- Supported for Users and Roles (not groups).

<img src="attachments/iam_permissions_boundaries.png"  width="500">

- **Use cases**:
  - Delegate responsabilities to non admins.
  - Allow devs to self-assign pollicies and manage their own permissions, making sure they can't escalate their privileges.
  - Restrict one specific user (instead of a whole account using Organizations & SCP).

## IAM Policy Evaluation Logic

- DENY mata todo (?).

![[iam_permissions_evaluation.png]]

## IAM Identity Center (successor to AWS SSO)

- **One login for**:
  - AWS accounts in AWS Organizations.
  - Business cloud applications.
  - SAML 2.0 apps.
  - [[EC2]] Windows Instances.
- Identity providers:
  - Buil-in identity store.
  - 3rd party: AD, OneLogin, Okta, etc.
- Permissions are managed using **Permission Sets**.

### Fine-Grained Permissions and Assignments

- **Multi-Account Permissions**
  - Manage access across accounts in an Organization.
  - Permission Sets : one or more policies assigned to users and groups.
- **Application Assignments**
  - SSO acess to many SAML 2.0 business apps.
  - Provide required URLs, certificates and metadata.
- **Attribute-Based Access Control (ABAC)**
  - Fine-grained permissions based on user's attributes stored in IAM Identity Center Identity Store.

<img src="attachments/iam_identity_center_example.png"  width="350">

## Active Directory Setup

*See [[AWSAD]].*

- **Connect to an AWS Managed Microsoft AD**.
  - Integration out of the box.
- **Connect to Self-Managed Directory**.
  - Create two-way trust relationship using AWS Managed Microsoft AD.
  - Create an AD Connector.






