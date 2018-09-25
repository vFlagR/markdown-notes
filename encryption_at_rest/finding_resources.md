<html><link rel="stylesheet" href="../css/air.css"></html>

[Home](../index.html)

# Finding Resources

These commands can be quite useful when trying to find all of the resources of a certain account for patching/EAR purposes

**Get a list of instances by EIP**
```
aws ec2 --profile $PROFILE describe-addresses | jq -r '.Addresses[] | .PublicIp + " " + .Domain + " " + .AssociationId' >> ec2-eip.txt
```

**Get a list of Instances by Name**
~~~
aws ec2 --profile $PROFILE describe-instances | jq -r '.Reservations[].Instances[] | .InstanceId + " " + (.Tags[]|select(.Key=="Name")|.Value)' >> ec2-instances.txt
~~~