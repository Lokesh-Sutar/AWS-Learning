# AWS cli (v2)

## Installation
Install AWS cli in arch based linux

```bash
yay -S aws-cli-v2
```

for complete guide go to:
- https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

## Configure AWS Credentials

Steps to Get Credentials:
- AWS Console
- Profile (top right corner)
- Security Credentials
- Access keys
- Create access key

Enter those credentials after following command:
```bash
aws configure
```

## Install Python Dependecies
Create Virtual Environment
```
python -m venv .venv
       OR
uv venv .venv
```

```
pip install boto3
       OR
uv pip install boto3
```