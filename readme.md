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