# Побег из Омска

Статическая игра (один файл `index.html`).

## Деплой на свой nginx

1. Скопируй содержимое репозитория в `/var/www/omsk/` на сервере.
2. Добавь vhost (см. ниже).
3. Перезагрузи nginx.

### Пример конфига (поддомен)

```nginx
server {
    listen 80;
    server_name omsk.key-auto-trans.ru;
    root /var/www/omsk;
    index index.html;

    location / {
        try_files $uri $uri/ /index.html;
    }

    location ~* \.(html|css|js|png|jpg)$ {
        expires 1d;
        add_header Cache-Control "public";
    }
}
```

После `certbot` для HTTPS — друзья смогут открывать и с VPN, и без.
