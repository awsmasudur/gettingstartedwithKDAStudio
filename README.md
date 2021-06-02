# Getting started with Kinesis Data Analytics Studio

## Step 1
1. Create a Cloud9 environment with all the default settings. https://console.aws.amazon.com/cloud9
2. Create an IAM role with full access to Kinesis Data Streams (AmazonKinesisFullAccess). For test purpose you can also use the default Admin policy (Select EC2 as service while creating the role).
3. Add the role to your Cloud9 environment as decribed here: https://track-and-trace-blockchain.workshop.aws/00-prerequisites/03-attach-machine-role.html

## Step 2 - working with Kinesis Data Streams
1. Create a new Kinesis Data Streams https://console.aws.amazon.com/kinesis
Data stream name: my-input-stream
Number of open shards: 2

2. Open the Cloud9 IDE
3. In the terminal create a file "random_data_generator.py"
vi random_data_generator.py 
4. Enter the below python code

```
import datetime
import json
import random
import boto3

STREAM_NAME = "my-input-stream"


def get_random_data():
    current_temperature = round(10 + random.random() * 170, 2)
    if current_temperature > 160:
        status = "ERROR"
    elif current_temperature > 140 or random.randrange(1, 100) > 80:
        status = random.choice(["WARNING","ERROR"])
    else:
        status = "OK"
    return {
        'sensor_id': random.randrange(1, 100),
        'current_temperature': current_temperature,
        'status': status,
        'event_time': datetime.datetime.now().isoformat()
    }


def send_data(stream_name, kinesis_client):
    while True:
        data = get_random_data()
        partition_key = str(data["sensor_id"])
        print(data)
        kinesis_client.put_record(
            StreamName=stream_name,
            Data=json.dumps(data),
            PartitionKey=partition_key)


if __name__ == '__main__':
    kinesis_client = boto3.client('kinesis')
    send_data(STREAM_NAME, kinesis_client)
    
```

