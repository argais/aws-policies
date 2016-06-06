# Allow password change on first login for IAM users

```
{
 "Version": "2012-10-17",
 "Statement": {
   "Effect": "Allow",
   "Action": [
     "iam:ChangePassword",
     "iam:GetAccountPasswordPolicy"
   ],
   "Resource": "*"
 }
}
```
