# SmartDelivery 

![FastAPI](https://img.shields.io/badge/FastAPI-0.115-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-14-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-25-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-336791?style=for-the-badge&logo=postgresql&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-3.13-FF6600?style=for-the-badge&logo=rabbitmq&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-7-DC382D?style=for-the-badge&logo=redis&logoColor=white)
![gRPC](https://img.shields.io/badge/gRPC-1.68-244c5c?style=for-the-badge&logo=grpc&logoColor=white)

Система управления доставкой готовой еды из ресторанов.

---

## 📖 Описание

SmartDelivery — микросервисная платформа для автоматизации процессов приёма, обработки и исполнения заказов на доставку готовой еды из ресторанов. Система объединяет клиентов, операторов колл-центра, курьеров и бухгалтерию в единое информационное пространство.

### Ключевые возможности

- **Многоканальный приём заказов**: Telegram-бот для клиентов и веб-панель для операторов
- **Умная маршрутизация**: автоматическое построение маршрутов с Яндекс.Картами, поиск ближайших курьеров через Redis GEO
- **LLM-агент**: классификация заказов и автоматические ответы на типовые вопросы
- **Интеграция с 1С**: автоматическая выгрузка закрытых заказов
- **Real-time трекинг**: отслеживание курьеров на карте в реальном времени

---

## 🛠 Технологический стек

### Backend
- **Python 3.11+** — основной язык разработки
- **FastAPI** — асинхронный веб-фреймворк для всех микросервисов
- **SQLAlchemy 2.0 (async)** + **Alembic** — ORM и миграции
- **Pydantic** — валидация данных и сериализация

### Коммуникация
- **REST** — синхронное взаимодействие между сервисами
- **gRPC** — высокопроизводительная коммуникация для geo-service
- **RabbitMQ** — асинхронная шина событий

### Хранение
- **PostgreSQL 16** — основная база данных
- **SQLite** — база данных для локальной разработки
- **Redis** — кэширование, хранение координат (GEO), сессии

### Frontend
- **Next.js 14+ (TypeScript)** — панель оператора и интерфейс курьера

### Инфраструктура
- **Docker / docker-compose** — контейнеризация всех сервисов
- **GitHub** — контроль версий

### Внешние интеграции
- **Яндекс.Карты** — геокодирование и маршрутизация
- **Telegram Bot API** — клиентский канал
- **1С REST API** — выгрузка закрытых заказов
- **Ollama / OpenRouter** — LLM-агент

---

## 🏗 Архитектура

Микросервисная архитектура (MSA) с синхронной (REST, gRPC) и асинхронной (RabbitMQ) коммуникацией.

| Сервис | Назначение | Порт | Протокол |
|--------|------------|------|----------|
| `gateway` | API Gateway, единая точка входа | 8000 | REST |
| `order-service` | Управление заказами, статусная машина | 8001 | REST |
| `restaurant-service` | CRUD ресторанов и меню | 8002 | REST |
| `courier-service` | Управление курьерами, трекинг | 8003 | REST |
| `geo-service` | Геокодирование, маршруты, Redis GEO | 50051 | gRPC |
| `notification-service` | Отправка уведомлений | 8004 | REST |
| `integration-1c` | Выгрузка данных в 1С | 8005 | REST |
| `llm-agent` | Обработка сообщений через LLM | 8006 | REST |
| `bot` | Адаптер Telegram Bot | — | Telegram API |

---

## 🚀 Быстрый старт

### Предварительные требования

- Docker Desktop
- Git

### Запуск

```bash
# Клонирование репозитория
git clone https://github.com/bukabtw/smart-delivery.git
cd smart-delivery

# Запуск всей системы
docker-compose up -d

# Проверка статуса сервисов
```bash
docker-compose ps
```

### После запуска

Доступные сервисы:

| Ресурс | URL |
|--------|-----|
| API Gateway (Swagger) | http://localhost:8000/docs |
| Панель оператора | http://localhost:3000 |
| PostgreSQL | localhost:5432 |
| Redis | localhost:6379 |
| RabbitMQ Management | http://localhost:15672 |

## 📂 Структура проекта

```
smart-delivery/
├── gateway/              # API Gateway (FastAPI)
├── order-service/        # Управление заказами (FastAPI)
├── restaurant-service/   # Рестораны и меню (FastAPI)
├── courier-service/      # Курьеры и трекинг (FastAPI)
├── geo-service/          # Геокодирование и маршруты (FastAPI + gRPC)
├── notification-service/ # Уведомления (FastAPI)
├── integration-1c/       # Выгрузка в 1С (FastAPI)
├── llm-agent/            # LLM-агент (FastAPI)
├── bot/                  # Telegram Bot (aiogram)
├── frontend/             # Next.js панель оператора
├── docker-compose.yml
└── README.md
```

## 🤝 Команда

| Роль | Имя | GitHub |
|------|-----|--------|
| Product Owner, Архитектор | Владислав Бедин | @MindlessMuse666 |
| Developer | Кирилл Букарев | @bukabtw |

## 📄 Лицензия

MIT License · Copyright (c) 2026 SmartDelivery Team