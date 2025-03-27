# Banking System - Daily Progress Report

## Date: March 27, 2025

## Overview
Today, we focused on managing Docker containers, troubleshooting MySQL service issues, and migrating the database from SQLite to MySQL for our Banking System project. The main goal was to ensure seamless database integration and stable application deployment.

## Tasks Completed

### 1. Docker Management
- **Building and Deploying Containers**
  - We used Docker Compose to build and start the required containers for our banking system.
    ```sh
    docker-compose build
    docker-compose up -d
    ```
- **Checking Running Containers**
  - Verified that the MySQL container was running properly:
    ```sh
    docker ps | grep mysql
    ```
- **Inspecting Application Logs**
  - Checked logs to debug issues in the banking system container:
    ```sh
    docker logs banking_system --follow
    ```
- **Accessing the Container Shell**
  - Connected to the running banking system container for manual checks:
    ```sh
    docker exec -it banking_system bash
    ```

### 2. Database Migration from SQLite to MySQL
- **Updating Django Settings**
  - Modified `settings.py` to use MySQL instead of SQLite:
    ```python
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.mysql',
            'NAME': 'banking_db',
            'USER': 'root',
            'PASSWORD': 'rootpass',
            'HOST': 'host.docker.internal',
            'PORT': '3306',
        }
    }
    ```
- **Checking Database Connection**
  - Verified that MySQL was running and accessible:
    ```sh
    docker exec -it mysql_db mysql -u root -p -e "SHOW DATABASES;"
    ```
- **Running Migrations**
  - Applied Django migrations to set up the MySQL database schema:
    ```sh
    docker exec -it banking_system python manage.py migrate
    ```
- **Listing Migrations**
  - Checked if migrations were properly applied:
    ```sh
    docker exec -it banking_system python manage.py showmigrations
    ```

### 3. MySQL Service Management
- **Starting MySQL Manually**
  - Restarted MySQL service for troubleshooting:
    ```sh
    sudo systemctl start mysql
    ```
- **Checking MySQL Status**
  - Verified if MySQL was active and running:
    ```sh
    systemctl status mysql.service
    ```
- **Accessing the MySQL Database**
  - Logged into MySQL shell to inspect database records:
    ```sh
    mysql -u root -p
    ```
- **Checking Existing Tables**
  - Verified tables inside the MySQL database:
    ```sh
    USE banking_db;
    SHOW TABLES;
    ```

### 4. Cleanup and Optimization
- **Stopping and Removing Containers**
  - Shut down the banking system and database containers:
    ```sh
    docker stop banking_system mysql_db
    docker rm banking_system mysql_db
    ```
- **Pruning Unused Docker Resources**
  - Removed all stopped containers, networks, and images:
    ```sh
    docker system prune -a -f
    ```
- **Rebuilding Containers from Scratch**
  - Used the `--no-cache` option to ensure a fresh build:
    ```sh
    docker-compose build --no-cache
    docker-compose up -d
    ```

## Challenges Faced
- **Database Connection Issues**
  - Faced issues with MySQL service failing to start inside the container.
  - Resolved by restarting MySQL and checking logs for errors.
- **Permission Denied Errors**
  - Some MySQL operations required elevated privileges, so we had to adjust user permissions.
- **Docker Volume Persistence**
  - Ensured MySQL data was not lost by mounting persistent volumes.

## Next Steps
- Perform further testing to confirm successful migration.
- Optimize database queries for better performance.
- Implement additional security measures for database access.
- Automate backup solutions for database integrity.

## Notes
- Code and database configurations have been updated.
- Further discussion planned for tomorrow to finalize testing.

---
**Prepared by:** [Your Name]
