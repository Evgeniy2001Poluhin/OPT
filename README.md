🔐 OTP Protection Service

Java backend-сервис для генерации, рассылки и проверки одноразовых паролей (OTP). Поддерживает Email, SMS (SMPP-эмулятор), Telegram и сохранение в файл.

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

Токенная авторизация: Bearer-токены

Логирование: SLF4J + Logback

🚀 Технологии

Компонент

Версия / Библиотека

Java

17

PostgreSQL (JDBC)

17

Maven

3.x

HTTP Server

com.sun.net.httpserver

Email

JavaMail

SMS

OpenSMPP-core + SMPPsim

Telegram API

Apache HttpClient

Логирование

SLF4J + Logback

🛠 Установка и запуск

Клонировать:

git clone https://github.com/Evgeniy2001Poluhin/OPT.git
cd OPT

Настроить:

Java 17 и PostgreSQL 17

Создать БД:

CREATE DATABASE otp_service;

Заполнить src/main/resources:

application.properties (БД)

email.properties (SMTP)

sms.properties (SMPP)

telegram.properties (токен и chatId)

Сборка и запуск:

mvn clean package
java -jar target/otp-backend.jar

Сервис на http://localhost:8080.

🔧 Конфигурация

# src/main/resources/application.properties

db.url=jdbc:postgresql://localhost:5432/otp_service
 db.user=postgres
 db.password=<ваш_пароль>

Аналогично для email.properties, sms.properties, telegram.properties.

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

🗂 Структура проекта

OPT/
├── src/main/java/otp/
│   ├── api/        # HTTP-контроллеры
│   ├── config/     # Конфигурации
│   ├── dao/        # JDBC-доступ к БД
│   ├── model/      # DTO и сущности
│   ├── service/    # Бизнес-логика
│   └── util/       # Утилиты
└── src/main/resources/
    ├── application.properties
    ├── email.properties
    ├── sms.properties
    ├── telegram.properties
    └── logback.xml

pom.xml
README.md

📖 Примеры API

Admin: настройка OTP

curl -X PATCH http://localhost:8080/admin/config \
  -H "Authorization: Bearer <ADMIN_TOKEN>" \
  -H "Content-Type: application/json" \
  -d '{"length":6,"ttlSeconds":300}'

Admin: управление пользователями

# Просмотр
curl -X GET http://localhost:8080/admin/users \
  -H "Authorization: Bearer <ADMIN_TOKEN>"
# Удаление
curl -X DELETE http://localhost:8080/admin/users/{id} \
  -H "Authorization: Bearer <ADMIN_TOKEN>"

🧪 Тестирование

Используйте Postman или curl для всех сценариев:

Регистрация / Логин

Генерация / Отправка OTP

Валидация кодов

Админ-функции

👤 Автор

<<<<<<< HEAD
Евгений ПолухинGitHub: Evgeniy2001PoluhinTelegram: @EvgeniyPoluhin
=======
Евгений ПолухинGitHub: Evgeniy2001PoluhinTelegram: @EvgeniyPoluhin
>>>>>>> f1bc3555d20cfc78a96166f767c2aa30e411bc67
