&#x20;Контракт API (API Contract)



Базовый путь: `/api/requests`



&#x20;Таблица эндпоинтов



| Метод и путь | Тело запроса (JSON) | Успех | Возможная ошибка |

|---|---|---|---|

| `GET /api/requests` | — | `200 OK`, массив объектов `\[]` | — |

| `GET /api/requests/{id}` | — | `200 OK`, объект заявки | `404 Not Found` |

| `POST /api/requests` | `title`, `carId`, `description` | `201 Created`, объект с `id`, `number`, `status: "New"` | `400 Bad Request` |

| `PATCH /api/requests/{id}/assignee` | `assigneeUserId` | `200 OK` | `404 Not Found` |

| `PATCH /api/requests/{id}/status` | `status` | `200 OK` | `404 Not Found`, `409 Conflict` |



\*Примечание: Клиент НЕ присылает `id`, `number`, `status` и `createdByUserId` при создании. Их генерирует и проставляет сервер.\*



&#x20;Примеры JSON



&#x20;1. Создание заявки (POST /api/requests)

\*\*Запрос:\*\*


{

&#x20; "title": "Поездка в аэропорт",

&#x20; "carId": 3,

&#x20; "description": "Забрать делегацию, 5 человек, багаж"

}

Ответ (201 Created):
{
  "id": 42,
  "number": "REQ-2026-042",
  "title": "Поездка в аэропорт",
  "description": "Забрать делегацию, 5 человек, багаж",
  "status": "New",
  "carId": 3,
  "createdByUserId": 10,
  "assigneeUserId": null
}

2. Назначение исполнителя (PATCH /api/requests/42/assignee)
Запрос:
{
  "assigneeUserId": 5
}
Ответ (200 OK): Успешно назначен.

3. Смена статуса (PATCH /api/requests/42/status)
Запрос:
{
  "status": "InProgress"
}
Ответ (200 OK): Статус изменен. (Допустимые значения: New, InProgress, Closed, Cancelled).

