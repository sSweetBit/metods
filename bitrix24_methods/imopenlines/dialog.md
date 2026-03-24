# Методы диалогов imopenlines

---

## imopenlines.dialog.get

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь с правом на доступ к диалогу  
**Параметры:** один из `CHAT_ID` / `DIALOG_ID` / `SESSION_ID` / `USER_CODE`

**Описание:**  
Возвращает данные чата открытой линии. Достаточно передать один из параметров.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `CHAT_ID` | integer | Идентификатор чата открытой линии |
| `DIALOG_ID` | string | Идентификатор диалога в формате `chat<ID>` |
| `SESSION_ID` | integer | Идентификатор сессии |
| `USER_CODE` | string | Строковый код пользователя. Формат: `<connector>|<LINE_ID>|<CONNECTOR_CHAT_ID>|<CONNECTOR_USER_ID>` |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"USER_CODE":"livechat|1|1373|211"}' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.dialog.get.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": {
        "id": 1777,
        "name": "Салатовый гость №17",
        "owner": 27,
        "color": "#58cc47",
        "type": "lines",
        "message_count": 104,
        "restrictions": {...},
        "entity_type": "LINES",
        "entity_id": "livechat|22|1775|599",
        "date_create": "2026-03-13T16:50:15+03:00",
        "role": "owner",
        "permissions": {...},
        "dialog_id": "chat1777"
    },
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | object | Объект данных чата |
| `time` | time | Информация о времени выполнения запроса |

**Основные поля `result`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `id` | integer | Идентификатор чата |
| `name` | string | Название чата |
| `owner` | integer | Идентификатор владельца |
| `color` | string | Цвет чата (HEX) |
| `type` | string | Тип чата (`lines` для открытых линий) |
| `message_count` | integer | Количество сообщений |
| `restrictions` | object | Права на действия с чатом |
| `entity_type` | string | Тип канала (`LINES`) |
| `entity_id` | string | Код пользователя открытой линии |
| `date_create` | datetime | Дата создания (ISO 8601) |
| `role` | string | Роль текущего пользователя |
| `permissions` | object | Права пользователя в чате |
| `dialog_id` | string | Идентификатор диалога |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 400 | `ACCESS_ERROR` | Диалог не найден или нет доступа к нему |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)
