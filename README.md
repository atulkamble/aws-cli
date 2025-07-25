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

