# PHARMMARKA Website

## Структура сайта

```
pharmmarka_site/
├── index.html          # Главная страница
├── css/
│   └── style.css       # Стили
├── js/
│   └── main.js         # JavaScript
├── images/             # Изображения (добавьте свои)
├── videos/             # Видео (добавьте свои)
├── .htaccess           # Настройки сервера
├── robots.txt          # Для поисковиков
└── sitemap.xml         # Карта сайта
```

## Установка на VPS

### 1. Установка веб-сервера (Nginx)

```bash
# Ubuntu/Debian
sudo apt update
sudo apt install nginx

# Запуск
sudo systemctl start nginx
sudo systemctl enable nginx
```

### 2. Копирование файлов

```bash
# Создать папку
sudo mkdir -p /var/www/pharmmarka

# Скопировать файлы
sudo cp -r /path/to/pharmmarka_site/* /var/www/pharmmarka/

# Права
sudo chown -R www-data:www-data /var/www/pharmmarka
```

### 3. Настройка Nginx

```bash
sudo nano /etc/nginx/sites-available/pharmmarka
```

Добавить:

```nginx
server {
    listen 80;
    server_name pharmmarka.kz www.pharmmarka.kz;
    root /var/www/pharmmarka;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # Gzip compression
    gzip on;
    gzip_types text/css application/javascript application/json;

    # Cache static files
    location ~* \.(css|js|png|jpg|jpeg|gif|ico|svg|woff|woff2)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }
}
```

```bash
sudo ln -s /etc/nginx/sites-available/pharmmarka /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

### 4. SSL (HTTPS) — бесплатно через Let's Encrypt

```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d pharmmarka.kz -d www.pharmmarka.kz
```

### 5. Добавление видео

1. Запишите видео про агрегацию и маркировку
2. Конвертируйте в MP4 (H.264)
3. Загрузите в папку `videos/`:
   - `videos/aggregation.mp4` — про агрегацию
   - `videos/marking.mp4` — про маркировку

### 6. SEO оптимизация

- Уже настроены: meta-теги, Schema.org, Open Graph, sitemap
- Добавьте изображения в `images/og-image.jpg` для соцсетей
- Зарегистрируйте сайт в Google Search Console
- Добавьте аналитику (Google Analytics / Яндекс.Метрика)

### 7. Контактная форма

Сейчас форма показывает alert. Для отправки на email:
- Настройте backend (PHP/Node.js/Python)
- Или используйте Formspree (бесплатно): https://formspree.io
- Или Telegram бота для заявок

## Для Google индексации

1. Проверьте robots.txt доступен
2. Проверьте sitemap.xml доступен
3. Зарегистрируйтесь: https://search.google.com/search-console
4. Добавьте сайт, подтвердите владение
5. Отправьте sitemap
6. Запросите индексацию главной страницы

## Контакты

PHARMMARKA
- Тел: +7 775 56 45 171
- Email: info@pharmmarka.kz
- Адрес: Алматы, пр. Райымбека 245Б
