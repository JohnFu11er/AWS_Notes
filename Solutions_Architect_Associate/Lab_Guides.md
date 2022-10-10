# Menu
- [Create and Assume roles in AWS](#41-create-and-assume-roles-in-aws)
- [Introduction to AWS Identity and Access Management (IAM)](#42-introduction-to-aws-identity-and-access-management-iam)

### 4.1 Create and Assume roles in AWS:
1. Create restricted Policy
   - Go to IAM
   - Click `Policies`
   - Click `Create Policy`
   - Click `Service`
   - Click `S3`
   - Click `All S3 actions`
   - Expand `Resources` section
   - Check all boxes except `bucket`
   - Get the `ARNs` for your buckets:
     - Open `S3` in another tab
     - Copy the bucket name that you want your policy to grant access to
   - Assign the `bucket ARN` to the policy
     - Go back to the IAM tab and click `Add ARN`
     - Paste the `ARN` of your bucket in the `Bucket name` box
     - Click `Add`
   - Click `Next: Tags`
   - Click `Next: Review`
   - Name the policy `S3RestrictedPolicy`
   - Click `Create Policy`
2. Create a Role that will use the restricted policy we just created
   - On the IAM dashboard, click on `Roles`
   - Click `Create Role`
   - Click `AWS account`
   - Click `This account`
   - Click `Next`
   - Select the `S3RestrictedPolicy` that you created in the steps above
   - Click `Next`
   - Name the role `S3RestrictedRole`
   - Click `Create Role`
3. Create a Security Token Service (STS) to allow users to assume roles
   - On the IAM dashboard, click on `Policies`
   - Click `Create Policy`
   - Click `Service`
   - Click `STS`
   - Click on arrow next to `Write`
   - Select `AssumeRole`
   - Click `Resources`
   - Click `Add ARN`
   - In the `Role name with path` field, enter `S3RestrictedRole` that you created above
   - Click `Add`
   - Click `Next: Tags`
   - Click `Next: Review`
   - Name the policy `AssumeS3Policy`
   - Click `CreatePolicy`
4. Attach a policy to a user
   - Click `AssumeS3Policy`
   - Click `Policy usage`
   - Click `Attach`
   - Select users
   - Click `Attach policy`
5. Assume a Role as a user
   - Login as the user who will assume the role, and was given access to the policy in step 4
   - Click on your user name in the top right
   - Copy `Account ID` to your clipboard for later use
   - Click on `Switch role`
   - Click `Switch Role`
   - Paste the `Account ID`
   - Type the name of your role to assume: `S3RestrictedRole`
   - Enter a display name
   - Click `Switch role`
   - You now have access at the role you selected


### 4.2 Introduction to AWS Identity and Access Management (IAM):
- Click `IAM`
- Click `User groups`
- Click `Add users`
- Select `user-1`
- Click `Add users`
- `user-1` is now part of `S3-support`
- **Note** - ANy deny statement in a json policy will allways override an allow statement.


### 5.1 S3 Replication