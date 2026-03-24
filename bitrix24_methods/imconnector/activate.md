# Методы активации imconnector

---

## imconnector.activate

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь  
**Параметры:** `CONNECTOR`, `LINE`, `ACTIVE` (все обязательные)

**Описание:**  
Активирует или деактивирует коннектор на указанной открытой линии.

> **Важно:** Метод работает только в контексте приложения (требуется OAuth авторизация).

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `CONNECTOR` | string | Строковый код коннектора (задается при регистрации через `imconnector.register`) |
| `LINE` | integer | Идентификатор открытой линии (можно получить через `imopenlines.config.get` или `imopenlines.config.list.get`) |
| `ACTIVE` | string | Признак активации: `1` или `Y` — включить, `0` или пустое значение — отключить |

> **Рекомендация:** Используйте значения `1`/`0` или `Y`/`N`.

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"CONNECTOR":"myconnector","LINE":107,"ACTIVE":"1"}' \
  https://your-domain.bitrix24.ru/rest/imconnector.activate?auth=**put_access_token_here**
```

**Пример ответа (HTTP 200):**
```json
{
    "result": true,
    "time": {
        "start": 1738065600.11,
        "finish": 1738065600.19,
        "duration": 0.08,
        "processing": 0.03,
        "date_start": "2025-01-28T12:00:00+00:00",
        "date_finish": "2025-01-28T12:00:00+00:00"
    }
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | boolean | `true`, если действие выполнено успешно |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 403 | `WRONG_AUTH_TYPE` | Метод вызван не в контексте приложения (требуется OAuth) |
| 400 | `ERROR_ARGUMENT` | Не передан параметр `CONNECTOR` |
| 400 | `ERROR_ARGUMENT` | Не передан параметр `LINE` |
| 400 | `ERROR_ARGUMENT` | Не передан параметр `ACTIVE` |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)
