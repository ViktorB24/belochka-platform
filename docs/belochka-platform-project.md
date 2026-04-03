Белочка парк — Platform Architecture

Версия: v0.1
Статус: Active
Архитектор: ARCHITECT Chat
Проект: Belochka Park Platform

1. PROJECT OVERVIEW
Описание проекта

Платформа «Белочка парк» — это франшизная система управления сетью:

кормушек для белок
арт-объектов с подсветкой
автоматов выдачи орехов
видеонаблюдения
образовательных проектов
мероприятий
интернет-магазина

Основной пользовательский сценарий:

QR → выбор корма → оплата → кормление → регистрация → повторные визиты

2. CORE BUSINESS MODEL
Основные продукты
Feeder (кормушка)
Art Object (белка)
Nut Machine (автомат орехов)
Events (мастер-классы)
Education (школа)
Streaming
Shop (будущий)
3. DOMAIN MODEL (MASTER)
Platform Structure

Platform
└── Franchise
└── City
└── Location
├── Device
│ ├── Feeder
│ ├── ArtObject
│ └── NutMachine
│
├── FeedInventory
├── Refill
│
├── Order
│ └── Payment
│
├── Subscription
│
├── Event
│
├── Telemetry
└── Alert

4. CUSTOMER DOMAIN (QR FLOW)
Основные сущности

Customer
CustomerSession
QRCode
QRScanEvent
FeedingSession

5. DEVICE DOMAIN

Device
Feeder
ArtObject
NutMachine

DeviceCommand

Telemetry
Alert

6. INVENTORY DOMAIN

FeedInventory
Refill
FeedConsumption

7. COMMERCE DOMAIN

Order
Payment
Subscription

8. MARKETING DOMAIN

Campaign
Offer
RegistrationStrategy

LoyaltyAccount
BonusTransaction

9. OPERATIONS DOMAIN

DeviceState
Alert
Monitoring

10. EVENTS DOMAIN

Event

(будущие)

Ticket
Attendance
Instructor

11. USERS DOMAIN

User
Role
Permission

12. BOUNDED CONTEXTS

Tenant Context
Location Context
Device Context
Inventory Context
Commerce Context
Customer Context
Marketing Context
Telemetry Context
Operations Context
Event Context
Subscription Context

13. ARCHITECTURE PRINCIPLES
API-first
Event-driven
Multi-tenant
Microservice-ready
Device-oriented
14. TECHNOLOGY STACK (PLANNED)

Backend:

NestJS
RabbitMQ
PostgreSQL
Redis

Frontend:

Next.js

Devices:

ESP32
MQTT

Streaming:

WebRTC / RTSP

15. ARCHITECTURE DECISIONS (ADR)
ADR-001

RabbitMQ выбран как брокер сообщений.

Причина:

простота внедрения
достаточная производительность
высокая совместимость

Статус: Approved

CHANGE LOG

v0.1 — Initial structure created

# 16. CORE USER FLOW

Основной пользовательский сценарий:

1 — Пользователь подходит к кормушке

2 — Сканирует QR-код

3 — Открывается страница устройства

4 — Выбирает корм

5 — Производит оплату

6 — Устройство выполняет команду кормления

7 — Пользователь наблюдает белок

8 — Система предлагает регистрацию

9 — Пользователь может получить бонусы

Основные сущности:

QRCode  
CustomerSession  
FeedingSession  
Order  
Payment  
DeviceCommand  

Это основной поток системы.
