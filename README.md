<div align="center">
    <img src="/docs/res/logo.png" alt="logo.png" width="200" height="200" />
    <h1>SmartDelivery 🍕</h1>
    <p><b><i>Веб-приложение системы управления доставкой еды (ﾉ◕ヮ◕)ﾉ*:･ﾟ✧</i></b></p>
    <br>
    <p align="center">
        <a href="https://fastapi.tiangolo.com/"><img src="https://img.shields.io/badge/FastAPI-0.115-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI"></a>
        <a href="https://go.dev/"><img src="https://img.shields.io/badge/Go-1.23-00ADD8?style=for-the-badge&logo=go&logoColor=white" alt="Go"></a>
        <a href="https://www.postgresql.org/"><img src="https://img.shields.io/badge/PostgreSQL-16-336791?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL"></a>
        <a href="https://vuejs.org/"><img src="https://img.shields.io/badge/Vue.js-3.4-4FC08D?style=for-the-badge&logo=vuedotjs&logoColor=white" alt="Vue.js"></a>
        <a href="https://vitejs.dev/"><img src="https://img.shields.io/badge/Vite-5.1-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite"></a>
        <a href="https://www.docker.com/"><img src="https://img.shields.io/badge/Docker-25-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker"></a>
        <a href="https://plantuml.com/"><img src="https://img.shields.io/badge/plantuml-4-FF6384?style=for-the-badge&logo=plantuml&logoColor=white" alt="PlantUML"></a>
        <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge" alt="MIT"></a>
    </p>
    <br>
</div>

## 📖 Описание

SmartDelivery - микросервисная платформа для автоматизации процессов приема, обработки и исполнения заказов на доставку еды из ресторанов. Система объединяет клиентов (через Telegram-бота) и операторов (через веб-панель).

### Ключевые возможности

- **Многоканальный прием заказов**: Telegram-бот для клиентов и веб-панель для операторов;
- **Синхронная архитектура**: все сервисы общаются через REST API;
- **Интеграция с 1С**: автовыгрузка закрытых заказов на учебный стенд 1С;
- **Статическая карта**: отображение меток ресторана и клиента на OpenStreetMap;
- **Локализация**: русский и английский языки в панели оператора.

## 🛠 Технологический стек

### Backend

- **Python 3.12+** (сервисы: ресторанов, уведомлений, интеграции 1С, Telegram-бот);
- **Go 1.25+** (API Gateway, сервис заказов);
- **FastAPI** - асинхронный веб-фреймворк для Python-сервисов;
- **SQLAlchemy 2.0 (async)** + **Alembic** - ORM и миграции;
- **Pydantic** - валидация данных и сериализация.

### Коммуникация

- **REST / HTTP** - протокол синхронного взаимодействия между сервисами.

### Хранение

- **PostgreSQL** - основная база данных (одна БД, разные схемы для сервисов).

### Frontend

- **Vue 3** + **Vuetify** - панель оператора;
- **Vite** - сборщик и dev-сервер;
- **Vue Router** - маршрутизация;
- **Vuex 4** - управление состоянием;
- **Vue i18n** - интернационализация (ru/en);
- **Axios** - HTTP-клиент для связи с API Gateway.

### Инфраструктура

- **Docker / docker-compose** - контейнеризация всех сервисов;
- **GitHub** - контроль версий.

### Внешние интеграции

- **Telegram Bot API** - клиентский канал;
- **Учебный стенд 1С** (HTTP-сервис) - выгрузка закрытых заказов;
- **OpenStreetMap (Leaflet.js)** - отображение статических карт.

## 🏗 Архитектура

Ознакомьтесь с актуальной диаграммой развертывания:

![Диаграмма развертывания](/docs/res/diagrams/диаграмма-развертывания/диаграмма_развертывания.png)

MSA с синхронной коммуникацией через REST.

| Сервис                 | Язык   | Назначение                            | Порт | Протокол     |
| ---------------------- | ------ | ------------------------------------- | ---- | ------------ |
| `gateway`              | Go     | API Gateway, единая точка входа       | 8000 | REST         |
| `order-service`        | Go     | Управление заказами, статусная машина | 8001 | REST         |
| `restaurant-service`   | Python | CRUD ресторанов и меню                | 8002 | REST         |
| `notification-service` | Python | Отправка уведомлений в Telegram       | 8003 | REST         |
| `integration-1c`       | Python | Выгрузка данных в учебный стенд 1С    | 8004 | REST         |
| `telegram-bot`         | Python | Обработка диалога с клиентами         | -    | Telegram API |
| `frontend`             | Vue    | Веб-панель оператора (SPA)            | 8080 | -            |

## 🚀 Быстрый старт

### Предварительные требования

- Docker Desktop
- Git

### Запуск

```bash
# клонируйте репо
git clone https://github.com/KontsertKishlaka/smart-delivery.git
cd smart-delivery

# запустите систему
docker-compose up -d

# проверьте статусы сервисов (опционально)
docker-compose ps
```

### После запуска

| Ресурс                                    | URL                          |
| ----------------------------------------- | ---------------------------- |
| API Gateway (Swagger для Python-сервисов) | <http://localhost:8000/docs> |
| Панель оператора (Vue)                    | <http://localhost:8080>      |
| PostgreSQL                                | <http://localhost:5432>      |

## 📂 Структура проекта

```text
smart-delivery/
├── gateway/                # API Gateway (Go)
├── order-service/          # Сервис заказов (Go)
├── restaurant-service/     # Сервис ресторанов (FastAPI)
├── notification-service/   # Сервис уведомлений (FastAPI)
├── integration-1c/         # Интеграция с 1С (FastAPI)
├── telegram-bot/           # Telegram-бот (aiogram)
├── frontend/               # Панель оператора (Vue + Vite)
├── docker-compose.yml
└── README.md
```

## 🤝 Команда

| Роль                       | Имя                                                   |
| -------------------------- | ----------------------------------------------------- |
| Владелец продукта, Тим-лид | [Владислав Бедин](https://github.com/MindlessMuse666) |
| Ведущий разработчик        | [Кирилл Букарев](https://github.com/bukabtw)          |

---

<div align="center">
  <img src="/docs/res/logo.png" alt="logo.png" width="100" height="100" />
  <br>
  <sub><b>Веб-приложение // SmartDelivery</b></sub>
  <br>
  <sup><i>Made with love by <a href="https://github.com/cranchy-team" target="_blank">MindlessMuse666 x bukabtw</a></i></sup>
</div>
