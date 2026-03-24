# Системные методы imopenlines

---

## imopenlines.revision.get

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь  
**Параметры:** нет

**Описание:**  
Получает информацию о ревизиях API Открытых линий.

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.revision.get.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": {
        "rest": 2,
        "web": 1,
        "mobile": 1
    },
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | object | Корневой объект с ревизиями API |
| `time` | time | Информация о времени выполнения запроса |

**Структура объекта `result`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `rest` | integer | Ревизия API для REST-клиентов |
| `web` | integer | Ревизия API для веб- и десктоп-клиента |
| `mobile` | integer | Ревизия API для мобильного клиента |

**Обработка ошибок:**

Специфичные ошибки: отсутствуют

Общие ошибки: см. [Обработка ошибок](../common/errors.md)
