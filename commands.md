```
// aws clli 

aws ec2 run-instances \
  --image-id ami-0abcdef1234567890 \
  --count 1 \
  --instance-type t2.micro \
  --key-name myKey \
  --security-groups MySecGroup

aws ec2 run-instances \
  --image-id ami-08a6efd148b1f7504 \
  --subnet-id subnet-0f135e475d49526d6 \
  --instance-type t3.micro \
  --key-name jenkins \
  --security-group-ids sg-02f72ff6dbca76714 \
  --count 1

// powershell

aws ec2 run-instances --image-id ami-08a6efd148b1f7504 --subnet-id subnet-0f135e475d49526d6 --instance-type t3.micro --key-name jenkins --security-group-ids sg-02f72ff6dbca76714 --count 1

aws ec2 describe-instances

aws ec2 terminate-instances --instance-ids i-00caa767007bbbd92


aws s3 mb s3://mybucketatulkamble

echo "hello" > a.txt

// upload a.txt 

aws s3 cp a.txt s3://mybucketatulkamble

// list objects 

aws s3 ls s3://mybucketatulkamble

// download a.txt

aws s3 cp s3://mybucketatulkamble/a.txt ./

// remove a.txt 

aws s3 rm s3://mybucketatulkamble/a.txt

// delete all objects 

aws s3 rm s3://mybucketatulkamble --recursive

// remove bucket

aws s3 rb s3://mybucketatulkamble

// list all buckets 

aws s3 ls 

// list users

aws iam list-users

// list groups 

aws iam list-groups

// create user 

aws iam create-user --user-name bob

// create group

aws iam create-group --group-name dev

// add user to group

aws iam add-user-to-group --group-name dev --user-name bob 

// list users from a group 

aws iam get-group --group-name dev 

// remove user from group 

aws iam remove-user-from-group --group-name dev --user-name bob

// delete group 

aws iam delete-group --group-name dev

// delete user 

aws iam delete-user --user-name bob
```












