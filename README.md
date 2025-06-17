<!-- README.md for OTP Protection Service -->

<p align="center">
  <img src="https://raw.githubusercontent.com/Evgeniy2001Poluhin/OPT/main/assets/otp-banner.png" alt="OTP Protection Service" width="600" />
</p>

<p align="center">
  <a href="https://github.com/Evgeniy2001Poluhin/OPT/actions"><img src="https://img.shields.io/github/actions/workflow/status/Evgeniy2001Poluhin/OPT/ci.yml?branch=main" alt="Build Status"></a>
  <a href="https://img.shields.io/badge/Java-17-blue"><img src="https://img.shields.io/badge/Java-17-blue" alt="Java 17"></a>
  <a href="https://img.shields.io/badge/Maven-3.x-green"><img src="https://img.shields.io/badge/Maven-3.x-green" alt="Maven"></a>
  <a href="https://img.shields.io/badge/PostgreSQL-17-blue"><img src="https://img.shields.io/badge/PostgreSQL-17-blue" alt="PostgreSQL 17"></a>
  <a href="https://img.shields.io/badge/License-MIT-yellow.svg"><img src="https://img.shields.io/badge/License-MIT-yellow.svg" alt="MIT License"></a>
</p>

# 🔐 OTP Protection Service

Java backend-сервис для генерации, рассылки и проверки одноразовых паролей (OTP). Поддерживает Email, SMS (SMPP-эмулятор), Telegram и локальное сохранение кодов.

---

## 📋 Содержание

* [✨ Функционал](#✨-функционал)
* [🚀 Технологии](#🚀-технологии)
* [🛠 Установка и запуск](#🛠-установка-и-запуск)
* [🔧 Конфигурация](#🔧-конфигурация)
* [⚡ Использование](#⚡-использование)
* [🗂 Структура проекта](#🗂-структура-проекта)
* [📖 Примеры API](#📖-примеры-api)
* [🧪 Тестирование](#🧪-тестирование)
* [👤 Автор](#👤-автор)
* [📄 Лицензия](#📄-лицензия)

---

## ✨ Функционал

* **Роли**: ADMIN и USER с разграничением доступа
* **Генерация и отправка OTP** через:

  * Email (JavaMail)
  * SMS (OpenSMPP-core + SMPPsim)
  * Telegram Bot API
  * Локальное сохранение в файл для отладки
* **Проверка OTP** с учётом статусов: `ACTIVE`, `USED`, `EXPIRED`
* **Админ-панель**:

  * Настройка длины кода и времени жизни (TTL)
  * Управление пользователями и ролями
* **Токенная авторизация**: Bearer-токены с проверкой ролей
* **Логирование** всех операций (SLF4J + Logback)

---

## 🚀 Технологии

* **Java 17**
* **PostgreSQL 17** (JDBC)
* **Maven** (сборка)
* **HTTP-сервер**: com.sun.net.httpserver
* **Email**: JavaMail
* **SMS**: OpenSMPP-core + SMPPsim
* **Telegram Bot API**: Apache HttpClient
* **Логирование**: SLF4J + Logback

---

## 🛠 Установка и запуск

1. Клонировать репозиторий:

   ```bash
   git clone https://github.com/Evgeniy2001Poluhin/OPT.git
   cd OPT
   ```
2. Установить Java 17 и PostgreSQL 17
3. Создать базу данных:

   ```sql
   CREATE DATABASE otp_service;
   ```
4. Скопировать и настроить файлы в `src/main/resources`:

   * `application.properties` (настройки БД)
   * `email.properties` (SMTP)
   * `sms.properties` (SMPP)
   * `telegram.properties` (токен и chatId)
5. Собрать и запустить:

   ```bash
   mvn clean package
   java -jar target/otp-backend.jar
   ```

Сервис запустится на `http://localhost:8080`.

---

## 🔧 Конфигурация

Файл `src/main/resources/application.properties`:

```properties
# Параметры PostgreSQL
 db.url=jdbc:postgresql://localhost:5432/otp_service
 db.user=postgres
 db.password=<ваш_пароль>
```

Аналогично заполнить `email.properties`, `sms.properties`, `telegram.properties`.

---

## ⚡ Использование

1. **Регистрация**:

```bash
curl -X POST http://localhost:8080/register \
-H "Content-Type: application/json" \
-d '{"username":"user1","password":"pass123","role":"USER"}'
```

2. **Логин**:

```bash
curl -X POST http://localhost:8080/login \
-H "Content-Type: application/json" \
-d '{"username":"user1","password":"pass123"}'
```

3. **Генерация OTP**:

```bash
curl -X POST http://localhost:8080/otp/generate \
-H "Authorization: Bearer $TOKEN" \
-H "Content-Type: application/json" \
-d '{"operationId":"op123","channel":"EMAIL"}'
```

4. **Проверка OTP**:

```bash
curl -X POST http://localhost:8080/otp/validate \
-H "Authorization: Bearer $TOKEN" \
-H "Content-Type: application/json" \
-d '{"code":"123456"}'
```


---

## 📖 Примеры API

**Админ: изменить параметры OTP**

```bash
curl -X PATCH http://localhost:8080/admin/config \
-H "Authorization: Bearer <ADMIN_TOKEN>" \
-H "Content-Type: application/json" \
-d '{"length":6,"ttlSeconds":300}'
```

**Админ: управление пользователями**

```bash
curl -X GET http://localhost:8080/admin/users \
-H "Authorization: Bearer <ADMIN_TOKEN>"
```

```bash
curl -X DELETE http://localhost:8080/admin/users/{id} \
-H "Authorization: Bearer <ADMIN_TOKEN>"
```

---

## 🧪 Тестирование

Проверить через **Postman** или **curl**:

* Регистрация и логин
* Генерация и отправка OTP
* Проверка кодов
* Админ-функции

---

## 👤 Автор

**Евгений Полухин**
GitHub: [https://github.com/Evgeniy2001Poluhin](https://github.com/Evgeniy2001Poluhin)
Telegram: [https://t.me/EvgeniyPoluhin](https://t.me/EvgeniyPoluhin)

---


