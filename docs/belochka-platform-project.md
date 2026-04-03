Белочка парк — Platform Architecture
Версия: v0.1
Статус: Active
Архитектор: ARCHITECT Chat
Проект: Belochka Park Platform
PROJECT OVERVIEW
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
CORE BUSINESS MODEL
Основные продукты
Feeder (кормушка)
Art Object (белка)
Nut Machine (автомат орехов)
Events (мастер-классы)
Education (школа)
Streaming
Shop (будущий)
DOMAIN MODEL (MASTER)
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
CUSTOMER DOMAIN (QR FLOW)
Основные сущности
Customer
CustomerSession
QRCode
QRScanEvent
FeedingSession
DEVICE DOMAIN
Device
Feeder
ArtObject
NutMachine
DeviceCommand
Telemetry
Alert
INVENTORY DOMAIN
FeedInventory
Refill
FeedConsumption
COMMERCE DOMAIN
Order
Payment
Subscription
MARKETING DOMAIN
Campaign
Offer
RegistrationStrategy
LoyaltyAccount
BonusTransaction
OPERATIONS DOMAIN
DeviceState
Alert
Monitoring
EVENTS DOMAIN
Event
(будущие)
Ticket
Attendance
Instructor
USERS DOMAIN
User
Role
Permission
BOUNDED CONTEXTS
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
ARCHITECTURE PRINCIPLES
API-first
Event-driven
Multi-tenant
Microservice-ready
Device-oriented
TECHNOLOGY STACK (PLANNED)
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
ARCHITECTURE DECISIONS (ADR)
ADR-001
RabbitMQ выбран как брокер сообщений.
Причина:
простота внедрения
достаточная производительность
высокая совместимость
Статус: Approved
CHANGE LOG
v0.1 — Initial structure created
16. CORE USER FLOW
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
17. DEVICE STATE MODEL
DeviceState
deviceId
onlineStatus (online, offline)
lastSeenAt
feedLevelPercent
feedLevelGrams
lastRefillAt
lastOrderStatus
errorStatus
temperature
voltage
updatedAt
18. DEVICE COMMAND MODEL
DeviceCommand
id
deviceId
commandType (feed, restart, update, test)
payload
status (pending, sent, executed, failed)
createdAt
executedAt
19. ALERT RULE MODEL
AlertRule
id
deviceType
condition
threshold
severity
messageTemplate
enabled
19. ALERT RULE MODEL
AlertRule
id
deviceType
condition
threshold
severity
messageTemplate
enabled
21. MARKETING MODELS
Campaign
id
franchiseId
name
campaignType
startDate
endDate
status
Offer
id
campaignId
offerType
value
conditions
LoyaltyAccount
id
customerId
points
level
BonusTransaction
id
customerId
amount
type
timestamp
