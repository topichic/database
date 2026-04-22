# ---- Этап 1: Сборка зависимостей и приложения ----
FROM rust:1-slim AS builder
WORKDIR /app
# Копируем только Cargo.toml (Cargo.lock не нужен на этом этапе)
COPY Cargo.toml .
# Создаём фиктивный src/main.rs, чтобы собрать зависимости
RUN mkdir src && echo "fn main() {}" > src/main.rs
# Собираем зависимости (при этом внутри контейнера создастся Cargo.lock)
RUN cargo build --release && rm -f target/release/rust-app*
# Теперь копируем настоящий исходный код
COPY src ./src
# Собираем окончательное приложение
RUN cargo build --release
# ---- Этап 2: Минимальный образ для запуска ----
FROM debian:stable-slim
# Создаём непривилегированного пользователя (рекомендация безопасности)
RUN useradd --create-home appuser
WORKDIR /home/appuser
# Копируем скомпилированный бинарник из этапа сборки
COPY --from=builder /app/target/release/rust-app ./rust-app
# Переключаемся на пользователя (не root)
USER appuser
# Если ваше приложение — веб-сервер, укажите порт
EXPOSE 8081
# Запуск в правильном JSON-формате (сигналы будут работать)
CMD ["./rust-app"]