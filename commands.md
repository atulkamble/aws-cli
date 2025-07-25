// aws clli 

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














