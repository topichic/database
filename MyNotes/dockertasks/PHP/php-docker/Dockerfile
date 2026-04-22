# Используем официальный образ PHP с Apache
FROM php:8.2-apache
# Устанавливаем дополнительные расширения PHP (опционально)
RUN docker-php-ext-install pdo_mysql mysqli
# Копируем исходный код приложения в стандартную директорию Apache
COPY src/ /var/www/html/
# Устанавливаем рабочую директорию
WORKDIR /var/www/html
# Указываем, что контейнер слушает порт 80
EXPOSE 80
# Apache запускается автоматически (CMD уже есть в базовом образе)