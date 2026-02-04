## Информация по работе с Dockerfile

<<<<<<< HEAD
### Создание контейнера с приложением на Python с помощью Dockerfile

1. Создайм bash скрипт `installPython_3_9.sh` для создания контейнера
```shell
#!/bin/bash
# Создайте тестовое приложение
mkdir test-app && cd test-app

# app.py
cat > app.py << EOF
from flask import Flask, jsonify
import time

app = Flask(__name__)

# Имитация долгой инициализации
print("Starting application...")
time.sleep(2)  # Задержка 2 секунды для инициализации
print("Application ready!")

@app.route('/')
def hello():
    return jsonify({"message": "Hello Docker!"})

@app.route('/health')
def health():
    return jsonify({"status": "healthy"}), 200

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=8000, debug=False)
EOF

# requirements.txt
echo "Flask==2.3.3" > requirements.txt

# .dockerignore
echo "__pycache__" > .dockerignore

# Исправленный Dockerfile
cat > Dockerfile << 'EOF'
FROM python:3.9-slim

RUN apt-get update && apt-get install -y \
    gcc \
    curl \
    && rm -rf /var/lib/apt/lists/*

RUN useradd -m -u 1000 appuser
USER appuser

WORKDIR /home/appuser/app

COPY --chown=appuser:appuser requirements.txt .
RUN pip install --no-cache-dir --user -r requirements.txt

ENV PATH="/home/appuser/.local/bin:${PATH}"

COPY --chown=appuser:appuser . .

ENV PYTHONUNBUFFERED=1 \
    FLASK_APP=app.py \
    FLASK_ENV=production

EXPOSE 8000

# Увеличиваем start-period до 30 секунд
HEALTHCHECK --interval=30s --timeout=10s --start-period=30s --retries=3 \
    CMD curl -f http://localhost:8000/health || exit 1

CMD ["python", "app.py"]
EOF

# Сборка и запуск
docker build -t myapp .
docker run -d -p 8000:8000 --name myapp-container myapp
# myapp-container - имя контейнера, myapp - имя образа
docker ps  # Проверяем статус
curl http://localhost:8000/  # Тестируем
```

Данный скрипт следует создать в отдельной папке Docker-проектов

2. Запустить созданный скрипт:
```shell
bash installPython_3_9.sh
```

Скрипт создайт нужный каталог и файлы в нём, загрузит всё необходимое и сразу протестирует результат.

3. Мониторинг и информация

Проверить статус

Только работающие
```shell
docker ps
```

Все контейнеры (включая остановленные)
```shell
docker ps -a
```

Фильтр по имени
```shell
docker ps -a --filter "name=myapp"
```

Подробная информация о контейнере
```shell
docker inspect myapp-container
```

Логи контейнера

Последние логи
```shell
docker logs myapp-container
```

Логи в реальном времени (follow)
```shell
docker logs -f myapp-container
```

Последние 50 строк
```shell
docker logs --tail 50 myapp-container
```

Логи за последние 5 минут
```shell
docker logs --since 5m myapp-container
```

Статистика использования ресурсов

В реальном времени
```shell
docker stats myapp-container
```

Однократный вывод
```shell
docker stats --no-stream myapp-container
```

Управление жизненным циклом

Остановка контейнера

Graceful остановка (SIGTERM)
```shell
docker stop myapp-container
```

Ждать 30 сек перед SIGKILL
```shell
docker stop -t 30 myapp-container
```

Принудительная остановка

Немедленно (SIGKILL)
```shell
docker kill myapp-container
```

Запуск остановленного контейнера
```shell
docker start myapp-container
```

Перезапуск контейнера
```shell
docker restart myapp-container
```

Пауза и возобновление

Приостановить все процессы
```shell
docker pause myapp-container
```

Возобновить
```shell
docker unpause myapp-container
```

Удаление контейнера

Удалить остановленный
```shell
docker rm myapp-container
```

Принудительно удалить работающий
```shell
docker rm -f myapp-container
```

Взаимодействие с контейнером

# Запуск команд внутри контейнера

Эта команда не понятна и не сработала!
```shell
docker exec myapp-container ls -la /app
```

Проверка версии Python в контейнере
```shell
docker exec myapp-container python --version
```

Интерактивный терминал
```shell
docker exec -it myapp-container /bin/bash
```

Для alpine образов
```shell
docker exec -it myapp-container /bin/sh
```

Копирование файлов

Из контейнера на хост
```shell
docker cp myapp-container:/app/logs.txt ./
```

С хоста в контейнер
```shell
docker cp ./config.yaml myapp-container:/app/
```

Проверка портов

Какие порты проброшены
```shell
docker port myapp-container
```

Выйти из командной строки контейнера
```shell
exit
```

Управление образом myapp

Список образов
```shell
docker images
```
```shell
docker image ls
```

Поиск образа
```shell
docker images | grep myapp
```

Информация об образе
```shell
docker image inspect myapp
```

История сборки образа
```shell
docker history myapp
```

Тегирование образов

Создать тег v1.0 (что это?)
```shell
docker tag myapp myapp:v1.0
```

Тег latest
```shell
docker tag myapp myapp:latest      # Тег latest
```

# Для Docker Hub
```shell
docker tag myapp username/myapp:latest
```

Удаление образа

Удалить если нет контейнеров
```shell
docker rmi myapp
```

Принудительное удаление
```shell
docker rmi -f myapp
```

Сохранение и загрузка

Экспорт образа в файл
```shell
docker save -o myapp.tar myapp
```

Импорт образа из файла
```shell
docker load -i myapp.tar
```

Экспорт контейнера
```shell
docker export -o myapp-container.tar myapp-container
```
```shell
docker import myapp-container.tar myapp:snapshot
```

Пересборка и обновление

Полный цикл разработки
```shell
docker stop myapp-container
```
```shell
docker rm myapp-container
```
```shell
docker rmi myapp
```
```shell
docker build -t myapp .
```
```shell
docker run -d -p 8000:8000 --name myapp-container myapp
```

Сокращенный вариант (автоматическая пересоздание)

Если используете docker-compose
```shell
docker-compose up --build
```

Отладка и диагностика

Проверка работы приложения
```shell
curl http://localhost:8000/health
```

Посмотреть процессы внутри контейнера
```shell
docker top myapp-container
```

Проверить использование ресурсов
```shell
docker stats myapp-container
```

Посмотреть изменения в файловой системе
```shell
docker diff myapp-container
```

Создать новый образ из измененного контейнера
```shell
docker commit myapp-container myapp-modified
```

Сетевые возможности

Сетевые настройки

Список сетей
```shell
docker network ls
```

Информация о сети
```shell
docker network inspect bridge
```

Присоединить контейнер к другой сети
```shell
docker network create mynetwork
```
```shell
docker network connect mynetwork myapp-container
```


Пример 1: Полный цикл разработки

1. Останавливаем и удаляем старый контейнер
```shell
docker stop myapp-container
```
```shell
docker rm myapp-container
```

2. Пересобираем образ с новыми изменениями
```shell
docker build -t myapp:v2 .
```

3. Запускаем новый контейнер
```shell
docker run -d \
  --name myapp-v2 \
  -p 8000:8000 \
  -e FLASK_ENV=development \
  -v $(pwd):/home/appuser/app \
  myapp:v2
```

4. Смотрим логи
```shell
docker logs -f myapp-v2
```

Пример 2: Бэкап и восстановление

Бэкап данных
```shell
docker exec myapp-container tar -czf /tmp/backup.tar.gz /app/data
```
```shell
docker cp myapp-container:/tmp/backup.tar.gz ./backup.tar.gz
```

Создание снапшота контейнера
```shell
docker commit -p myapp-container myapp-backup
```
```shell
docker save -o myapp-backup.tar myapp-backup
```

Восстановление
```shell
docker load -i myapp-backup.tar
```
```shell
docker run -d --name restored-app -p 8001:8000 myapp-backup
```

Пример 3: Мониторинг

Создать скрипт мониторинга
```shell
cat > monitor.sh << 'EOF'
#!/bin/bash
while true; do
  clear
  echo "=== Docker Monitor ==="
  echo "Containers:"
  docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"
  echo -e "\nImages:"
  docker images --format "table {{.Repository}}\t{{.Tag}}\t{{.Size}}"
  echo -e "\nStats (last 5 sec):"
  docker stats --no-stream --format "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}"
  sleep 5
done
EOF
chmod +x monitor.sh
./monitor.sh
```

Docker Compose для удобства:

# docker-compose.yml
```yml
version: '3.8'
services:
  app:
    build: .
    image: myapp
    container_name: myapp-container
    ports:
      - "8000:8000"
    environment:
      - FLASK_ENV=production
      - PYTHONUNBUFFERED=1
    volumes:
      - ./logs:/app/logs
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
```

Использование docker-compose

Запуск в фоне
```shell
docker-compose up -d
```

Остановка и удаление
```shell
docker-compose down
```

Просмотр логов
```shell
docker-compose logs -f
```

Статус
```shell
docker-cmpose ps
```

Вход в контейнер
```shell
docker-compose exec app bash
```

Команды для очистки:

Очистка контейнеров

Удалить остановленные контейнеры
```shell
docker container prune
```

Удалить ВСЕ контейнеры
```shell
docker rm $(docker ps -aq)
```

Очистка образов

Удалить dangling образы
```shell
docker image prune
```

Удалить все неиспользуемые образы
```shell
docker image prune -a
```

Удалить ВСЕ образы
```shell
docker rmi $(docker images -q)
```

Полная очистка

ВСЁ: контейнеры, образы, тома, сети
```shell
docker system prune -a --volumes
```

Проверка дискового пространства
```shell
docker system df
```

Шпаргалка на каждый день:

# 🔄 Работа с контейнером
docker start/stop/restart <name>
docker logs -f <name>
docker exec -it <name> bash

# 📊 Мониторинг
docker ps
docker stats
docker system df

# 🛠️ Разработка
docker build -t <name> .
docker run -d -p <port> --name <name> <image>
docker-compose up --build

# 🧹 Очистка
docker container prune
docker image prune
=======
>>>>>>> 255df40356ef6007d18b0af44ceb711cfa050d01
