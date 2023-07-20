# Project Cloud and Big Data

Authors: CHOUKROUN Simon, CANARIO Théo

## Project Requirements

The first part of the project requirements can be found in the `AwsDeployment` folder.

## Quiz

### IAM QUIZ:

1. 1.png: Option 3
2. 2.png: Option 1
3. 3.png: Option 3, 4
4. 4.png: Option 1
5. 5.png: Option 2
6. 6.png: Option 3
7. 7.png: Option 1

### NETWORK QUIZ:

1. 1.png: Option 3
2. 2.png: Option 3
3. 3.png: Option 1, 3, 6
4. 4.png: Option 4

## Policies Evaluation
**What actions are allowed for EC2 instances and S3 objects based on this policy? What specific resources are included?**
    The policy permits performing actions on EC2 instances, specifically allowing users to run and terminate instances. Additionally, for S3 objects, the policy allows users to get and put objects. The policy applies to all EC2 instances within the us-east-1 region associated with the AWS account 123456789012. Moreover, it grants access to all content and objects stored in the S3 bucket named example-bucket.

**Question: Under what condition does this policy allow access to VPC-related information? Which AWS region is specified?**
    The policy provides read-only access to VPC-related information, specifically allowing users to describe the VPC and its subnets used in any EC2 instance. However, there is an additional condition included in the policy, which restricts the requested region for these permissions to only us-west-2.

**Question: What actions are allowed on the "example-bucket" and its objects based on this policy? What specific prefixes are specified in the condition?**
    The policy allows certain actions on the example-bucket S3 bucket. Users are permitted to get, put, and list objects from the bucket, but only if those objects match the specified prefixes. The specific prefixes mentioned in the policy's condition are documents/* and images/*.

**Question: What actions are allowed for IAM users based on this policy? How are the resource ARNs constructed?**
    The policy allows creating and deleting IAM users. Resource ARNs use the AWS account ID and ${aws:username}. This computed value fetches the current requesting user's IAM username, tailoring policies specifically for IAM users, excluding other types like federated users, assumed roles, EC2 instances roles, and anonymous callers. Note: ${aws:username} is valid for the AWS policy file version ("2012-10-17"). The AllowIAMUserCreation policy may seem redundant as users must exist before inclusion. AllowIAMUserDeletion allows users to delete their own accounts.

    
**Which AWS service does this policy grant you access to? Does it allow you to create an IAM user, group, policy, or role? Go to https://docs.aws.amazon.com/IAM/latest/UserGuide/ and in the left navigation expand Reference > Policy Reference > Actions, Resources, and Condition Keys. Choose Identity And Access Management. Scroll to the Actions Defined by Identity And Access Management list.Name at least three specific actions that the iam:Get\* action allows.**

    This policy grants access to the IAM service, enabling users to retrieve information about IAM users, groups, policies, and roles, including listing them. However, it does not permit users to create new IAM entities. Here are some specific actions that are in the iam:Get* action allowance:

    - iam:GetUser
    - iam:GetGroup
    - iam:GetPolicy

**What actions does the policy allow?**
    The policy explicitly denies running or starting any instances of type t2.micro and t2.small in any region for any AWS account. However, it does not specify any allowance for other instance types. Therefore, by default, the policy permits these actions for all other instance types.

**Say that the policy included an additional statement object: How would the policy restrict the access granted to you by this additional statement? If the policy included both the statement on the left and the statement in question 2, could you terminate an m3.xlarge instance that existed in the account?**
    The policy grants unrestricted access to all actions and properties related to EC2 instances, thus not imposing any restrictions on EC2 access. If both statements were included in the policy, you would retain the ability to terminate an m3.xlarge instance since this instance type is not covered by the deny statement. As the deny statement does not affect termination, the policy would fall back to the second statement, which allows all actions on all EC2 instances. Consequently, you would successfully terminate an m3.xlarge instance existing in the account.

## AWS Quicksight
    All the screens are in the quicksight folder