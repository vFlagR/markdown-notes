<html><link rel="stylesheet" href="../css/air.css"></html>

[Home](../index.html)

# Creating a bash script to pull a secure param from SSM

1. Log in to the AWS Console and navigate to Systems Manager

2. Go to Parameter Store in the bottom left of the nav

3. Create a new Parameter, give it a sensible name and choose SecureString. You can use the default SSM KMS key or create another for this specific key or perhaps a group of params that will be used as part of one project could be given a KMS key of their own.

4. Navigate to IAM and create a new user. Choose Programmatic Access. Don't give this User any permissions yet. Take a note of the Secret key and Access key you are given after creating the user, you'll need them later.

5. Go back in to the User and add an inline policy on the right hand side of the permissions block.

6. Switch to a Json view and enter the following. Make sure to update the Account Number, Region and Parameter Name

   (Note: You can get your account number by going to Support in the top right of the console then openinig the Support Dashboard. You're account number is at the top)

   ```json
   {
       "Version": "2012-10-17",
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "ssm:DescribeParameters"
               ],
               "Resource": "*"
           },
           {
               "Effect": "Allow",
               "Action": [
                   "ssm:GetParameter"
               ],
               "Resource": "arn:aws:ssm:REGION:ACCOUNT_NUMBER:parameter/PARAMETER_NAME"
           }
       ]
   }
   ```

7. Review the policy, give it a name and save.

8. Log in to the server where your script will run and edit 

      ```shell
      ~/.aws/credentials
      ```

9. Add a new profile similar to the below in to the credentials file. Use the Secret and Access keys you took note of earlier

      ```bash
      [Profile_name]
      aws_access_key_id = KEY_ID
      aws_secret_access_key = ACCCESS_KEY
      ```

10. Finnaly, create a bash script similar to the below. It will grab only the value of the Parameter from AWS and assign it to the $get_param variable. It's an unquoted string too so can be dropped in to connection strings for DB's etc.

       ```bash
       #!/bin/bash 
       
       profile=""
       param_name=""
       region="eu-west-1"
       
       get_param=$(aws ssm get-parameter --name $param_name --with-decryption --region $region --profile $profile --output text | awk '{ print $6 }')
       
       echo $get_param
       ```
