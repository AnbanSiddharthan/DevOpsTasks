## Launch Linux EC2 instances in two regions using a single Terraform file.

### Step 1 — Install AWS CLI
 ```bash
 sudo apt update
 sudo apt install awscli -y
```
## Step 2 — Check AWS authentication

```bash
 aws sts get-caller-identity
```
## Step 3 — Create an IAM role for this EC2

<img width="1917" height="811" alt="image" src="https://github.com/user-attachments/assets/625c0f38-ba24-43a2-b798-81a6e0ab000c" />

## Step 4 — Install Terraform

```bash
 sudo apt update
sudo apt install -y gnupg software-properties-common
```

```bash
 wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg > /dev/null
```

```bash
 echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
```

```bash
 sudo apt update
sudo apt install terraform -y
```

```bash
 terraform --version
```
## Step 5 — Create the Terraform project

```bash
 mkdir terraform-two-regions

nano main.tf
```
#### File content 


```bash
 terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
    }
  }
}

# Region 1
provider "aws" {
  region = "eu-north-1"
}

# Region 2
provider "aws" {
  alias  = "us_east"
  region = "us-east-1"
}

# Find the latest Ubuntu 24.04 AMI in eu-north-1
data "aws_ssm_parameter" "ubuntu_eu_north" {
  name = "/aws/service/canonical/ubuntu/server/24.04/stable/current/amd64/hvm/ebs-gp3/ami-id"
}

# Find the latest Ubuntu 24.04 AMI in us-east-1
data "aws_ssm_parameter" "ubuntu_us_east" {
  provider = aws.us_east

  name = "/aws/service/canonical/ubuntu/server/24.04/stable/current/amd64/hvm/ebs-gp3/ami-id"
}

# Ubuntu EC2 in eu-north-1
resource "aws_instance" "ubuntu_eu_north" {
  ami           = data.aws_ssm_parameter.ubuntu_eu_north.value
  instance_type = "t3.micro"

  tags = {
    Name = "Ubuntu-EU-North"
  }
}

# Ubuntu EC2 in us-east-1
resource "aws_instance" "ubuntu_us_east" {
  provider      = aws.us_east
  ami           = data.aws_ssm_parameter.ubuntu_us_east.value
  instance_type = "t3.micro"

  tags = {
    Name = "Ubuntu-US-East"
  }
}

```

```bash
 terraform fmt
```

```bash
 terraform validate
```

```bash
 terraform plan
```


```bash
 terraform apply
```
### Let's verify them with AWS CLI

```bash
 aws ec2 describe-instances \
  --region eu-north-1 \
  --query 'Reservations[].Instances[].{ID:InstanceId,State:State.Name,Type:InstanceType,Name:Tags[?Key==`Name`].Value|[0]}' \
  --output table
```


```bash
 aws ec2 describe-instances \
  --region us-east-1 \
  --query 'Reservations[].Instances[].{ID:InstanceId,State:State.Name,Type:InstanceType,Name:Tags[?Key==`Name`].Value|[0]}' \
  --output table
```

### Screenshots

<img width="1917" height="1017" alt="image" src="https://github.com/user-attachments/assets/b479ed25-e47c-4a79-8d31-597a2c88f90a" />
<img width="1917" height="1015" alt="image" src="https://github.com/user-attachments/assets/fb57e4a6-d3b9-4bdc-91f0-aa652b038947" />
<img width="1917" height="1017" alt="image" src="https://github.com/user-attachments/assets/0ae5eeda-faf2-40a0-b00e-b20986d1d139" />
<img width="1917" height="1013" alt="image" src="https://github.com/user-attachments/assets/2be387b3-23fd-4fe0-a994-dfe0dbbefe3b" />
<img width="1917" height="1012" alt="image" src="https://github.com/user-attachments/assets/c5ff31a3-9ded-49c0-96c1-af28fc435051" />
<img width="1917" height="1012" alt="image" src="https://github.com/user-attachments/assets/30d086c6-1f71-46fb-8a99-9d0d8ad29c6d" />
<img width="1917" height="1020" alt="image" src="https://github.com/user-attachments/assets/97b297e6-6904-47cd-94c5-6f2309d473ef" />
<img width="1917" height="1012" alt="image" src="https://github.com/user-attachments/assets/2d4e140a-dba2-4bd2-a389-8d913a39b112" />
<img width="1917" height="1000" alt="image" src="https://github.com/user-attachments/assets/1f477698-90d1-4588-81d2-d4d8b8b1e805" />

