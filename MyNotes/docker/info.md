# Полное руководство и команды

## 📜 История Docker
Docker был представлен в 2013 году компанией dotCloud как инструмент для упрощения развертывания приложений. В 2014 году вышла версия 1.0, и Docker стал открытым стандартом для контейнеризации. Сегодня это промышленный стандарт для упаковки и доставки приложений.

## 🛠 ПОЛНЫЙ СПИСОК КОМАНД

### Управление контейнерами
```bash
# Запуск контейнера
docker run [ОПЦИИ] ОБРАЗ [КОМАНДА]
docker run -d -p 8080:80 --name my-nginx nginx
docker run -it ubuntu:20.04 /bin/bash

# Просмотр контейнеров
docker ps          # активные контейнеры
docker ps -a       # все контейнеры
docker ps -q       # только ID контейнеров

# Остановка и запуск
docker stop КОНТЕЙНЕР      # корректная остановка
docker start КОНТЕЙНЕР     # запуск остановленного
docker restart КОНТЕЙНЕР   # перезапуск
docker pause КОНТЕЙНЕР     # приостановка
docker unpause КОНТЕЙНЕР   # возобновление

# Удаление
docker rm КОНТЕЙНЕР        # удалить контейнер
docker rm -f КОНТЕЙНЕР     # принудительно удалить работающий
docker container prune     # удалить все остановленные контейнеры
```
##
# Поиск и загрузка
```bash
docker search ТЕРМИН        # поиск в Docker Hub
docker pull ОБРАЗ:ТЕГ      # загрузка образа
docker pull nginx:alpine

# Просмотр и удаление
docker images               # список образов
docker image ls             # альтернатива
docker rmi ОБРАЗ           # удаление образа
docker image prune         # удалить неиспользуемые образы

# Сборка образов
docker build -t ИМЯ:ТЕГ .
docker build -f Dockerfile.dev .  # указать другой Dockerfile
```
##

# Логи
```bash
docker logs КОНТЕЙНЕР      # показать логи
docker logs -f КОНТЕЙНЕР   # логи в реальном времени
docker logs --tail 50 КОНТЕЙНЕР  # последние 50 строк

# Выполнение команд
docker exec [ОПЦИИ] КОНТЕЙНЕР КОМАНДА
docker exec -it КОНТЕЙНЕР /bin/bash    # интерактивная оболочка
docker exec КОНТЕЙНЕР ls -la           # выполнить команду

# Инспекция
docker inspect КОНТЕЙНЕР    # детальная информация
docker stats               # статистика использования ресурсов
docker top КОНТЕЙНЕР       # процессы в контейнере
```
##


# Пример полноценного DOCKERFILLE
```bash
# Базовый образ
FROM python:3.9-slim

# Метаданные
LABEL maintainer="your.email@example.com"
LABEL version="1.0"
LABEL description="Мое приложение на Python"

# Рабочая директория
WORKDIR /app

# Установка зависимостей системы
RUN apt-get update && apt-get install -y \
    gcc \
    && rm -rf /var/lib/apt/lists/*

# Копирование зависимостей
COPY requirements.txt .

# Установка Python зависимостей
RUN pip install --no-cache-dir -r requirements.txt

# Копирование кода приложения
COPY . .

# Переменные окружения
ENV PYTHONUNBUFFERED=1
ENV APP_PORT=8000

# Открытие порта
EXPOSE 8000

# Health check
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD curl -f http://localhost:8000/health || exit 1

# Команда запуска
CMD ["python", "app.py"]