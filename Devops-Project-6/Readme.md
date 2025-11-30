🌐 # AWS S3 Static Website Hosting Using Terraform #

A beginner-friendly Infrastructure as Code (IaC) project that deploys a fully functional static website hosted on Amazon S3, built and managed using Terraform. The website files (HTML/CSS) are stored in S3, and S3 website hosting is enabled for public access.

**Flow:

- Launch EC2 with IAM Role
- Install Terraform on EC2
- Run Terraform code to create S3 Website
- Upload index.html
- Access the public S3 Website URL

Devops-Project-6/
│
├── README.md                # Project documentation
│
├── terraform/               # All Terraform IaC files
│   ├── provider.tf
│   ├── main.tf
│   ├── variables.tf
│   └── output.tf
│
├── website/                 # Static website files
    ├── index.html



🟦 **Step 1: Launch an EC2 Instance**

Choose:
Amazon Linux 2 AMI
t2.micro (Free tier)
VPC/Subnet: Default
Allow SSH (Port 22)
Key pair: Create and download

🟦 **Step 2: Create an IAM Role & Attach to EC2**

**IAM Role ➝ EC2 Role**

Go to IAM → Roles → Create Role
Choose AWS Service → EC2
Attach permission:AmazonS3FullAccess
Give a role name:EC2-S3-Terraform-Role
After EC2 launches → Actions → Security → Modify IAM Role
Attach the role.

🟦 **Step 3: SSH into EC2**

From your laptop/terminal:
```
ssh -i mykey.pem ec2-user@EC2_PUBLIC_IP
```

🟦 **Step 4: Install Terraform on EC2**
```
sudo yum install -y yum-utils
sudo yum-config-manager --add-repo https://rpm.releases.hashicorp.com/AmazonLinux/hashicorp.repo
sudo yum -y install terraform
terraform -v
```

🟦 **Step 5: Create Project Directory**
```
mkdir Devops-Project-6/terraform
cd wDevops-Project-6/terraform
```

🟦 **Step 6: Create Terraform Files (copy/paste from file)**
```
nano provider.tf
nano main.tf
nano variables.tf
nano output.tf
```

✔ provider.tf

Tells Terraform to use AWS.

Defines the AWS region (like ap-south-1).

✔ variables.tf

Lets you input bucket name and region.

Good practice for reusability.

✔ main.tf

Creates an S3 bucket.

Enables static website hosting.

Makes the bucket publicly readable.

Creates website index/error configuration.

✔ output.tf

Shows you the website URL after terraform apply.


🟦 **Step 7: Initialize Terraform**
```
terraform init
```
🟦 **Step 8: Run Terraform Plan**
```
terraform plan -var="bucket_name=my-demo-portfolio-123"
```
🟦 **Step 9: Apply Terraform**
```
terraform apply -var="bucket_name=my-demo-portfolio-123" -auto-approve
```
Output will display something like:
```
s3_website_endpoint = "my-demo-portfolio-123.s3-website.ap-south-1.amazonaws.com"
```
🟦 **Step 10: Create index.html on EC2**
```
nano index.html
```
Paste the HTML portfolio code.

🟦 **Step 11: Upload HTML File to S3 Bucket**

```
aws s3 cp index.html s3://my-demo-portfolio-123/
```

🟦 **Step 12:Public S3 Bucket Policy (Allow website access)**

Update the "Resource" ARN with your bucket name:
```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": [
        "s3:GetObject"
      ],
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
    }
  ]
}
```

✅ Why Do We Need This Public S3 Bucket Policy?

When you enable static website hosting in S3, the website files must be public so anyone on the internet can open them (e.g., index.html).
But by default, S3 blocks all public access.
You attach it ONLY after you create the S3 bucket.
You would attach it in the Permissions → Bucket Policy section of S3.

🟦 **Step 13: Open Your Website 🎉**

Open the endpoint from Terraform output:
```
http://my-demo-portfolio-123.s3-website.ap-south-1.amazonaws.com
```

Your static website is now live.

🟦 **Destroy All Resources**

To delete everything created by Terraform:
```
terraform destroy -var="bucket_name=my-demo-portfolio-123"
```


