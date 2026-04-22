# ---- Этап 1: Сборка и компиляция TypeScript ----
FROM node:20-alpine AS builder
WORKDIR /app
# Копируем файлы с зависимостями
COPY package*.json tsconfig.json ./
# Устанавливаем ВСЕ зависимости (включая TypeScript и dev-зависимости)
# Используем npm install, так как package-lock.json может отсутствовать
RUN npm install
# Копируем исходный код
COPY src ./src
# Компилируем TypeScript в JavaScript
RUN npm run build
# ---- Этап 2: Финальный образ для запуска ----
FROM node:20-alpine AS runner
WORKDIR /app
# Копируем только готовый JavaScript-код и production-зависимости
# (dev-зависимости, включая TypeScript, уже не нужны)
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./
# Устанавливаем только production-зависимости (без dev)
RUN npm install --omit=dev
# Создаём непривилегированного пользователя для безопасности
USER node
# Указываем порт (если ваше приложение — веб-сервер)
EXPOSE 3000
# Запускаем скомпилированное приложение
CMD ["node", "dist/index.js"]