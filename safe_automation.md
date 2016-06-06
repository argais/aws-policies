# Safe policy for automation users

If you ever needed to give someone a key to use on automation scripts and you never restricted it, you probably didn't sleep well considering that a rogue script could have deleted all your instances right?

User with these two policies can create instances, but only reboot/stop/terminate if they have a certain tag on it.

Yes, of course someone could go in there and remove the tag, or add the tag to other instances, but I'm not going that far.

If you need something that is immutable during the entire lifecycle of an instance, make a role mandatory and check for it.

I'll update this once I manage to get that working. If you have it, feel free to send a pull/merge request.

## Allows creating instances and tagging it

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "ec2:RunInstances",
                "ec2:CreateTags",
                "ec2:ModifyInstanceAttribute"
            ],
            "Resource": ["*"],
            "Effect": "Allow"
        }
    ]
}
```

## Restricts start/stop/reboot/terminate to instances with tag created_by_magic

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Action": [
                "ec2:StartInstances",
                "ec2:StopInstances",
                "ec2:RebootInstances",
                "ec2:TerminateInstances"
            ],
            "Condition": {
                "StringEquals": {
                    "ec2:ResourceTag/created_by_magic": "true"
                }
            },
            "Resource": [
                "arn:aws:ec2:us-east-1:<account_number_here>:instance/*"
            ],
            "Effect": "Allow"
        }
    ]
}
```
