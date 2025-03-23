# AWS IAM Lab

This lab guides you through creating and managing IAM users, groups, and policies in AWS. It demonstrates how to control access and secure your environment using IAM best practices.

## Prerequisites

* An AWS account with administrator access.
* Basic understanding of AWS concepts.

## Lab Objectives

* Create IAM users and groups.
* Assign policies to users and groups.
* Understand and implement least privilege principles.
* Test and verify IAM permissions.
* Explore IAM policy conditions.

## Lab Steps

**1. Create IAM Groups:**

* Navigate to the IAM console in the AWS Management Console.
* Go to "User groups" and click "Create group."
* Create two groups: `Developers` and `ReadOnlyUsers`.
* Don't attach policies yet.

**2. Create IAM Users:**

* Go to "Users" and click "Add users."
* Create three users: `dev-alice`, `dev-bob`, and `read-only-charlie`.
* Select "Password - AWS Management Console access" and choose "Auto-generated password" or create a custom password.
* Uncheck "Users must create a new password at next sign-in" for simplicity in this lab.
* Download the `.csv` file containing the user credentials and store it securely.

**3. Assign Users to Groups:**

* Go to "User groups."
* Select the `Developers` group and click "Add users to group."
* Add `dev-alice` and `dev-bob` to the `Developers` group.
* Select the `ReadOnlyUsers` group and add `read-only-charlie` to the `ReadOnlyUsers` group.

**4. Create and Attach Policies:**

* Go to "Policies" and click "Create policy."
* Create a policy for the `Developers` group allowing them to create and manage S3 buckets and objects.
    * Choose the JSON editor and paste the following policy:

    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "s3:CreateBucket",
                    "s3:PutObject",
                    "s3:GetObject",
                    "s3:ListBucket",
                    "s3:DeleteObject",
                    "s3:DeleteBucket"
                ],
                "Resource": "arn:aws:s3:::*"
            }
        ]
    }
    ```

    * Name the policy `DevelopersS3Access`.
    * Create another policy for the `ReadOnlyUsers` group allowing them to list and read S3 objects:

    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "s3:ListBucket",
                    "s3:GetObject"
                ],
                "Resource": "arn:aws:s3:::*"
            }
        ]
    }
    ```

    * Name the policy `ReadOnlyS3Access`.
* Go to "User groups."
* Select the `Developers` group, go to the "Permissions" tab, and click "Attach policies."
* Attach the `DevelopersS3Access` policy.
* Select the `ReadOnlyUsers` group, go to the "Permissions" tab, and attach the `ReadOnlyS3Access` policy.

**5. Test User Permissions:**

* Open a new browser window or an incognito window.
* Log in to the AWS Management Console using the credentials for `dev-alice`.
* Navigate to the S3 console.
* Try creating a bucket, uploading objects, downloading objects, and deleting them.
* Log in to the AWS Management console using the credentials for `read-only-charlie`.
* Navigate to the S3 console.
* Try listing and downloading objects. Try creating or deleting buckets. Those actions should be denied.
* Log in as `dev-bob` and repeat the developer tests.

**6. Implement Least Privilege:**

* Edit the `DevelopersS3Access` policy to restrict access to specific S3 buckets or prefixes.
    * Modify the `Resource` section to:

    ```json
    "Resource": [
        "arn:aws:s3:::my-dev-bucket",
        "arn:aws:s3:::my-dev-bucket/*"
    ]
    ```

    * Replace `my-dev-bucket` with a bucket name of your choice.
* Modify the `ReadOnlyS3Access` policy similarly.
* Test that the users permissions have changed to the newly defined resources.

**7. Explore IAM Policy Conditions (Optional):**

* Edit the `DevelopersS3Access` policy to add a condition that restricts access based on the source IP address or a specific time range.
    * Example condition for IP restriction:

    ```json
    {
        "Effect": "Allow",
        "Action": [
            "s3:PutObject",
            "s3:GetObject",
            "s3:ListBucket"
        ],
        "Resource": "arn:aws:s3:::my-dev-bucket/*",
        "Condition": {
            "IpAddress": {
                "aws:SourceIp": "203.0.113.0/24"
            }
        }
    }
    ```

    * Example condition for time restriction:

    ```json
    {
        "Effect": "Allow",
        "Action": [
            "s3:PutObject",
            "s3:GetObject",
            "s3:ListBucket"
        ],
        "Resource": "arn:aws:s3:::my-dev-bucket/*",
        "Condition": {
            "DateGreaterThan": {
                "aws:CurrentTime": "2024-01-01T00:00:00Z"
            },
            "DateLessThan": {
                "aws:CurrentTime": "2024-12-31T23:59:59Z"
            }
        }
    }
    ```

* Test the conditions to verify that they work as expected.

**8. Cleanup:**

* Delete all S3 buckets created during the lab.
* Detach all policies from the IAM groups.
* Delete the IAM groups and users.
* Delete the IAM policies.

## Security Considerations

* Always follow the principle of least privilege.
* Use IAM roles for applications and services instead of IAM users.
* Enable MFA for all IAM users.
* Regularly review and audit IAM permissions.
* Use AWS Organizations Service Control Policies (SCPs) to enforce organization-wide permissions.

This lab provides a basic introduction to AWS IAM. You can expand it by exploring more advanced IAM features, such as IAM roles, policy variables, and service control policies.
