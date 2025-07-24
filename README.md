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


