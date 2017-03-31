Empty repo to Java AWS Lambda

1. Create git repo on AWS CodeCommit
2. Add SSH key to AWS IAM user
3. Add policies to AWS IAM user:
    * IAMUserSSHKeys
    * IAMReadOnlyAccess
    * AWSCodeCommitFullAccess
4. git clone, open in IntelliJ
    * create readme.md ;)
    * create .gitignore
5. Setup Java project
    * get gradle wrapper
    * setup build.gradle
    * add java code
    * reopen into intellij to make gradle project
6. Setup AWS files that live in git
    * Create bucket in s3
    * Add CloudFormation input template
    * Add buildspec.yml
      * add aws cloudformation install command that produces output template
      * include output template in artifact
7. Create new role in AWS IAM
    * Role Type: AWS CloudFormation
    * Attach Policy: AWS Lambda Execute
    * Inline Custom Role Policy
      * copy from aws/cloudformation-role-policy.json
      * from http://docs.aws.amazon.com/lambda/latest/dg/automating-deployment.html
      * replace account-id and region, from upper right in aws console header
      * account-id=061121813127
      * region=us-east-1 
8. Create pipeline in AWS CodePipeline
    * Link to AWS CodeCommit repo
    * Create AWS CodeBuild project
      * Use AWS CodeBuild image: aws/codebuild/java:openjdk-8
    * Deployment provider AWS CloudFormation
      * Create or replace change set
      * template file = output template in #6
      * CAPABILITY_IAM
      * Use role in #7 for pipeline role
    * Create new IAM role for AWS Service Role
9. Pipeline will automatically run.
    * If it doesn't succeed (maybe some yml files not checked in) the pipeline won't be configured correctly (!)
10. Modify pipeline, modify Beta stage
    * Add action below
    * Deploy
    * Delpoyment provider: AWS CloudFormation
    * Action Mode: Execute a Change Set

Open questions
* aws cloudformation package command executed appears to upload to s3. how does this differ from files present in buildspec.yml?
