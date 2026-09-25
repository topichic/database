# 🚀 DevOps Portfolio — CI/CD Pipeline Examples

Коллекция демонстрационных проектов с настроенными CI/CD пайплайнами на **GitHub Actions**

---

## 📋 Оглавление

- [Проекты](#-проекты)
- [Скриншоты пайплайнов](#-скриншоты-cicd-пайплайнов)
- [Что реализовано в каждом проекте](#-что-реализовано-в-каждом-проекте)
- [Быстрый старт](#-быстрый-старт)
- [Структура проекта](#-структура-проекта)
- [Используемые технологии](#-используемые-технологии)
- [Лицензия](#-лицензия)

---

## 📊 Проекты

| # | Язык/Стек | Репозиторий | CI/CD статус |
|---|-----------|-------------|---------------|
| 1 | <img src="https://img.icons8.com/color/48/000000/nodejs.png" width="20"/> **Node.js** | [my-node-app](https://github.com/topichic/my-node-app.git) | ✅ [![Node.js CI](https://github.com/topichic/my-node-app/actions/workflows/ci.yml/badge.svg)](https://github.com/topichic/my-node-app/actions/workflows/ci.yml) |
| 2 | <img src="https://img.icons8.com/color/48/000000/golang.png" width="20"/> **Go** | [my-go-app](https://github.com/topichic/my-go-app.git) | ✅ [![Go CI](https://github.com/topichic/my-go-app/actions/workflows/ci.yml/badge.svg)](https://github.com/topichic/my-go-app/actions/workflows/ci.yml) |
| 3 | <img src="https://img.icons8.com/color/48/000000/rust.png" width="20"/> **Rust + JS** | [my-rust-app](https://github.com/topichic/my-rust-app.git) | ✅ [![Rust CI](https://github.com/topichic/my-rust-app/actions/workflows/ci.yml/badge.svg)](https://github.com/topichic/my-rust-app/actions) |
| 4 | <img src="https://img.icons8.com/color/48/000000/php.png" width="20"/> **PHP** | [my-php-app](https://github.com/topichic/my-php-app.git) | ✅ [![PHP CI](https://github.com/topichic/my-php-app/actions/workflows/ci.yml/badge.svg)](https://github.com/topichic/my-php-app/actions/workflows/ci.yml) |
| 5 | <img src="https://img.icons8.com/color/48/000000/c-plus-plus-logo.png" width="20"/> **C++** | [my-cpp-app](https://github.com/topichic/my-cpp-app.git) | ✅ [![C++ CI](https://github.com/topichic/my-cpp-app/actions/workflows/ci.yml/badge.svg)](https://github.com/topichic/my-cpp-app/actions/workflows/ci.yml) |
| 6 | <img src="https://img.icons8.com/color/48/000000/java-coffee-cup-logo.png" width="20"/> **Java + Maven** | [my-java-app](https://github.com/topichic/my-java-app.git) | ✅ [![Java CI](https://github.com/topichic/my-java-app/actions/workflows/ci.yml/badge.svg)](https://github.com/topichic/my-java-app/actions/workflows/ci.yml) |

---

## 📸 Скриншоты CI/CD пайплайнов

| Приложение | Скриншоты |
|:-----------|:----------|
| **Node.js** | ![NodeJS1](/MyNotes/pipelines/img/nodejs.png)<br>![NodeJS2](/MyNotes/pipelines/img/nodejs2.png) |
| **Go** | ![go](/MyNotes/pipelines/img/go.png)<br>![go2](/MyNotes/pipelines/img/go2.png)<br>![go3](/MyNotes/pipelines/img/go3.png)<br>![go4](/MyNotes/pipelines/img/go4.png) |
| **Rust + JavaScript** | ![rust-js](/MyNotes/pipelines/img/rust-js.png)<br>![rust-js2](/MyNotes/pipelines/img/rust-js2.png)<br>![rust-js3](/MyNotes/pipelines/img/rust-js3.png) |
| **PHP** | ![php2](/MyNotes/pipelines/img/php2.png) |
| **C++** | ![my-cpp-app](/MyNotes/pipelines/img/my-cpp-app.png)<br>![my-cpp-app2](/MyNotes/pipelines/img/my-cpp-app2.png) |
| **Java + Maven** | ![java](/MyNotes/pipelines/img/java.png)<br>![java2](/MyNotes/pipelines/img/java2.png)<br>![java3](/MyNotes/pipelines/img/java3.png) |

---

## ⚙️ Что реализовано в каждом проекте

### ✅ Node.js

| Шаг пайплайна | Описание |
|---------------|----------|
| Установка зависимостей | `npm ci` — чистая установка из package-lock.json |
| Линтинг | ESLint проверка кода |
| Запуск тестов | Jest тесты с coverage |
| Сборка Docker образа | Многоступенчатая сборка |
| Публикация | Push в Docker registry (опционально) |

### ✅ Go

| Шаг пайплайна | Описание |
|---------------|----------|
| Кэширование модулей | Кэш для Go modules |
| Линтинг | golangci-lint — быстрый линтер |
| Запуск тестов | `go test -race -cover` с проверкой гонок |
| Сборка бинарника | Статическая сборка |
| Docker сборка | Многоступенчатая (builder + scratch/alpine) |

### ✅ Rust + JavaScript

| Шаг пайплайна | Описание |
|---------------|----------|
| Форматирование | `rustfmt` — проверка стиля |
| Линтинг | `clippy` — дополнительные предупреждения |
| Запуск тестов | `cargo test` — модульные и интеграционные |
| Сборка | `cargo build --release` |
| WASM (опционально) | Сборка в WebAssembly для браузера |

### ✅ PHP

| Шаг пайплайна | Описание |
|---------------|----------|
| Установка зависимостей | `composer install` |
| Линтинг | PHP_CodeSniffer (PSR-12 стандарт) |
| Запуск тестов | PHPUnit тесты |
| Docker сборка | Apache + PHP образ |

### ✅ C++

| Шаг пайплайна | Описание |
|---------------|----------|
| Установка компилятора | gcc / clang (на выбор) |
| CMake конфигурация | Генерация build системы |
| Сборка | `make` / `cmake --build` |
| Запуск тестов | CTest / GoogleTest |
| Valgrind (опционально) | Проверка утечек памяти |

### ✅ Java + Maven

| Шаг пайплайна | Описание |
|---------------|----------|
| Установка JDK | JDK 17 (Temurin) через `actions/setup-java@v4` |
| Кэширование Maven | Кэш `~/.m2/repository` для ускорения сборки |
| Сборка и тесты | `mvn clean verify` — компиляция + JUnit 5 тесты |
| Shade Plugin | Сборка «толстого» JAR с main-классом |
| Docker сборка | Многоступенчатая (Maven builder + JRE Alpine) |
| Запуск контейнера | `docker run --rm hello-java` |

---

## 🚀 Быстрый старт

### Клонирование репозитория

```bash
# Node.js
git clone https://github.com/topichic/my-node-app.git
cd my-node-app

# Go
git clone https://github.com/topichic/my-go-app.git
cd my-go-app

# Rust + JS
git clone https://github.com/topichic/my-rust-app.git
cd my-rust-app

# PHP
git clone https://github.com/topichic/my-php-app.git
cd my-php-app

# C++
git clone https://github.com/topichic/my-cpp-app.git
cd my-cpp-app

# Java + Maven
git clone https://github.com/topichic/my-java-app.git
cd my-java-app
