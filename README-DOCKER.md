# iRedAdmin - Docker Setup

## ✅ Cách chạy

```bash
# Build và start
docker-compose build
docker-compose up -d

# Xem logs
docker-compose logs -f

# Truy cập web
# iRedAdmin: http://localhost:7790
# phpMyAdmin: http://localhost:8080
```

## 📊 Thông tin hệ thống

- **iRedAdmin**: http://localhost:7790
- **phpMyAdmin**: http://localhost:8080
- **Database**: MariaDB 10.11
  - Host: localhost:3306 (hoặc `mariadb` từ container)
  - Root User: root
  - Root Password: rootpassword
  - Database: iredadmin
  - User: iredadmin
  - Password: iredadmin_password

### 🔐 Đăng nhập phpMyAdmin

```
Server: mariadb
Username: root
Password: rootpassword
```

Hoặc:

```
Server: mariadb
Username: iredadmin
Password: iredadmin_password
```

## 🛠️ Quản lý

```bash
# Stop
docker-compose down

# Restart
docker-compose restart

# Restart app only
docker-compose restart app

# Xem logs
docker-compose logs -f app
docker-compose logs -f mariadb

# Truy cập database
docker exec -it iredadmin-mariadb mysql -uiredadmin -piredadmin_password iredadmin

# Xem status
docker-compose ps
```

## 📁 Cấu trúc

- **Dockerfile**: Image all-in-one chứa:
  - Python 3.11
  - uWSGI (WSGI server)
  - Nginx (Web server)
  - Supervisor (Process manager)
- **docker-compose.yml**: Orchestration 3 services:
  - MariaDB (Database)
  - App (Python + uWSGI + Nginx)
  - phpMyAdmin (Database management UI)

## 🔧 Database được tạo tự động

Database `iredadmin` sẽ tự động import schema khi khởi động lần đầu từ file `SQL/iredadmin.mysql`

## ⚠️ Lưu ý

- Warning về `version` trong docker-compose.yml là bình thường (obsolete nhưng vẫn hoạt động)
- Warning về uWSGI chạy as root có thể ignore trong môi trường dev
- Đổi passwords trong production!
