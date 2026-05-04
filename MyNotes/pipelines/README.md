# 🚀 DevOps Portfolio — CI/CD Pipeline Examples

Коллекция демонстрационных проектов с настроенными CI/CD пайплайнами на **GitHub Actions**

---

## 📋 Оглавление

- [Проекты](#-проекты)
- [Скриншоты пайплайнов](#-скриншоты-cicd-пайплайнов)
- [Что реализовано в каждом проекте](#что-реализовано-в-каждом-проекте)
- [Быстрый старт](#-быстрый-старт)

---

## 📊 Проекты

| # | Язык/Стек | Репозиторий | CI/CD статус |
|:--:|:----------|:------------|:--------------|
| 1 | <img src="https://img.icons8.com/color/48/000000/nodejs.png" width="20"/> **Node.js** | [my-node-app](https://github.com/topichic/my-node-app.git) | [✅ CI for Node.js App passing](https://github.com/topichic/my-node-app/actions/workflows/ci.yml) |
| 2 | <img src="https://img.icons8.com/color/48/000000/golang.png" width="20"/> **Go** | [my-go-app](https://github.com/topichic/my-go-app.git) | [✅ CI for Go App passing](https://github.com/topichic/my-go-app/actions/workflows/ci.yml) |
| 3 | <img src="https://img.icons8.com/color/48/000000/rust.png" width="20"/> **Rust + JS** | [my-rust-app](https://github.com/topichic/my-rust-app.git) | [✅ Rust CI](https://github.com/topichic/my-rust-app/actions/workflows/ci.yml) |
| 4 | <img src="https://img.icons8.com/color/48/000000/php.png" width="20"/> **PHP** | [my-php-app](https://github.com/topichic/my-php-app.git) | [✅ PHP CI Pipeline passing](https://github.com/topichic/my-php-app/actions/workflows/ci.yml) |
| 5 | <img src="https://img.icons8.com/color/48/000000/c-plus-plus-logo.png" width="20"/> **C++** | [my-cpp-app](https://github.com/topichic/my-cpp-app.git) | [✅ C++ CI Pipeline passing](https://github.com/topichic/my-cpp-app/actions/workflows/ci.yml) |

---

## 📸 Скриншоты CI/CD пайплайнов

## Node.js

![NodeJS1](/MyNotes/pipelines/img/nodejs.png)
![NodeJS2](/MyNotes/pipelines/img/nodejs2.png)

---

## Go

![go3](/MyNotes/pipelines/img/go3.png)
![go](/MyNotes/pipelines/img/go.png)
![go2](/MyNotes/pipelines/img/go2.png)
![go4](/MyNotes/pipelines/img/go4.png)

---

## Rust + JavaScript

![rust-js2](/MyNotes/pipelines/img/rust-js2.png)
![rust-js](/MyNotes/pipelines/img/rust-js.png)
![rust-js3](/MyNotes/pipelines/img/rust-js3.png)

---

## PHP

![php2](/MyNotes/pipelines/img/php2.png)
![php](/MyNotes/pipelines/img/php.png)

---

## C++

![my-cpp-app](/MyNotes/pipelines/img/my-cpp-app.png)
![my-cpp-app2](/MyNotes/pipelines/img/my-cpp-app2.png)

---

## Что реализовано в каждом проекте

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

---

## 🚀 Быстрый старт

### Клонирование репозитория

```bash
git clone https://github.com/topichic/my-node-app.git
cd my-node-app
```
---
## Локальная сборка Docker образа


### Node.js
```shell
docker build -t my-node-app:latest .
```
Создание и запуск контейнера:
```shell
docker run --rm my-node-app:latest
```

### Go
```shell
docker build -t my-go-app:latest .
```
Создание и запуск контейнера:
```shell
docker run --rm my-go-app:latest
```

### Rust
```shell
docker build -t my-rust-app:latest .
```
Запуск контейнера:
```shell
docker run --rm my-rust-app:latest
```

### PHP
```shell
docker build -t my-php-app:latest .
```
Запустить контейнер
```shell
docker run --rm my-php-app:latest
```

### C++

```shell
docker build -t my-cpp-app:latest .
```
Запустить контейнер
```shell
docker run --rm my-cpp-app:latest
```
