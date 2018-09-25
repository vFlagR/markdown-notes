<html><link rel="stylesheet" href="../assets/css/air.css"></html>

[Home](../index.html)

# Encrypting S3

Use the below command to copy the entire of a buck on top of itself with encryption enabled. Replace the $ variables with the appropriate input.

##### Warning: Doing this action creates new markers for the items meaning lifecycle policies will see them as new. Disable any lifecycle policies on the bucket before running the below command. ##### 

~~~~
screen -dm aws s3 cp --recursive --profile $PROFILE --sse AES256 s3://$BUCKETNAME s3://$BUCKETNAME
~~~~