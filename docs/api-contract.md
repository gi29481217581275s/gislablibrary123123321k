# API-контракт

Базовый путь: `/api/bookings`. Все ответы - JSON. Метод DELETE не используется:
отмена брони - это `PATCH .../status` со значением `Cancelled`.

## Таблица

| Метод и путь | Тело запроса | Успех | Ошибка |
|-|-|-|-|
| GET /api/bookings | - | 200, массив (возможно `[]`) | - |
| GET /api/bookings/{id} | - | 200, объект | 404 |
| POST /api/bookings | title, resourceId, description | 201, id, number, status: New | 400 |
| PATCH /api/bookings/{id}/assignee | assigneeUserId | 200 | 404 |
| PATCH /api/bookings/{id}/status | status | 200 | 404, 409 |

Клиент **не присылает** при создании `id`, `number`, `status`, `assigneeUserId`.
Их определяет сервер.

Статусы: только `New`, `InProgress`, `Closed`, `Cancelled`.

## Примеры JSON

### POST /api/bookings - запрос
```json
{
  "title": "Бронь на среду",
  "resourceId": 12,
  "description": "Нужна книга по алгоритмам на один день"
}
```

### 201 Created - ответ
```json
{
  "id": 101,
  "number": "BR-0001",
  "title": "Бронь на среду",
  "description": "Нужна книга по алгоритмам на один день",
  "status": "New",
  "resourceId": 12,
  "createdByUserId": 5,
  "assigneeUserId": null
}
```

### PATCH /api/bookings/{id}/assignee - запрос
```json
{ "assigneeUserId": 7 }
```

### PATCH /api/bookings/{id}/status - запрос
```json
{ "status": "InProgress" }
```

### Ошибки
```json
{ "error": "Not found" }
```
```json
{ "error": "Invalid status transition" }
```