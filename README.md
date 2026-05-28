#: Migrating Legacy System to AWS

## Overview
This project demonstrates migrating a company's 
legacy on-premise system to AWS cloud infrastructure. 
The migration involves deploying a full LAMP stack 
(Linux, Apache, MySQL, PHP) with WordPress on 
Amazon EC2, modernizing the application deployment 
and improving scalability, security, and reliability.

## Architecture
- Amazon EC2 (Ubuntu 22.04 LTS)
- Apache 2 Web Server
- MySQL 8.4 Database
- PHP 8.5
- WordPress 7.0
- AWS Security Groups (SSH, HTTP, HTTPS)

## Real World Use Case
Companies migrate legacy systems to AWS to:
- Eliminate physical server maintenance
- Improve uptime and reliability
- Scale resources based on demand
- Reduce operational costs
- Enhance security and compliance
- Enable remote management

## Tools Used
| Tool | Version | Purpose |
|------|---------|---------|
| AWS EC2 | t2.micro | Virtual server |
| Ubuntu | 22.04 LTS | Operating system |
| Apache | 2.x | Web server |
| MySQL | 8.4 | Database |
| PHP | 8.5 | Server language |
| WordPress | 7.0 | CMS platform |

## Prerequisites
- AWS Account
- SSH key pair
- Security group with ports 22, 80, 443

## Deployment Steps

### 1. Launch EC2 Instance
- AMI: Ubuntu Server 22.04 LTS
- Instance type: t2.micro
- Security group: Allow SSH, HTTP, HTTPS

### 2. Connect to EC2
```bash
ssh -i your-key.pem ubuntu@YOUR_EC2_IP
```

### 3. Update System
```bash
sudo apt update -y
sudo apt upgrade -y
```

### 4. Install LAMP Stack
```bash
# Install Apache
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2

# Install MySQL
sudo apt install mysql-server -y
sudo mysql_secure_installation

# Install PHP
sudo apt install php libapache2-mod-php php-mysql -y
```

### 5. Configure WordPress Database
```sql
CREATE DATABASE wordpress;
CREATE USER 'wpuser'@'localhost' 
IDENTIFIED BY 'WpPassword123!';
GRANT ALL PRIVILEGES ON wordpress.* 
TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
```

### 6. Install WordPress
```bash
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
sudo mv wordpress /var/www/html/
sudo chown -R www-data:www-data /var/www/html/wordpress
sudo chmod -R 755 /var/www/html/wordpress
```

### 7. Configure Apache
```bash
sudo nano /etc/apache2/sites-available/wordpress.conf
sudo a2ensite wordpress.conf
sudo a2enmod rewrite
sudo a2dissite 000-default.conf
sudo systemctl restart apache2
```

### 8. Access WordPress

http://YOUR_EC2_PUBLIC_IP

## Key Concepts Demonstrated
- Cloud migration from legacy systems
- LAMP stack deployment on AWS
- Linux server administration
- Apache virtual host configuration
- MySQL database management
- WordPress CMS deployment
- AWS security group configuration
- SSH remote server management

## Author
**Abdon Njunwa**
- GitHub: [@ABDON72](https://github.com/ABDON72)
- Certifications: AWS Solutions Architect | CompTIA A+ | CompTIA Security+
