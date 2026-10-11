# Матрица требований

| Требование | Поле или сущность | Запрос | Критерий |
|-|-|-|-|
| Создать бронь | Booking, title, resourceId, description | POST /api/bookings | 1 |
| Назначить исполнителя | assigneeUserId | PATCH /api/bookings/{id}/assignee | 2 |
| Перевести в работу | status = InProgress | PATCH /api/bookings/{id}/status | 3 |