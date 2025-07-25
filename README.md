## 🔐 **IAM Setup (Pre-requisite)**

1. **Create IAM User (in AWS Console):**

   * Go to **IAM → Users → Add user** atul
   * Username: `atul`
   * add user to group admin 
   * Access type: ✅ **Programmatic access**
   * Group Permissions: Attach existing policies directly → ✅ **AdministratorAccess**
   * Download `.csv` file with **Access Key ID** and **Secret Access Key**

---

## 🪟 **Install AWS CLI on Windows**

### 1️⃣ Install Python (needed for pip)

* **Option 1:** Using [winget](https://learn.microsoft.com/en-us/windows/package-manager/winget/) in **PowerShell (Run as Admin)**:

  ```powershell
  winget install -e --id Python.Python.3.11
  ```

* **Option 2:** Using Chocolatey (if installed):

  ```powershell
  choco install python
  ```

* Or download manually: [https://www.python.org/](https://www.python.org/)

> ✅ Check Python version:

```powershell
python --version
```

---

### 2️⃣ Install AWS CLI

* Download installer: [AWS CLI for Windows](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

* Or install via `msiexec` (CMD as admin):

```cmd
msiexec.exe /i https://awscli.amazonaws.com/AWSCLIV2.msi
```

* ✅ Check version:

```powershell
aws --version
```

---

## 🐧 **Install AWS CLI on Linux (Ubuntu / Debian)**

### 1️⃣ Install Python (if not already installed)

```bash
sudo apt update
sudo apt install python3 python3-pip -y
python3 --version
```

### 2️⃣ Install AWS CLI (v2)

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

* ✅ Verify:

```bash
aws --version
```

---

## 🍏 **Install AWS CLI on macOS**

### 1️⃣ Install Python (optional)

* Use Homebrew:

```bash
brew install python
```

* Or download from: [https://www.python.org/](https://www.python.org/)

### 2️⃣ Install AWS CLI v2

```bash
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /
```

* ✅ Check:

```bash
aws --version
```

---

## 🔧 **Configure AWS CLI**

Once installed, configure using your IAM credentials:

```bash
aws configure
```

> You will be prompted for:

```
AWS Access Key ID [None]: <YOUR_ACCESS_KEY>
AWS Secret Access Key [None]: <YOUR_SECRET_KEY>
Default region name [None]: us-east-1
Default output format [None]: json
```

---

## ✅ **Test AWS CLI**

### 📦 Create an S3 Bucket:

```bash
aws s3api create-bucket \
  --bucket mybucketatulkamble2 \
  --region us-east-1
```

> ✅ You should get JSON response confirming the bucket creation.

### 🔍 List Buckets:

```bash
aws s3 ls
```

---

## 📚 **Helpful Links**

* AWS CLI Install Guide:
  👉 [https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)

* Python Download:
  👉 [https://www.python.org/downloads/](https://www.python.org/downloads/)

* IAM Best Practices:
  👉 [https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)


Here's a comprehensive list of essential **AWS CLI commands** for **EC2** and **S3** operations.

---

## ✅ EC2 CLI Commands

### 📋 General

| Description         | Command                                                          |
| ------------------- | ---------------------------------------------------------------- |
| List instances      | `aws ec2 describe-instances`                                     |
| Start an instance   | `aws ec2 start-instances --instance-ids i-xxxxxxxxxxxxxxxxx`     |
| Stop an instance    | `aws ec2 stop-instances --instance-ids i-xxxxxxxxxxxxxxxxx`      |
| Terminate instance  | `aws ec2 terminate-instances --instance-ids i-xxxxxxxxxxxxxxxxx` |
| Reboot instance     | `aws ec2 reboot-instances --instance-ids i-xxxxxxxxxxxxxxxxx`    |
| Get instance status | `aws ec2 describe-instance-status`                               |

---

### 🛠 Launch Instance

```bash
aws ec2 run-instances \
  --image-id ami-xxxxxxxx \
  --instance-type t2.micro \
  --key-name my-key \
  --security-groups my-sg \
  --count 1
```

---

### 🔑 Key Pairs

| Description        | Command                                     |
| ------------------ | ------------------------------------------- |
| Create key pair    | `aws ec2 create-key-pair --key-name my-key` |
| Describe key pairs | `aws ec2 describe-key-pairs`                |
| Delete key pair    | `aws ec2 delete-key-pair --key-name my-key` |

---

### 🔐 Security Groups

| Description            | Command                                                                                                 |
| ---------------------- | ------------------------------------------------------------------------------------------------------- |
| Create security group  | `aws ec2 create-security-group --group-name my-sg --description "My SG"`                                |
| Authorize inbound rule | `aws ec2 authorize-security-group-ingress --group-name my-sg --protocol tcp --port 22 --cidr 0.0.0.0/0` |
| Describe SGs           | `aws ec2 describe-security-groups`                                                                      |
| Delete SG              | `aws ec2 delete-security-group --group-name my-sg`                                                      |

---

### 📍 Elastic IP

| Description     | Command                                                                                |
| --------------- | -------------------------------------------------------------------------------------- |
| Allocate IP     | `aws ec2 allocate-address`                                                             |
| Associate IP    | `aws ec2 associate-address --instance-id i-xxxxxxxx --allocation-id eipalloc-xxxxxxxx` |
| Disassociate IP | `aws ec2 disassociate-address --association-id eipassoc-xxxxxxxx`                      |
| Release IP      | `aws ec2 release-address --allocation-id eipalloc-xxxxxxxx`                            |

---

### 📝 AMIs & Snapshots

| Description                | Command                                                        |
| -------------------------- | -------------------------------------------------------------- |
| List available AMIs        | `aws ec2 describe-images --owners self amazon`                 |
| Create image from instance | `aws ec2 create-image --instance-id i-xxxxxx --name "MyImage"` |
| Describe snapshots         | `aws ec2 describe-snapshots --owner-ids self`                  |

---

## ✅ S3 CLI Commands

### 📂 Bucket Operations

| Description          | Command                         |
| -------------------- | ------------------------------- |
| List buckets         | `aws s3 ls`                     |
| Create bucket        | `aws s3 mb s3://my-bucket-name` |
| Delete bucket        | `aws s3 rb s3://my-bucket-name` |
| List bucket contents | `aws s3 ls s3://my-bucket-name` |

---

### 📤 File Upload/Download

| Description              | Command                                       |
| ------------------------ | --------------------------------------------- |
| Upload file              | `aws s3 cp file.txt s3://my-bucket-name/`     |
| Download file            | `aws s3 cp s3://my-bucket-name/file.txt ./`   |
| Sync directory to bucket | `aws s3 sync ./mydir s3://my-bucket-name`     |
| Sync bucket to local     | `aws s3 sync s3://my-bucket-name ./local-dir` |

---

### 🧹 Delete Files

| Description             | Command                                     |
| ----------------------- | ------------------------------------------- |
| Delete file from bucket | `aws s3 rm s3://my-bucket-name/file.txt`    |
| Delete all objects      | `aws s3 rm s3://my-bucket-name --recursive` |

---

### 🌐 Static Website Hosting

| Description                | Command                                                                                               |
| -------------------------- | ----------------------------------------------------------------------------------------------------- |
| Enable website hosting     | `aws s3 website s3://my-bucket-name/ --index-document index.html --error-document error.html`         |
| Set bucket policy (public) | Via JSON file with: `aws s3api put-bucket-policy --bucket my-bucket-name --policy file://policy.json` |

---

### 🧾 Bucket Policies

| Description          | Command                                                  |
| -------------------- | -------------------------------------------------------- |
| Get bucket policy    | `aws s3api get-bucket-policy --bucket my-bucket-name`    |
| Delete bucket policy | `aws s3api delete-bucket-policy --bucket my-bucket-name` |

---

Here's a complete list of essential **AWS CLI commands for AWS IAM** operations — for managing users, groups, roles, policies, and credentials.

---

## ✅ IAM User Management

| Description      | Command                                  |
| ---------------- | ---------------------------------------- |
| List users       | `aws iam list-users`                     |
| Create user      | `aws iam create-user --user-name myuser` |
| Delete user      | `aws iam delete-user --user-name myuser` |
| Get user details | `aws iam get-user --user-name myuser`    |

---

### 🔐 Access Keys

| Description       | Command                                                                   |
| ----------------- | ------------------------------------------------------------------------- |
| Create access key | `aws iam create-access-key --user-name myuser`                            |
| List access keys  | `aws iam list-access-keys --user-name myuser`                             |
| Delete access key | `aws iam delete-access-key --access-key-id AKIAxxxxxx --user-name myuser` |

---

## 🧑‍🤝‍🧑 IAM Groups

| Description            | Command                                                                  |
| ---------------------- | ------------------------------------------------------------------------ |
| List groups            | `aws iam list-groups`                                                    |
| Create group           | `aws iam create-group --group-name mygroup`                              |
| Add user to group      | `aws iam add-user-to-group --group-name mygroup --user-name myuser`      |
| Remove user from group | `aws iam remove-user-from-group --group-name mygroup --user-name myuser` |
| Delete group           | `aws iam delete-group --group-name mygroup`                              |

---

## 📜 IAM Policies

| Description             | Command                                                                                                   |
| ----------------------- | --------------------------------------------------------------------------------------------------------- |
| List all policies       | `aws iam list-policies`                                                                                   |
| Attach policy to user   | `aws iam attach-user-policy --user-name myuser --policy-arn arn:aws:iam::aws:policy/AdministratorAccess`  |
| Detach policy from user | `aws iam detach-user-policy --user-name myuser --policy-arn arn:aws:iam::aws:policy/AdministratorAccess`  |
| Attach policy to group  | `aws iam attach-group-policy --group-name mygroup --policy-arn arn:aws:iam::aws:policy/IAMReadOnlyAccess` |
| Create inline policy    | `aws iam put-user-policy --user-name myuser --policy-name MyPolicy --policy-document file://policy.json`  |

---

## 🎭 IAM Roles

| Description             | Command                                                                                             |
| ----------------------- | --------------------------------------------------------------------------------------------------- |
| List roles              | `aws iam list-roles`                                                                                |
| Create role             | `aws iam create-role --role-name myrole --assume-role-policy-document file://trust-policy.json`     |
| Attach policy to role   | `aws iam attach-role-policy --role-name myrole --policy-arn arn:aws:iam::aws:policy/ReadOnlyAccess` |
| Detach policy from role | `aws iam detach-role-policy --role-name myrole --policy-arn arn:aws:iam::aws:policy/ReadOnlyAccess` |
| Delete role             | `aws iam delete-role --role-name myrole`                                                            |

---

## 🔎 Permissions and Validation

| Description                  | Command                                                                                                                                                                             |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Simulate user permissions    | `aws iam simulate-principal-policy --policy-source-arn arn:aws:iam::123456789012:user/myuser --action-names s3:ListBucket`                                                          |
| Get user/group/role policies | `aws iam list-attached-user-policies --user-name myuser`<br>`aws iam list-attached-group-policies --group-name mygroup`<br>`aws iam list-attached-role-policies --role-name myrole` |

---

## 📦 Example: Create Full Admin User via CLI

```bash
aws iam create-user --user-name devadmin

aws iam attach-user-policy \
  --user-name devadmin \
  --policy-arn arn:aws:iam::aws:policy/AdministratorAccess

aws iam create-access-key --user-name devadmin
```

---
# 📖 Modernized AWS CLI Quick Reference & Tutorials

Upgrade your AWS CLI skills with **practical, up-to-date commands and tutorials** covering not just IAM, EC2, and S3—but also popular services like RDS (databases), Lambda (serverless compute), VPC (networking), CloudWatch (monitoring), and more.

## 🚦 Basics: CLI Setup and Testing

**(Already covered above; no changes needed.)**

## 🏆 Newly Added: CLI Essentials for Key AWS Services

### 🗄️ RDS (Relational Database Service)

| Task                                    | Command                                                                                                   |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| List DB Instances                       | `aws rds describe-db-instances`                                                                           |
| Create MySQL Instance                   | <br>```aws rds create-db-instance --db-instance-identifier mydb --engine mysql --master-username admin --master-user-password <PASSWORD> --db-instance-class db.t3.micro --allocated-storage 20```
| Delete DB Instance                      | `aws rds delete-db-instance --db-instance-identifier mydb --skip-final-snapshot`                          |
| List Snapshots                          | `aws rds describe-db-snapshots`                                                                           |
| Create Manual Snapshot                  | `aws rds create-db-snapshot --db-instance-identifier mydb --db-snapshot-identifier mydb-snap1`           |
| Restore DB from Snapshot                | `aws rds restore-db-instance-from-db-snapshot --db-instance-identifier newdb --db-snapshot-identifier mydb-snap1` |

### 🛡️ VPC (Virtual Private Cloud)

| Task                         | Command                                                                                     |
| ---------------------------- | -------------------------------------------------------------------------------------------|
| List VPCs                    | `aws ec2 describe-vpcs`                                                                    |
| Create VPC                   | `aws ec2 create-vpc --cidr-block 10.0.0.0/16`                                              |
| List Subnets                 | `aws ec2 describe-subnets`                                                                 |
| Create Subnet                | `aws ec2 create-subnet --vpc-id vpc-xxxxxx --cidr-block 10.0.1.0/24`                       |
| List Security Groups         | `aws ec2 describe-security-groups`                                                         |
| Create Internet Gateway      | `aws ec2 create-internet-gateway`                                                          |
| Attach IGW to VPC            | `aws ec2 attach-internet-gateway --internet-gateway-id igw-xxxxxx --vpc-id vpc-xxxxxx`     |

### 💡 Lambda (Serverless Compute)

| Task                                   | Command                                                                                            |
| --------------------------------------- | -------------------------------------------------------------------------------------------------- |
| List Functions                         | `aws lambda list-functions`                                                                         |
| Create Function (from ZIP)              | `aws lambda create-function --function-name myfunc --runtime python3.9 --role arn:aws:iam::xxxx:role/lambda-role --handler lambda_function.lambda_handler --zip-file fileb://function.zip` |
| Invoke Function                        | `aws lambda invoke --function-name myfunc output.txt`                                               |
| Delete Function                        | `aws lambda delete-function --function-name myfunc`                                                 |

### 📊 CloudWatch (Logs & Alarms)

| Task                                       | Command                                                                              |
| ------------------------------------------- | ------------------------------------------------------------------------------------ |
| List Log Groups                            | `aws logs describe-log-groups`                                                       |
| Tail Log Stream                            | `aws logs tail /aws/lambda/myfunc`                                                   |
| Put Metric Alarm Example                    | <br>```aws cloudwatch put-metric-alarm --alarm-name CPUAlarm --metric-name CPUUtilization --namespace AWS/EC2 --statistic Average --period 300 --threshold 80 --comparison-operator GreaterThanOrEqualToThreshold --dimension Name=InstanceId,Value=i-xxxxxx --evaluation-periods 2 --alarm-actions arn:aws:sns:... --unit Percent```

### 🔔 SNS (Simple Notification Service)

| Task                | Command                                                             |
| ------------------- | ------------------------------------------------------------------- |
| List Topics         | `aws sns list-topics`                                               |
| Create Topic        | `aws sns create-topic --name my-topic`                              |
| Subscribe           | `aws sns subscribe --topic-arn arn:aws:sns:... --protocol email --notification-endpoint my@email.com` |
| Publish Message     | `aws sns publish --topic-arn arn:aws:sns:... --message "Hello SNS"` |
| Delete Topic        | `aws sns delete-topic --topic-arn arn:aws:sns:...`                  |

### 🕸️ SQS (Simple Queue Service)

| Task                 | Command                                                          |
| -------------------- | ---------------------------------------------------------------- |
| List Queues          | `aws sqs list-queues`                                            |
| Create Queue         | `aws sqs create-queue --queue-name myqueue`                      |
| Send Message         | `aws sqs send-message --queue-url <queue-url> --message-body "Hello"` |
| Receive Message      | `aws sqs receive-message --queue-url <queue-url>`                |
| Delete Queue         | `aws sqs delete-queue --queue-url <queue-url>`                   |

### 🌉 CloudFormation

| Task                           | Command                                                            |
| ------------------------------ | ------------------------------------------------------------------ |
| List Stacks                    | `aws cloudformation list-stacks`                                   |
| Create Stack                   | `aws cloudformation create-stack --stack-name mystack --template-body file://template.yaml` |
| Delete Stack                   | `aws cloudformation delete-stack --stack-name mystack`              |

## 🚀 Example Tutorials for Common Scenarios

### Quick EC2 Launch and Connect

1. **Launch Instance:**
    ```bash
    aws ec2 run-instances \
      --image-id ami-xxxxxx \
      --instance-type t2.micro \
      --key-name my-key \
      --security-group-ids sg-xxxxxx \
      --subnet-id subnet-xxxxxx \
      --associate-public-ip-address \
      --count 1
    ```
2. **Get Public IP:**
    ```bash
    aws ec2 describe-instances --filters Name=instance-id,Values=i-xxxxxx --query "Reservations[*].Instances[*].PublicIpAddress" --output text
    ```
3. **SSH to Instance:**
    ```bash
    ssh -i my-key.pem ubuntu@<PUBLIC_IP>
    ```

### Add an Inline IAM Policy to User

```bash
aws iam put-user-policy \
  --user-name bob \
  --policy-name s3-full-access \
  --policy-document file://s3-full-access-policy.json
```
Where `s3-full-access-policy.json` is a JSON file with your desired permissions.

### Backup and Restore RDS Instance

```bash
# Create a manual RDS snapshot
aws rds create-db-snapshot --db-instance-identifier mydb --db-snapshot-identifier mydb-snap1

# Restore new instance from snapshot
aws rds restore-db-instance-from-db-snapshot --db-instance-identifier mydb-copy --db-snapshot-identifier mydb-snap1
```

### Trigger Lambda from CLI

```bash
aws lambda invoke --function-name myfunc response.json
cat response.json
```

### Monitor EC2 Instance CPU via CloudWatch

```bash
aws cloudwatch get-metric-statistics \
  --metric-name CPUUtilization \
  --start-time 2025-07-25T00:00:00Z \
  --end-time 2025-07-25T12:00:00Z \
  --period 3600 \
  --namespace AWS/EC2 \
  --statistics Average \
  --dimensions Name=InstanceId,Value=i-xxxxxx
```

## ⚡ Pro Tips

- Use `--profile <name>` for multiple AWS accounts/profiles.
- Try adding `--output yaml` or `--output table` for more readable CLI output.
- Always check the default region (`aws configure list`) to avoid resource misplacement.
- Set `--no-cli-pager` in CLI config to suppress interactive output.

## 🔗 Quick References

- **Full AWS CLI Command Reference:** [https://docs.aws.amazon.com/cli/latest/reference/](https://docs.aws.amazon.com/cli/latest/reference/)
- **Official AWS CLI Examples:** [https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-examples.html](https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-examples.html)

This expanded guide ensures you are ready for common and advanced AWS tasks directly from your terminal. Try out these commands in a safe environment and modify placeholders (`<ids>`, `<names>`, etc.) for your use case.

Let me know if you need tutorials for any other AWS services or deeper automation examples!

Sources

