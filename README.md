# Getting started with Kinesis Data Analytics Studio

## Step 1
1. Create a Cloud9 environment with all the default settings. https://console.aws.amazon.com/cloud9
2. Create an IAM role with full access to Kinesis Data Streams (AmazonKinesisFullAccess). For test purpose you can also use the default Admin policy (Select EC2 as service while creating the role).
3. Add the role to your Cloud9 environment as decribed here: https://track-and-trace-blockchain.workshop.aws/00-prerequisites/03-attach-machine-role.html

##Step 2 - working with Kinesis Data Streams
1. Create a new Kinesis Data Streams https://console.aws.amazon.com/kinesis
Data stream name: my-input-stream
Number of open shards: 2

