# Регистрация коннектора imconnector

---

## imconnector.register

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь  
**Параметры:** `ID`, `NAME`, `ICON`, `PLACEMENT_HANDLER` (все обязательные)

**Описание:**  
Регистрирует пользовательский коннектор для открытых линий.

> **Важно:** Метод работает только в контексте приложения (требуется OAuth авторизация).

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `ID` | string | Уникальный идентификатор коннектора (приводится к нижнему регистру). Используйте цифры, буквы в нижнем регистре и `_`. Символ `.` запрещен |
| `NAME` | string | Название коннектора в интерфейсе |
| `ICON` | object | Параметры основной иконки |
| `PLACEMENT_HANDLER` | string | URL обработчика встраивания для настроек коннектора |
| `ICON_DISABLED` | object | Параметры иконки неактивного состояния |
| `DEL_EXTERNAL_MESSAGES` | boolean | Разрешить удалять входящие сообщения (по умолчанию `true`) |
| `EDIT_INTERNAL_MESSAGES` | boolean | Разрешить редактировать сообщения операторов (по умолчанию `true`) |
| `DEL_INTERNAL_MESSAGES` | boolean | Разрешить удалять сообщения операторов (по умолчанию `true`) |
| `NEWSLETTER` | boolean | Разрешить использование в CRM-рассылках (по умолчанию `true`) |
| `NEED_SYSTEM_MESSAGES` | boolean | Разрешить отправку системных сообщений (по умолчанию `true`) |
| `NEED_SIGNATURE` | boolean | Добавлять подпись оператора (по умолчанию `true`) |
| `CHAT_GROUP` | boolean | Режим группировки: `true` — по `chat.id`, `false` — по `user.id` (по умолчанию `false`) |
| `COMMENT` | string | Текстовое пояснение в настройках коннектора |

**Структура объекта `ICON`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `DATA_IMAGE` | string | SVG-иконка в формате Data URI (`data:image/svg+xml,...`) |
| `COLOR` | string | Цвет фона иконки (например, `#69acc0`) |
| `SIZE` | string | Размер фона (например, `90%`) |
| `POSITION` | string | Позиция фона (например, `center`) |

**Структура объекта `ICON_DISABLED`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `DATA_IMAGE` | string | SVG-иконка неактивного состояния в формате Data URI |
| `COLOR` | string | Цвет фона неактивной иконки |
| `SIZE` | string | Размер фона неактивной иконки |
| `POSITION` | string | Позиция фона неактивной иконки |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{
    "ID": "myconnector",
    "NAME": "Мой коннектор",
    "ICON": {
      "DATA_IMAGE": "data:image/svg+xml,%3Csvg%20xmlns%3D%22http://www.w3.org/2000/svg%22/%3E",
      "COLOR": "#69acc0",
      "SIZE": "90%",
      "POSITION": "center"
    },
    "PLACEMENT_HANDLER": "https://example.com/connector/settings",
    "ICON_DISABLED": {
      "DATA_IMAGE": "data:image/svg+xml,%3Csvg%20xmlns%3D%22http://www.w3.org/2000/svg%22/%3E",
      "COLOR": "#99adb3"
    },
    "DEL_EXTERNAL_MESSAGES": true,
    "EDIT_INTERNAL_MESSAGES": true,
    "DEL_INTERNAL_MESSAGES": true,
    "NEWSLETTER": true,
    "NEED_SYSTEM_MESSAGES": true,
    "NEED_SIGNATURE": true,
    "CHAT_GROUP": false,
    "COMMENT": "Настройка канала"
  }' \
  https://your-domain.bitrix24.ru/rest/imconnector.register?auth=**put_access_token_here**
```

**Пример ответа (HTTP 200):**
```json
{
    "result": {
        "result": true
    },
    "time": {
        "start": 1738065600.11,
        "finish": 1738065600.38,
        "duration": 0.27,
        "processing": 0.10,
        "date_start": "2025-01-28T12:00:00+00:00",
        "date_finish": "2025-01-28T12:00:00+00:00"
    }
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | boolean | `true`, если коннектор успешно зарегистрирован |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

Метод может возвращать ошибки в двух форматах:

1. **HTTP 200** с `result = false`:

| Код | Описание |
|-----|----------|
| `APPLICATION_REGISTRATION_ERROR_POINT` | В идентификаторе коннектора использован символ `.` |
| `CONNECTOR_ID_REQUIRED` | Пустой или нестроковый `ID` |
| `NAME_REQUIRED` | Пустой или нестроковый `NAME` |
| `ICON_REQUIRED` | Не передан `ICON.DATA_IMAGE` |
| `NO_APPLICATION_ID` | Не удалось получить ID приложения |
| `NO_PLACEMENT_HANDLER` | Пустой или нестроковый `PLACEMENT_HANDLER` |
| `APPLICATION_REGISTRATION_ERROR` | Не удалось завершить регистрацию |
| `GENERAL_CONNECTOR_REGISTRATION_ERROR` | Общая ошибка валидации |

2. **HTTP 403** для системной ошибки авторизации:

| Статус | Код | Описание |
|--------|-----|----------|
| 403 | `WRONG_AUTH_TYPE` | Метод вызван не в контексте приложения (требуется OAuth) |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)
