# Allows another account to assume an admin role on your account.

Nice when you got several accounts but centralized IAM logins in just one of them.

Requiring MFA, cause of obvious reasons.

Create a file called admin_role_allow.json
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": "sts:AssumeRole",
            "Principal": {
                "AWS": "arn:aws:iam::<account_number_with_the_iam_users>:root"
            },
            "Effect": "Allow",
            "Condition": {
                "Bool": {
                    "aws:MultiFactorAuthPresent": true
                }
            },
            "Sid": ""
        }
    ]
}

```

Run
```
aws iam create-role --role-name AllowRemoteAdmin --assume-role-policy-document file://cloudster-role-admin.json
aws iam create-role --role-name AllowRemoteAdminReadOnly --assume-role-policy-document file://cloudster-role-admin.json
aws iam attach-role-policy --policy-arn arn:aws:iam::aws:policy/AdministratorAccess --role-name AllowRemoteAdmin
aws iam attach-role-policy --policy-arn arn:aws:iam::aws:policy/ReadOnlyAccess --role-name AllowRemoteAdminReadOnly
```

Now when using your credentials on the main account where you have your IAM users, you can assume two roles on the other account, AllowRemoteAdmin, for administrator access, and AllowRemoteAdminReadOnly so you can just look around without risking breaking anything ;)
