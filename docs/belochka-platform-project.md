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
# 17. DEVICE STATE MODEL

DeviceState
-----------
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

# 18. DEVICE COMMAND MODEL

DeviceCommand
-------------
id
deviceId
commandType (feed, restart, update, test)
payload
status (pending, sent, executed, failed)
createdAt
executedAt


# 19. ALERT RULE MODEL

AlertRule
----------
id
deviceType
condition
threshold
severity
messageTemplate
enabled

# 21. MARKETING MODELS

Campaign
--------
id
franchiseId
name
campaignType
startDate
endDate
status

Offer
-----
id
campaignId
offerType
value
conditions

LoyaltyAccount
--------------
id
customerId
points
level

BonusTransaction
----------------
id
customerId
amount
type
timestamp


## 17. DEVICE STATE MODEL

DeviceState
-----------
deviceId: string  
onlineStatus: enum ['online', 'offline', 'needs_maintenance']  
lastSeenAt: datetime  
feedLevelPercent: float  
feedLevelGrams: float  
lastRefillAt: datetime  
lastOrderStatus: string  
errorStatus: string  
temperature: float  
voltage: float  
updatedAt: datetime  

Description:
- **deviceId**: Уникальный идентификатор устройства.
- **onlineStatus**: Статус подключения устройства (online, offline, needs_maintenance).
- **lastSeenAt**: Время последней активности устройства.
- **feedLevelPercent**: Процент оставшегося корма.
- **feedLevelGrams**: Количество оставшегося корма в граммах.
- **lastRefillAt**: Время последнего пополнения корма.
- **lastOrderStatus**: Статус последнего заказа (например, успешный или неудачный).
- **errorStatus**: Статус ошибок устройства.
- **temperature**: Температура устройства.
- **voltage**: Напряжение устройства.
- **updatedAt**: Время последнего обновления состояния устройства.

## 18. FEED LEVEL MODEL

FeedLevel
----------
deviceId: string  
currentFeedLevel: float  
maxFeedCapacity: float  
lastRefillTimestamp: datetime  
feedStatus: enum ['sufficient', 'needs_refill', 'critical']  

Description:
- **deviceId**: Уникальный идентификатор устройства.
- **currentFeedLevel**: Текущий уровень корма в устройстве (в килограммах или литрах).
- **maxFeedCapacity**: Максимальная ёмкость устройства.
- **lastRefillTimestamp**: Время последнего пополнения корма.
- **feedStatus**: Статус корма (sufficient, needs_refill, critical).

## 19. REFILL MODEL

Refill
------
refillId: string  
deviceId: string  
refillAmount: float  
refillTimestamp: datetime  

Description:
- **refillId**: Уникальный идентификатор пополнения.
- **deviceId**: Идентификатор устройства.
- **refillAmount**: Количество добавленного корма.
- **refillTimestamp**: Время пополнения.

## 20. ALERT MODEL

Alert
-----
alertId: string  
deviceId: string  
alertType: enum ['low_feed', 'device_error', 'maintenance_required']  
timestamp: datetime  
severity: enum ['low', 'medium', 'high']  
message: string  

Description:
- **alertId**: Идентификатор тревоги.
- **deviceId**: Идентификатор устройства.
- **alertType**: Тип тревоги (например, низкий уровень корма, ошибка устройства).
- **timestamp**: Время возникновения тревоги.
- **severity**: Степень серьёзности тревоги (low, medium, high).
- **message**: Сообщение тревоги.

## 21. OPERATIONS DASHBOARD

The Operations Dashboard is designed to provide administrators with a real-time overview of the following key data:

### 1. Devices:
- **Device Status**: Displays the current status of the devices, whether they are online, offline, or in need of maintenance.
- **Errors**: Displays the last error messages and their types.
- **Last Maintenance**: Shows the time of the last maintenance.

### 2. Feed Levels:
- Displays the current feed level in each device and the status (sufficient, needs refill, critical).

### 3. Feed Forecast:
- **Forecast of Feed Depletion**: Shows the predicted time when the feed in each device will run out, based on the current consumption rate.

### 4. Refill History:
- Displays the history of feed refills, showing when and how much feed was replenished.

### 5. Device Errors:
- Displays recent errors and provides detailed information about device malfunctions.
