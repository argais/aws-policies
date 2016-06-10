# aws-policies
## Collection of commonly used policies

Over the time I end up needing a policy I used in the past, so why not have a collection of them right?

#### safe_automation

I use this one whenever someone asks me for a key to use with their jenkins/ansible/whatever to create instances, to avoid crappy scripts from wreaking havoc on ec2

#### allow_iam_change_password

Created a user, assigned a password, flagged to change it on first login, minutes later a ticket pops up on jira with "i cant change my password"??? Here's your solution

#### s3_website

Bucket policy. Allows read permission on all objects in a bucket, useful when you're hosting a static website on s3

#### allow_assume_admin_role

Allows another account to assume an admin role on your account. Nice when you got several accounts but centralized IAM logins in just one of them.
