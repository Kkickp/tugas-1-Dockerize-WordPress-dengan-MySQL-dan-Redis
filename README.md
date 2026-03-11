# 🐳 Services

## 1. WordPress

Image:

```
wordpress:latest
```

Port:

```
8000:80
```

Environment variables:

```
WORDPRESS_DB_HOST=mysql:3306
WORDPRESS_DB_NAME=wordpress_db
WORDPRESS_DB_USER=wordpress_user
WORDPRESS_DB_PASSWORD=wordpress_password
```

Volume:

```
wordpress_data:/var/www/html
```

---

## 2. MySQL

Image:

```
mysql:5.7
```

Environment variables:

```
MYSQL_ROOT_PASSWORD=rootpassword
MYSQL_DATABASE=wordpress_db
MYSQL_USER=wordpress_user
MYSQL_PASSWORD=wordpress_password
```

Volume:

```
mysql_data:/var/lib/mysql
```

---

## 3. Redis

Image:

```
redis:alpine
```

Digunakan sebagai **object cache** untuk meningkatkan performa WordPress.

---

# 🚀 Cara Menjalankan Project

## 1. Clone Repository

```
git clone https://github.com/username/wordpress-docker-compose.git
cd wordpress-docker-compose
```

## 2. Jalankan Docker Compose

```
docker compose up -d
```

Docker akan menjalankan 3 container:

* WordPress
* MySQL
* Redis

---

## 3. Cek Container

```
docker ps
```

Output harus menunjukkan:

```
wordpress_app
wordpress_mysql
wordpress_redis
```

---

## 4. Akses WordPress

Buka browser:

```
http://localhost:8000
```

Lalu lakukan instalasi WordPress melalui halaman setup.

---

# ⚡ Redis Object Cache Setup

Install plugin **Redis Object Cache** di WordPress.

Kemudian tambahkan konfigurasi di `wp-config.php`:

```
define('WP_REDIS_HOST', 'redis');
define('WP_REDIS_PORT', 6379);
```

Aktifkan Redis di menu:

```
Settings → Redis → Enable Object Cache
```

---

# 🧪 Testing Redis Connection

Masuk ke container Redis:

```
docker exec -it wordpress_redis redis-cli
```

Test koneksi:

```
ping
```

Output:

```
PONG
```

---

# 💾 Data Persistence

Project ini menggunakan **Docker volumes** untuk menyimpan data:

```
wordpress_data
mysql_data
```

Keuntungan:

* Data tidak hilang saat container restart
* Database tetap tersimpan

---

# ❓ Jawaban Pertanyaan

## Kenapa perlu volume untuk MySQL?

Karena container bersifat sementara. Jika container dihapus maka data database juga hilang. Volume membuat data database tetap tersimpan.

---

## Apa fungsi depends_on?

Mengatur urutan startup container. WordPress akan dijalankan setelah MySQL dan Redis berjalan.

---

## Bagaimana WordPress connect ke MySQL?

WordPress menggunakan hostname `mysql` yang merupakan nama service di Docker Compose.

---

## Apa keuntungan Redis untuk WordPress?

Redis digunakan sebagai cache untuk:

* mempercepat loading website
* mengurangi query database
* meningkatkan performa WordPress

---

# 📦 Containers

Project ini menjalankan 3 container:

| Container       | Image            | Fungsi        |
| --------------- | ---------------- | ------------- |
| wordpress_app   | wordpress:latest | CMS WordPress |
| wordpress_mysql | mysql:5.7        | Database      |
| wordpress_redis | redis:alpine     | Cache         |

---

# 📚 Learning Outcomes

Setelah menyelesaikan project ini, mahasiswa memahami:

* Docker Compose multi-container setup
* Docker networking
* Volume persistence
* Redis caching untuk WordPress
