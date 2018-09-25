<html><link rel="stylesheet" href="../css/air.css"></html>

[Home](../index.html)

# Old AutoDeployment

##### In order to update the parameters for an old AutoDeployment follow the below steps: #####

1. SSH to the instance where AD is running and CD to the directory
~~~
cd /opt/autodeployment
~~~
2. Connect to the AutoDeployment Database
~~~
sqlite3 autodeployment.db
~~~
3. Find the deployment ID you need in order to update the correct JSON
~~~
select * from deployments;
~~~
4. After identifying the correct JSON string copy and paste it in to http://jsoneditoronline.org.
5. Make the necessary changes to the JSON string then minimise it again.
6. Go back to the database and update the relevant field using the following command:
~~~
update deployments set json='INSERT MINIMIZED JSON' where id=ID_FROM_STEP_3>;
~~~
7. Confirm the changes
~~~
select * from deployments where id=ID_FROM_STEP_3;
~~~

