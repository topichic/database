# ---- Базовый образ ----
FROM ruby:3.3-slim
# Устанавливаем необходимые системные пакеты для компиляции нативных гемов
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*
# ---- Установка рабочей директории ----
WORKDIR /app
# ---- Копирование файла с зависимостями и их установка ----
# Копируем только Gemfile (не Gemfile.lock, если его нет)
COPY Gemfile ./
# Устанавливаем зависимости (гемы)
RUN bundle install
# ---- Копирование остального кода приложения ----
COPY . .
# ---- Запуск приложения ----
CMD ["ruby", "app.rb"]