🔐 OTP Protection Service

Java backend-сервис для генерации, рассылки и проверки одноразовых паролей (OTP). Поддерживает отправку через Email, SMS (SMPP-эмулятор), Telegram и сохраняет коды в файл для отладки.

📋 Содержание

✨ Функционал

🚀 Технологии

🛠 Установка и запуск

🔧 Конфигурация

⚡ Использование

🗂 Структура проекта

📖 Примеры API

🧪 Тестирование

👤 Автор

📄 Лицензия

✨ Функционал

Роли и доступ: ADMIN и USER

Отправка OTP:

Email (JavaMail)

SMS (OpenSMPP-core + SMPPsim)

Telegram Bot API

Сохранение в локальный файл

Проверка OTP: статусы ACTIVE, USED, EXPIRED

Админ-панель:

Настройка длины кода и TTL

Управление пользователями

Токенная авторизация (Bearer-токены)

Логирование запросов и операций (SLF4J + Logback)

🚀 Технологии

Компонент

Версия / Библиотека

Java

17

СУБД

PostgreSQL 17 (JDBC)

Сборка

Maven

HTTP-сервер

com.sun.net.httpserver

Email

JavaMail

SMS

OpenSMPP-core + SMPPsim

Telegram Bot API

Apache HttpClient

Логирование

SLF4J + Logback

🛠 Установка и запуск

Клонировать репозиторий:

git clone https://github.com/Evgeniy2001Poluhin/OPT.git
cd OPT

Настроить окружение:

Установить Java 17 и PostgreSQL 17

Создать БД:

CREATE DATABASE otp_service;

Скопировать и заполнить в src/main/resources:

application.properties (параметры БД)

email.properties (SMTP)

sms.properties (SMPP)

telegram.properties (токен и chatId)

Собрать и запустить:

mvn clean package
java -jar target/otp-backend.jar

По умолчанию сервис доступен на http://localhost:8080.

🔧 Конфигурация

Пример application.properties:

db.url=jdbc:postgresql://localhost:5432/otp_service
db.user=postgres
db.password=<ваш_пароль>

Файлы email.properties, sms.properties и telegram.properties содержат аналогичные параметры для своих сервисов.

⚡ Использование

Регистрация:

curl -X POST http://localhost:8080/register \
  -H "Content-Type: application/json" \
  -d '{"username":"user1","password":"pass123","role":"USER"}'

Логин:

curl -X POST http://localhost:8080/login \
  -H "Content-Type: application/json" \
  -d '{"username":"user1","password":"pass123"}'

Генерация OTP:

curl -X POST http://localhost:8080/otp/generate \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"operationId":"op123","channel":"EMAIL"}'

Проверка OTP:

curl -X POST http://localhost:8080/otp/validate \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"code":"123456"}'

📖 Примеры API

Admin: настройка параметров OTP

curl -X PATCH http://localhost:8080/admin/config \
  -H "Authorization: Bearer <ADMIN_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{"length":6,"ttlSeconds":300}'

Admin: управление пользователями

# Просмотр всех
curl -X GET http://localhost:8080/admin/users \
  -H "Authorization: Bearer <ADMIN_TOKEN>"
# Удаление
curl -X DELETE http://localhost:8080/admin/users/{id} \
  -H "Authorization: Bearer <ADMIN_TOKEN>"

🧪 Тестирование

Используйте Postman или curl для проверки всех сценариев:

Регистрация / Логин

Генерация / Отправка OTP

Валидация кодов

Админ-функции

👤 Автор

Евгений ПолухинGitHub: Evgeniy2001PoluhinTelegram: @EvgeniyPoluhin
