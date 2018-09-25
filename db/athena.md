<html><link rel="stylesheet" href="../assets/css/air.css"></html>

[Home](../index.html)

# Athena

There are a few default Athena queries you can run in order to make an Athena table for various AWS Services. These can be found below:

**Note: Make sure to change the TableName and BucketName variables.**

##### S3 Bucket Access Logs:

~~~sql
CREATE EXTERNAL TABLE IF NOT EXISTS DATABASE.TABLE_NAME (
  BucketOwner string,
  Bucket string,
  RequestDateTime string,
  RemoteIP string,
  Requester string,
  RequestID string,
  Operation string,
  Key string,
  RequestURI_operation string,
  RequestURI_key string,
  RequestURI_httpProtoversion string,
  HTTPstatus string,
  ErrorCode string,
  BytesSent string,
  ObjectSize string,
  TotalTime string,
  TurnAroundTime string,
  Referrer string,
  UserAgent string,
  VersionId string)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.RegexSerDe'
WITH SERDEPROPERTIES (
 'serialization.format' = '1',
  'input.regex' = '([^ ]*) ([^ ]*) \\[(.*?)\\] ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) \\\"([^ ]*) ([^ ]*) (- |[^ ]*)\\\" (-|[0-9]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*) (\"[^\"]*\") ([^ ]*)$'
) LOCATION 's3://BUCKETNAME/'
~~~
##### CloudFront Logs

~~~sql
CREATE EXTERNAL TABLE IF NOT EXISTS DATABASE.TABLE_NAME (
  `date` DATE,
  time STRING,
  location STRING,
  bytes BIGINT,
  requestip STRING,
  method STRING,
  host STRING,
  uri STRING,
  status INT,
  referrer STRING,
  useragent STRING,
  querystring STRING,
  cookie STRING,
  resulttype STRING,
  requestid STRING,
  hostheader STRING,
  requestprotocol STRING,
  requestbytes BIGINT,
  timetaken FLOAT,
  xforwardedfor STRING,
  sslprotocol STRING,
  sslcipher STRING,
  responseresulttype STRING,
  httpversion STRING,
  filestatus STRING,
  encryptedfields INT
)
ROW FORMAT DELIMITED 
FIELDS TERMINATED BY '\t'
LOCATION 's3://BUCKETNAME'
TBLPROPERTIES ( 'skip.header.line.count'='2' )
~~~

##### ELB (Classic LoadBalancer)

~~~sql
CREATE EXTERNAL TABLE IF NOT EXISTS DATABASE.TABLE_NAME (
 request_timestamp string,
 elb_name string,
 request_ip string,
 request_port int,
 backend_ip string,
 backend_port int,
 request_processing_time double,
 backend_processing_time double,
 client_response_time double,
 elb_response_code string,
 backend_response_code string,
 received_bytes bigint,
 sent_bytes bigint,
 request_verb string,
 url string,
 protocol string,
 user_agent string,
 ssl_cipher string,
 ssl_protocol string
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.RegexSerDe'
WITH SERDEPROPERTIES (
 'serialization.format' = '1',
 'input.regex' = '([^ ]*) ([^ ]*) ([^ ]*):([0-9]*) ([^ ]*)[:\-]([0-9]*) ([-.0-9]*) ([-.0-9]*) ([-.0-9]*) (|[-0-9]*) (-|[-0-9]*) ([-0-9]*) ([-0-9]*) \\\"([^ ]*) ([^ ]*) (- |[^ ]*)\\\" (\"[^\"]*\") ([A-Z0-9-]+) ([A-Za-z0-9.-]*)$' )
LOCATION 's3://BUCKETNAME/';
~~~

##### ALB (Application Load Balancer)

~~~sql
CREATE EXTERNAL TABLE IF NOT EXISTS DATABASE.TABLE_NAME (
    type string,
    time string,
    elb string,
    client_ip string,
    client_port int,
    target_ip string,
    target_port int,
    request_processing_time double,
    target_processing_time double,
    response_processing_time double,
    elb_status_code string,
    target_status_code string,
    received_bytes bigint,
    sent_bytes bigint,
    request_verb string,
    request_url string,
    request_proto string,
    user_agent string,
    ssl_cipher string,
    ssl_protocol string,
    target_group_arn string,
    trace_id string,
    domain_name string,
    chosen_cert_arn string,
    matched_rule_priority string,
    request_creation_time string,
    actions_executed string,
    redirect_url string,
    new_field string
    )
    ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.RegexSerDe'
    WITH SERDEPROPERTIES (
    'serialization.format' = '1',
    'input.regex' = 
'([^ ]*) ([^ ]*) ([^ ]*) ([^ ]*):([0-9]*) ([^ ]*)[:-]([0-9]*) ([-.0-9]*) ([-.0-9]*) ([-.0-9]*) (|[-0-9]*) (-|[-0-9]*) ([-0-9]*) ([-0-9]*) \"([^ ]*) ([^ ]*) (- |[^ ]*)\" \"([^\"]*)\" ([A-Z0-9-]+) ([A-Za-z0-9.-]*) ([^ ]*) \"([^\"]*)\" \"([^\"]*)\" \"([^\"]*)\" ([-.0-9]*) ([^ ]*) \"([^\"]*)\"($| \"[^ ]*\")(.*)')
    LOCATION 's3://BUCKETNAME/';
~~~

##### VPC Flow Logs

~~~sql
CREATE EXTERNAL TABLE IF NOT EXISTS DATABASE.TABLE_NAME (
  version int,
  account string,
  interfaceid string,
  sourceaddress string,
  destinationaddress string,
  sourceport int,
  destinationport int,
  protocol int,
  numpackets int,
  numbytes int,
  starttime int,
  endtime int,
  action string,
  logstatus string
)  
PARTITIONED BY (dt string)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ' '
LOCATION 's3://BUCKETNAME/'
TBLPROPERTIES ("skip.header.line.count"="1");
~~~

