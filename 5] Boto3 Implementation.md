# Boto3 Implementation

## EC2 Boto3 Important Functions
| Function                             | Purpose               |
|--------------------------------------|-----------------------|
| `run_instances()`                    | Launch EC2 instance   |
| `describe_instances()`               | View instance details |
| `terminate_instances()`              | Delete instance       |
| `stop_instances()`                   | Stop instance         |
| `start_instances()`                  | Start instance        |
| `reboot_instances()`                 | Reboot instance       |
| `create_key_pair()`                  | Create SSH key        |
| `create_security_group()`            | Create security group |
| `authorize_security_group_ingress()` | Add inbound rule      |
| `create_image()`                     | Create AMI            |
| `describe_images()`                  | List AMIs             |

## Using Client Method

### Instance

#### Create Instance
```python
import boto3

# Create EC2 client
ec2 = boto3.client('ec2', region_name='us-east-1')

# Create instance
response = ec2.run_instances(
    ImageId='ami-0f3caa1cf4417e51b',
    InstanceType='t3.micro',
    KeyName='Learning Key Pair (pem)',
    MinCount=1,
    MaxCount=1,
    TagSpecifications=[
        {
            'ResourceType': 'instance',
            'Tags': [
                {'Key': 'Name', 'Value': 'py-script'}
            ]
        }
    ]
)

print("Instance Created!")
print("Instance ID:", response['Instances'][0]['InstanceId'])
```

#### Delete/Terminate Instance
```python
import boto3

ec2 = boto3.resource('ec2', region_name='us-east-1')

instance = ec2.Instance('i-xxxxxxxxxxxxxxxxx')
instance.terminate()
instance.wait_until_terminated()

print("EC2 Instance Deleted")
```

---

### AMI (Amazon Machine Image)

#### Create AMI
```python
import boto3

ec2 = boto3.client('ec2', region_name='us-east-1')

response = ec2.create_image(
    InstanceId='i-xxxxxxxxxxxxxxxxx',
    Name='AMI-py-script',
    Description='Created via SDK (boto3)',
    NoReboot=True
)

ami_id = response['ImageId']
print("Creating AMI:", ami_id)

waiter = ec2.get_waiter('image_available')
waiter.wait(ImageIds=[ami_id])

print("AMI is available:", ami_id)
```

#### Delete AMI
```python
import boto3

region = "us-east-1"
ami_id = "ami-xxxxxxxxxxxxxxxxx"

ec2 = boto3.client('ec2', region_name=region)

image = ec2.describe_images(ImageIds=[ami_id])
snapshots = []

for bd in image['Images'][0]['BlockDeviceMappings']:
    if 'Ebs' in bd:
        snapshots.append(bd['Ebs']['SnapshotId'])

ec2.deregister_image(ImageId=ami_id)
print("AMI deregistered")

for snap in snapshots:
    ec2.delete_snapshot(SnapshotId=snap)
    print("Deleted snapshot:", snap)
```

---

### Key Pair

#### Create Key Pair
```python
import boto3

ec2 = boto3.client('ec2', region_name='us-east-1')
response = ec2.create_key_pair(KeyName='boto3')

with open('boto3.pem', 'w') as file:
    file.write(response['KeyMaterial'])

print("Key Pair Created Successfully")
```

#### List Key Pairs
```python
import boto3

ec2 = boto3.client('ec2', region_name='us-east-1')

response = ec2.describe_key_pairs()
for key in response['KeyPairs']:
    print(key['KeyName'])
```

#### Delete Key Pair
```python
import boto3

ec2 = boto3.client('ec2', region_name='us-east-1')
ec2.delete_key_pair(KeyName='boto3')
```

---

## Using Resource Method

### Create Instance
```python
import boto3

ec2 = boto3.resource('ec2', region_name='us-east-1')

instances = ec2.create_instances(
    ImageId='ami-0f3caa1cf4417e51b',
    MinCount=1,
    MaxCount=1,
    InstanceType='t3.micro',
    KeyName='Learning Key Pair (pem)'
)

for instance in instances:
    print("Instance ID:", instance.id)
```

### Terminate Instance
```python
import boto3

ec2 = boto3.resource('ec2', region_name='us-east-1')

instance = ec2.Instance('i-xxxxxxxxxxxxxxxxx')
instance.terminate()
instance.wait_until_terminated()

print("EC2 Instance Deleted")
```

### Create Key Pair (Resource)
```python
import boto3

ec2 = boto3.resource('ec2', region_name='us-east-1')

key_pair = ec2.create_key_pair(KeyName='boto3')

with open('boto3.pem', 'w') as file:
    file.write(key_pair.key_material)

print("Key Created:", key_pair.name)
```

### Delete Key Pair (Resource)
```python
import boto3

ec2 = boto3.resource('ec2', region_name='us-east-1')

key_pair = ec2.KeyPair('boto3')
key_pair.delete()

print("Key pair deleted:", key_pair.name)
```