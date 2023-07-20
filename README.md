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
    Actions allowed for EC2 instances are to run and terminate an instance, and S3 objects are to get and put an object. The specific resources included are all the EC2 instances in the us-east-1 region for the account 123456789012, and all the content/objects from the S3 example-bucket.

**Question: Under what condition does this policy allow access to VPC-related information? Which AWS region is specified?**
    Read-only access to VPC-related information is allowed only to describe the VPC (and its subnets) used in any EC2 instance. However, an extra condition is specified limiting the requested region for the permissions to us-west-2.

**Question: What actions are allowed on the "example-bucket" and its objects based on this policy? What specific prefixes are specified in the condition?**
    The actions allowed are to get, put and list objects from the bucket example-bucket if they match the given prefixes. The specific prefixes specified in the condition are documents/* and images/*.

**Question: What actions are allowed for IAM users based on this policy? How are the resource ARNs constructed?**
    The actions allowed are to create and delete an IAM user. The resource ARNs are constructed with the AWS account ID and the username. ${aws:username} is a computed value that allows to dynamically fetch the current requesting user IAM username and to allow the policies specifically for him. However, it slightly different from using * because not all AWS users have a username: only IAM users have ones, effectively excluding federated users, assumed roles, EC2 instances roles and anonymous callers such as Amazon S3 from the policy. Note: the use of the computed value ${aws:username} is valid only because we used a version of the AWS policy file that is compatible with computed values ("2012-10-17"). The AllowIAMUserCreation policy does not make much sense because in order to be included in the ressource, the user that is being created would need to already exist, however the AllowIAMUserDeletion makes sense as it allows the user to delete his own account.

    
**Which AWS service does this policy grant you access to? Does it allow you to create an IAM user, group, policy, or role? Go to https://docs.aws.amazon.com/IAM/latest/UserGuide/ and in the left navigation expand Reference > Policy Reference > Actions, Resources, and Condition Keys. Choose Identity And Access Management. Scroll to the Actions Defined by Identity And Access Management list.��Name at least three specific actions that the iam:Get* action allows.**

    This policy grants access to IAM service. It allows to retrieve information about IAM users, groups, policies and roles as well as list them, but not to create them. Here are some specific actions that are in the iam:Get* action allowance:

    - iam:GetUser
    - iam:GetGroup
    - iam:GetPolicy

**What actions does the policy allow?**
    The policy denies to run or start any instance of type t2.micro and t2.small in any region for any account. It does not specify any allowance, so by default it will allow these actions for all the other instance types.

**Say that the policy included an additional statement object: How would the policy restrict the access granted to you by this additional statement? If the policy included both the statement on the left and the statement in question 2, could you terminate an m3.xlarge instance that existed in the account?**
    It would allow all actions on all EC2 instances and properties, therefore it will not restrict any access using EC2. If the policy included both statements, you would be able to terminate an m3.xlarge instance that existed in the account because the m3.xlarge is not a condition in the deny statement, and the deny statement does not affect terminating. Therefore, as the first statement being evaluated denies running and starting t2.micro or t2.small instances, it would fallback to the second statement which allows all actions on all ec2 instances, succeeding to terminate an m3.xlarge instance that existed in the account.

## AWS Quicksight
    All the screens are in the quicksight folder