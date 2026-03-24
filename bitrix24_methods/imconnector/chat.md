# Методы управления чатами imconnector

---

## imconnector.chat.name.set

**Scope:** `imconnector`  
**Кто может выполнять:** любой пользователь  
**Параметры:** `CONNECTOR`, `LINE`, `CHAT_ID`, `NAME` (все обязательные), `USER_ID` (опциональный)

**Описание:**  
Устанавливает новое имя для чата.

> **Важно:** Метод работает только в контексте приложения (требуется OAuth авторизация).

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `CONNECTOR` | string | Строковый код коннектора (задается при регистрации через `imconnector.register`) |
| `LINE` | integer | Идентификатор открытой линии (можно получить через `imopenlines.config.get` или `imopenlines.config.list.get`) |
| `CHAT_ID` | string | Идентификатор чата во внешней системе |
| `NAME` | string | Новое имя для чата |
| `USER_ID` | string | Идентификатор пользователя. Обязателен только для коннекторов без групповых чатов (при `CHAT_GROUP=N` в `imconnector.register`) |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{
    "CONNECTOR": "connector",
    "LINE": 105,
    "CHAT_ID": "47e007b1-ee15-43db-bcba-1c26e5884d3f",
    "NAME": "New Dialog Name"
  }' \
  https://your-domain.bitrix24.ru/rest/imconnector.chat.name.set?auth=**put_access_token_here**
```

**Пример ответа (HTTP 200):**
```json
{
    "answer": {
        "result": {
            "SUCCESS": true,
            "DATA": {
                "RESULT": {}
            }
        },
        "time": {
            "start": 1732110908.525962,
            "finish": 1732110908.879113,
            "duration": 0.3531508445739746,
            "processing": 0.07694888114929199,
            "date_start": "2024-11-20T15:55:08+02:00",
            "date_finish": "2024-11-20T15:55:08+02:00"
        }
    }
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `SUCCESS` | boolean | `true`, если имя чата успешно установлено |
| `DATA` | object | Содержит объект `RESULT` с параметрами нового имени чата |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 400 | `NOT_ACTIVE_LINE` | Линия с таким ID неактивна или не существует |
| 400 | `IMCONNECTOR_NO_CORRECT_PROVIDER` | Не удалось найти подходящий провайдер для коннектора |
| 400 | `ERROR_ARGUMENT` | Отсутствуют обязательные параметры `NAME`, `CHAT_ID`, `USER_ID`, `CONNECTOR` или `LINE` |
| 400 | `CHAT_RENAMING_FAILED` | Не удалось переименовать чат |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)
