# Sturdy Guacamole

A CodeIgniter 3 web application project providing a solid foundation for building web applications with the popular PHP framework.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PHP: 7.0+](https://img.shields.io/badge/PHP-7.0%2B-blue.svg)](https://www.php.net/)

## Table of Contents

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Project Structure](#project-structure)
- [Configuration](#configuration)
- [Development](#development)
- [Database Setup](#database-setup)
- [Testing](#testing)
- [Deployment](#deployment)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## Features

- Built on CodeIgniter 3 framework
- RESTful architecture support
- MVC pattern implementation
- Database abstraction layer
- Template engine integration
- Security best practices included
- Composer dependency management
- Environment-based configuration

## Requirements

- **PHP**: 7.0 or higher
- **Composer**: Latest version
- **Database**: MySQL 5.7+ / MariaDB 10.2+
- **Web Server**: Apache/Nginx with mod_rewrite support
- **Extensions**: php-mysql, php-curl, php-gd

## Installation

### Step 1: Clone the Repository

```bash
git clone https://github.com/jobiebumpy/sturdy-guacamole.git
cd sturdy-guacamole
```

### Step 2: Install Dependencies

```bash
composer install
```

### Step 3: Configure Environment

```bash
cp .env.example .env
```

Edit `.env` and configure:
- Database credentials
- Application base URL
- Encryption key (generate with `php -r "echo bin2hex(random_bytes(16));"`
)
- Environment (development/production)

### Step 4: Set Permissions

```bash
chmod 755 application/logs
chmod 755 application/cache
mkdir -p application/logs application/cache
touch application/logs/index.html
touch application/cache/index.html
```

### Step 5: Create Database

```bash
mysql -u root -p < database/schema.sql
```

## Project Structure

```
sturdy-guacamole/
├── application/              # Application code
│   ├── controllers/         # Request handlers
│   ├── models/              # Data models
│   ├── views/               # HTML templates
│   ├── config/              # Configuration files
│   ├── logs/                # Application logs
│   └── cache/               # Cached data
├── system/                  # CodeIgniter core (don't modify)
├── public/                  # Web root
│   ├── index.php            # Application entry point
│   ├── css/                 # Stylesheets
│   ├── js/                  # JavaScript files
│   └── images/              # Images
├── vendor/                  # Composer dependencies
├── database/                # Database scripts
├── .env                     # Environment variables (local)
├── .env.example             # Environment template
├── .gitignore               # Git ignore rules
├── composer.json            # PHP dependencies
└── README.md                # This file
```

## Configuration

### Database Configuration

Edit `application/config/database.php` or set in `.env`:

```php
database.default.hostname = localhost
database.default.database = sturdy_guacamole
database.default.username = root
database.default.password = your_password
database.default.DBDriver = MySQLi
```

### Application Configuration

Edit `application/config/config.php`:

```php
$config['base_url'] = 'http://localhost:8000/';
$config['index_page'] = '';
$config['uri_protocol'] = 'REQUEST_URI';
$config['encryption_key'] = 'your_encryption_key_here';
```

## Development

### Local Server

Start a local PHP server:

```bash
php -S localhost:8000 -t public
```

Visit `http://localhost:8000` in your browser.

### Creating Controllers

Create a new controller in `application/controllers/Welcome.php`:

```php
<?php
class Welcome extends CI_Controller {
    public function index() {
        $this->load->view('welcome_message');
    }
}
```

### Creating Models

Create a new model in `application/models/User_model.php`:

```php
<?php
class User_model extends CI_Model {
    public function get_users() {
        return $this->db->get('users')->result();
    }
}
```

### Creating Views

Create views in `application/views/`:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Welcome</title>
</head>
<body>
    <h1>Welcome to Sturdy Guacamole!</h1>
</body>
</html>
```

## Database Setup

### Creating Tables

Create a `database/schema.sql` file:

```sql
CREATE TABLE IF NOT EXISTS users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(255) NOT NULL UNIQUE,
    email VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### Running Migrations

```bash
mysql -u root -p sturdy_guacamole < database/schema.sql
```

## Testing

### Running Tests

```bash
composer test
```

### Writing Tests

Create tests in `application/tests/`:

```php
<?php
use PHPUnit\Framework\TestCase;

class WelcomeControllerTest extends TestCase {
    public function testWelcomePage() {
        $this->assertTrue(true);
    }
}
```

## Deployment

### Production Checklist

- [ ] Set `CI_ENVIRONMENT = production` in `.env`
- [ ] Generate a strong encryption key
- [ ] Set `display_errors = Off` in php.ini
- [ ] Enable HTTPS
- [ ] Configure proper file permissions (644 for files, 755 for directories)
- [ ] Set up database backups
- [ ] Configure error logging
- [ ] Enable caching where appropriate
- [ ] Set up monitoring and alerting

### Deploying to Server

1. Clone repository to server
2. Install dependencies: `composer install --no-dev`
3. Configure `.env` for production
4. Set proper permissions
5. Configure web server (Apache/Nginx)
6. Set up SSL certificate
7. Configure firewall rules

## Troubleshooting

### Common Issues

**404 Errors on All Pages**
- Ensure mod_rewrite is enabled: `a2enmod rewrite`
- Check `.htaccess` in public directory
- Verify base URL in config

**Database Connection Error**
- Verify MySQL is running: `systemctl status mysql`
- Check credentials in `.env`
- Ensure database exists: `mysql -u root -p -e "SHOW DATABASES;"`

**Permission Denied Errors**
- Fix permissions: `chmod -R 755 application/logs application/cache`
- Ensure web server user owns files

**Blank Page**
- Check `application/logs/` for error messages
- Enable error display in development: `error_reporting(E_ALL);`

## Contributing

We welcome contributions! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/awesome-feature`
3. Commit changes: `git commit -am 'Add awesome feature'`
4. Push to branch: `git push origin feature/awesome-feature`
5. Submit a Pull Request

### Code Style

- Follow PSR-2 coding standards
- Use 4 spaces for indentation
- Document all public methods with PHPDoc
- Write meaningful commit messages

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For issues, questions, or suggestions, please [open an issue](https://github.com/jobiebumpy/sturdy-guacamole/issues) on GitHub.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for version history and updates.

---

**Last Updated**: June 2026
**Maintained by**: jobiebumpy
