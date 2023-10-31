# Hosting a WordPress Website on AWS

This repository provides instructions on how to host a WordPress website on AWS EC2 using a MySQL server and PHP.

## Prerequisites:

- An AWS account
- A SSH client

## Steps:

### 1. Launch an EC2 instance.
![Screenshot from 2023-10-31 00-14-46](https://github.com/Sayandeep06/Hosting-a-Wordpress-website-on-AWS/assets/100061797/ea9f4c54-5aa5-4883-84f0-20d8752a327d)

#### AWS EC2 Configuration
![Screenshot from 2023-10-31 00-16-04](https://github.com/Sayandeep06/Hosting-a-Wordpress-website-on-AWS/assets/100061797/889b53d1-0d8e-4669-b244-dadc2a1d7e46)

#### EC2 Instance Setup
![Screenshot from 2023-10-31 00-16-55](https://github.com/Sayandeep06/Hosting-a-Wordpress-website-on-AWS/assets/100061797/1c5c5137-1fc2-4e0e-b555-5c82b086605b)

Launch an AWS EC2 instance with the following specifications:
- **AMI**: Ubuntu
- **Instance Type**: t2.micro
- **Storage**: 30GB
- **Security Group**: Configure to allow inbound traffic for HTTP (port 80) and HTTPS (port 443).

### 2. SSH into Your EC2 Instance.
![Screenshot from 2023-10-31 00-29-29](https://github.com/Sayandeep06/Hosting-a-Wordpress-website-on-AWS/assets/100061797/5a05e086-d7cf-49d3-abc5-db2153065113)

Use your local machine's terminal to SSH into your EC2 instance. Replace `<YourInstanceIP>` with the actual IPv4 address.

```bash
```
ssh -i .pem ubuntu@<YourInstanceIP>
# WordPress Installation on AWS EC2 Instance

This guide will walk you through the steps to install WordPress on an AWS EC2 instance using Ubuntu. You can use this setup as a starting point for your WordPress website.

## Prerequisites

Before you begin, make sure you have the following:

- An AWS EC2 instance with Ubuntu.
- SSH access to the EC2 instance.

## Installation Steps

1. **Install the Apache web server:**

    ```bash
    sudo apt-get install apache2
    ```
    ![Screenshot from 2023-10-31 00-34-57](https://github.com/Sayandeep06/Hosting-a-Wordpress-website-on-AWS/assets/100061797/aa85311e-193b-43e8-84dc-bc081471e7f2)![Screenshot from 2023-10-31 00-40-55](https://github.com/Sayandeep06/Hosting-a-Wordpress-website-on-AWS/assets/100061797/503d743f-08b5-436e-b49d-8c77b3425006)



2. **Install the MySQL server:**

    ```bash
    sudo apt-get install mysql-server
    ```
    

3. **Create a database user and database:**

    ```bash
    sudo mysql -u root
    ```

    ```sql
    CREATE USER 'wordpressuser'@'localhost' IDENTIFIED BY 'password';
    GRANT ALL PRIVILEGES ON wordpressdb.* TO 'wordpressuser'@'localhost';
    FLUSH PRIVILEGES;
    ```

    ```sql
    CREATE DATABASE wordpressdb;
    ```
    ![Screenshot from 2023-10-31 00-56-35](https://github.com/Sayandeep06/Hosting-a-Wordpress-website-on-AWS/assets/100061797/46c4235c-8c88-4e3d-9082-8410f548d9a6)


4. **Install PHP and MySQL support for PHP:**

    ```bash
    sudo apt-get install php php-mysqli
    ```
    ![Screenshot from 2023-10-31 01-12-14](https://github.com/Sayandeep06/Hosting-a-Wordpress-website-on-AWS/assets/100061797/4fe302bf-0d81-4ea0-8dbb-b438622781eb)


5. **Download and install WordPress:**

    ```bash
    cd /home
    sudo wget https://wordpress.org/latest.tar.gz
    sudo tar -xzvf wordpress.tar.gz
    cd wordpress
    ```
    

6. **Remove the default index.html file from the web server root directory:**

    ```bash
    sudo rm /var/www/html/index.html
    ```
    ![Screenshot from 2023-10-31 01-23-07](https://github.com/Sayandeep06/Hosting-a-Wordpress-website-on-AWS/assets/100061797/f7c17c2b-9903-4103-90ba-6f71a763c701)


7. **Change the ownership of the web server root directory to the www-data user:**

    ```bash
    sudo chown -R www-data:www-data /var/www/html
    ```
    ![Screenshot from 2023-10-31 01-25-23](https://github.com/Sayandeep06/Hosting-a-Wordpress-website-on-AWS/assets/100061797/5cee5d60-0447-45d9-8554-a4f8163c1032)


8. **Start the Apache web server:**

    ```bash
    sudo systemctl start apache2
    ```

9. **Open a web browser and navigate to the public DNS of the EC2 instance.**
    ![Screenshot from 2023-10-31 01-25-23](https://github.com/Sayandeep06/Hosting-a-Wordpress-website-on-AWS/assets/100061797/acd30f5d-70ae-4319-8023-9399fd222bdf)


10. **Complete the WordPress installation process.**

   - Follow the on-screen instructions to set up your WordPress site.
     ![Screenshot from 2023-10-31 01-25-23](https://github.com/Sayandeep06/Hosting-a-Wordpress-website-on-AWS/assets/100061797/7922113c-1fa0-453b-a7ff-849c7dd9d084)
     ![Screenshot from 2023-10-31 01-34-34](https://github.com/Sayandeep06/Hosting-a-Wordpress-website-on-AWS/assets/100061797/14b49352-79b2-4c55-8d87-6941b12a05b8)
     **The WordPress site is now ready**


## Additional Notes

- You can use a DNS service such as Route 53 to create a custom domain name for your WordPress website.
- You can use an AWS load balancer to distribute traffic across multiple EC2 instances.
- You can use an AWS RDS database instance to manage your WordPress database.

## Contributing

If you have any suggestions or improvements for this repository, please feel free to open a pull request.
