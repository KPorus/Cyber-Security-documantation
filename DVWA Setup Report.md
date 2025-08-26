# DVWA Setup Report

## Overview

This report documents the complete setup process for Damn Vulnerable Web Application (DVWA) on a Linux system, detailing each configuration step required to establish a functional penetration testing environment.

## Prerequisites

- Linux system with Apache2 web server
- MySQL database server
- PHP (version 8.2 or higher)
- Git for repository management


## Setup Process

### 1. DVWA Installation

**Objective**: Clone and prepare the DVWA application files

**Steps**:

1. Navigate to the web server root directory:

```bash
cd /var/www/html
```

2. Clone the DVWA repository from GitHub:

```bash
git clone https://github.com/digininja/DVWA.git
```

3. Configure the application by copying the distribution config file:

```bash
cd DVWA/config
cp config.inc.php.dist config.inc.php
```

4. Edit `config.inc.php` to update database credentials, specifically modifying the password field to match your database setup.

### 2. Database Configuration

**Objective**: Set up MySQL database with appropriate user permissions

**Steps**:

1. Start MySQL service:

```bash
sudo systemctl start mysql
```

2. Access MySQL as root user:

```bash
sudo mysql -u root
```

3. Create DVWA database user and configure permissions:

```sql
CREATE USER 'dvwa'@'localhost' IDENTIFIED BY 'your_configured_password';
GRANT ALL PRIVILEGES ON dvwa.* TO 'dvwa'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```


### 3. PHP Configuration

**Objective**: Configure PHP settings to support DVWA functionality

**Steps**:

1. Identify your PHP version:

```bash
php -v
```

2. Edit the PHP configuration file (path varies by version):

```bash
sudo nano /etc/php/8.2/apache2/php.ini
```

*Note: Version number may differ (e.g., 8.4) - verify your specific PHP version*
3. Locate and modify the following settings:
    - `allow_url_fopen = On`
    - `allow_url_include = On`

### 4. Apache2 Service Management

**Objective**: Start and configure the web server

**Steps**:

1. Start Apache2 service:

```bash
sudo systemctl start apache2
```

2. Enable Apache2 to start on boot:

```bash
sudo systemctl enable apache2
```


### 5. DVWA Database Initialization

**Objective**: Create and populate the DVWA database schema

**Steps**:

1. Access the DVWA setup page via web browser:

```
http://localhost/DVWA/setup.php
```

2. Click the "Create/Reset Database" button to initialize the database structure and sample data.

### 6. DVWA Access and Authentication

**Objective**: Access the application interface

**Steps**:

1. Navigate to the login page:

```
http://localhost/DVWA/login.php
```

2. Log in using default credentials:
    - **Username**: `admin`
    - **Password**: `password`
3. Upon successful authentication, you will be redirected to the main DVWA dashboard where various vulnerability categories are available for testing.

## Post-Setup Verification

- Confirm all DVWA modules display green status indicators on the setup page
- Verify database connectivity
- Test basic functionality by attempting a simple vulnerability exercise


## Security Considerations

- This setup is intended for educational and testing purposes only
- Ensure DVWA is deployed in an isolated environment
- Never expose DVWA to production networks or public internet
- Use this environment exclusively for authorized penetration testing practice


## Available Attack Categories

Once successfully configured, DVWA provides hands-on experience with:

- SQL Injection
- Cross-Site Scripting (XSS)
- Cross-Site Request Forgery (CSRF)
- File Upload vulnerabilities
- Command Injection
- Authentication bypass techniques

This setup provides a controlled environment for practicing ethical hacking techniques and understanding web application security vulnerabilities.

