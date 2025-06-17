🔐 OTP Protection Service

Backend‑сервис на Java для генерации, рассылки и проверки одноразовых паролей (OTP) с поддержкой отправки через Email, SMS (SMPP эмулятор), Telegram и сохранением в файл. Используется для защиты критичных операций пользователей.

📋 Основные возможности

Пользователи и роли: ADMIN и USER с разграничением доступа

Отправка OTP:

Email (JavaMail)

SMS (эмулятор SMPP)

Telegram Bot API

Локальное сохранение в файл для отладки

Проверка OTP с учётом статусов: ACTIVE, USED, EXPIRED

Админ-панель:

Настройка длины кода и TTL

Управление списком пользователей

Токенная авторизация (Bearer-токены с ролями)

Логирование всех запросов и ключевых операций через SLF4J/Logback

⚙️ Стек технологий

Java 17

PostgreSQL 17 + JDBC (без ORM)

Maven для сборки

com.sun.net.httpserver (HTTPServer)

JavaMail (отправка Email)

OpenSMPP-core с SMPPsim (эмулятор SMS)

Apache HttpClient (Telegram Bot API)

SLF4J + Logback для логирования

🚀 Установка и запуск

. Клонирование репозитория

git clone https://github.com/Evgeniy2001Poluhin/OPT.git
cd OPT

2. Настройка окружения

Установите Java 17 и PostgreSQL 17

Создайте базу данных otp_service:

CREATE DATABASE otp_service;

Скопируйте и заполните в src/main/resources:

application.properties (параметры БД)

email.properties (SMTP сервер)

sms.properties (SMPP эмулятор)

telegram.properties (токен и chatId)

Пример application.properties:

db.url=jdbc:postgresql://localhost:5432/otp_service
db.user=postgres
db.password=ваш_пароль

3. Сборка и запуск

mvn clean package
java -jar target/otp-backend.jar

После старта сервис будет слушать на порту 8080.

🔑 Роли и авторизация

ADMIN:

Полный контроль: настройка OTP, управление пользователями

USER:

Генерация и проверка своих OTP

Токены передаются в заголовке:

Authorization: Bearer <token>

📖 Примеры API-запросов

Регистрация

curl -X POST http://localhost:8080/register \
  -H "Content-Type: application/json" \
  -d '{"username":"user1","password":"pass123","role":"USER"}'

Вход (получение токена)

curl -X POST http://localhost:8080/login \
  -H "Content-Type: application/json" \
  -d '{"username":"user1","password":"pass123"}'

Генерация OTP

curl -X POST http://localhost:8080/otp/generate \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"operationId":"op123","channel":"EMAIL"}'

Проверка OTP

curl -X POST http://localhost:8080/otp/validate \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"code":"123456"}'

Admin: управление конфигом

curl -X PATCH http://localhost:8080/admin/config \
  -H "Authorization: Bearer $ADMIN_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"length":6,"ttlSeconds":300}'

🧪 Тестирование

Проверяйте API через Postman или curl:

Регистрация и логин

Генерация/отправка OTP

Валидация кода

Админ-функции
