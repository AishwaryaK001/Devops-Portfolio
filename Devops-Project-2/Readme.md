# Launch an EC2 instance, install Apache, host a static page #
**Create & configure the EC2 instance**

**1. Steps in the console**

- Login to AWS Console → Services → EC2 → Launch instances.
- Choose Amazon Linux 2 AMI (x86_64) (Free tier eligible).
- Select t2.micro (Free tier).
- Configure instance details (defaults OK for this example).
- Add storage (defaults fine).
- Create / select a Key pair → download .pem.
- Create/select a Security group with inbound SSH (your IP) and HTTP (0.0.0.0/0).
- Launch.

**2. Connect to the EC2 instance from your local machine (SSH)**
- Set secure permissions so SSH will accept it:
  ```
  chmod 400 /path/to/my-key-pair.pem
  ```
- Find the public address
    In EC2 console, select the instance → note Public IPv4 or Public DNS (IPv4).

  SSH command (Amazon Linux 2)

- Default username for Amazon Linux is ec2-user.Replace PUBLIC_IP and the path to your key:
```
ssh -i /path/to/my-key-pair.pem ec2-user@PUBLIC_IP
```
**3. Commands to install Apache (httpd) on the EC2 instance**

Once SSH’d in as ec2-user, run these commands(Amazon Linux 2):
```
# update packages
sudo yum update -y

# install Apache (called httpd)
sudo yum install -y httpd

# start Apache now
sudo systemctl start httpd

# enable Apache to start on boot
sudo systemctl enable httpd

# check service status
sudo systemctl status httpd
```
**4. Create a basic HTML file**

Create a simple index.html on the EC2 instance.

**5. Place the HTML file in Apache’s served directory**

On Amazon Linux, the default document root is /var/www/html. 
The commands above already placed index.html there. Verify file and permissions:
```
ls -l /var/www/html
# ensure apache can read files 
sudo chown -R root:root /var/www/html
sudo chmod -R 644 /var/www/html
```
If you ever change ownership or face permission problems, ensure the web server user (usually apache or www-data) can read the files.

**6. Check from your browser if the website is working**

Open in your local browser:
```
http://PUBLIC_IP/
```
You should see the “Hello from EC2 + Apache!” page.

<p align="center">
  <img src="https://github.com/user-attachments/assets/0c9977f0-aedf-45e0-b565-ca53ae5f2515" alt="AWS S3 Screenshot" width="600">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/a5990c2c-3e82-47cf-85a3-0c69fd538784" alt="AWS S3 Screenshot" width="600">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/13447689-25e2-48e1-a35f-fc04de049612" alt="AWS S3 Screenshot" width="600">
</p>

<p align="center">
  <img src="https://github.com/user-attachments/assets/9919d467-85d3-4975-986a-2c6ae7e99a16" alt="AWS S3 Screenshot" width="600">
</p>




