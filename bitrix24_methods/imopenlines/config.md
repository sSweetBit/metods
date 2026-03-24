# Методы конфигурации imopenlines

---

## imopenlines.config.add

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь  
**Параметры:** `PARAMS` (объект)

**Описание:**  
Добавляет новую открытую линию.

> **Примечание:** Чтобы пользователи могли писать в открытую линию, необходимо настроить коннектор методом `imconnector.connector.data.set`.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `PARAMS` | object | Объект с настройками открытой линии |

**Основные поля `PARAMS`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `LINE_NAME` | string | Название открытой линии |
| `ACTIVE` | char | Активность: `Y` — активна, `N` — неактивна |
| `QUEUE` | array | Очередь операторов (объекты с `ENTITY_TYPE` и `ENTITY_ID`) |
| `QUEUE_TYPE` | string | Режим распределения: `evenly`, `strictly`, `all` |
| `QUEUE_TIME` | integer | Время до перехода к следующему оператору (сек) |
| `NO_ANSWER_TIME` | integer | Время до сценария без ответа (сек) |
| `WELCOME_MESSAGE` | char | Отправлять приветствие: `Y`/`N` |
| `WELCOME_MESSAGE_TEXT` | string | Текст приветственного сообщения |
| `WORKTIME_ENABLE` | char | Учитывать рабочее время: `Y`/`N` |
| `WORKTIME_FROM` | string | Начало рабочего времени (HH:MM) |
| `WORKTIME_TO` | string | Окончание рабочего времени (HH:MM) |
| `WORKTIME_TIMEZONE` | string | Часовой пояс |
| `CRM` | char | Искать клиента в CRM: `Y`/`N` |
| `CRM_CREATE` | string | Что создавать в CRM для нового клиента |
| `VOTE_MESSAGE` | char | Запрашивать оценку: `Y`/`N` |
| `LANGUAGE_ID` | string | Язык линии |
| `MAX_CHAT` | integer | Максимум одновременных диалогов у оператора |
| `TYPE_MAX_CHAT` | string | Тип ограничения: `answered`, `answered_new`, `closed` |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{
    "PARAMS": {
      "LINE_NAME": "Линия поддержки",
      "QUEUE": [
        {"ENTITY_TYPE": "user", "ENTITY_ID": "1"},
        {"ENTITY_TYPE": "user", "ENTITY_ID": "15"}
      ],
      "QUEUE_TYPE": "strictly",
      "QUEUE_TIME": 45,
      "WELCOME_MESSAGE": "Y",
      "WELCOME_MESSAGE_TEXT": "Здравствуйте!",
      "WORKTIME_ENABLE": "Y",
      "WORKTIME_FROM": "09:00",
      "WORKTIME_TO": "21:00",
      "WORKTIME_TIMEZONE": "Europe/Moscow"
    }
  }' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.config.add.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": 15,
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | integer | Идентификатор созданной открытой линии |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

Специфичные ошибки: отсутствуют

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## imopenlines.config.get

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь  
**Параметры:** `CONFIG_ID` (обязательный), `WITH_QUEUE` (опциональный), `SHOW_OFFLINE` (опциональный)

**Описание:**  
Получает настройки открытой линии по идентификатору.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `CONFIG_ID` | integer | Идентификатор открытой линии |
| `WITH_QUEUE` | char | Возвращать данные очереди: `Y`/`N` |
| `SHOW_OFFLINE` | char | Возвращать офлайн-операторов: `Y`/`N` |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"CONFIG_ID":15,"WITH_QUEUE":"Y"}' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.config.get.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": {
        "ID": "22",
        "LINE_NAME": "Линия поддержки",
        "ACTIVE": "Y",
        "QUEUE": ["27", "103"],
        ...
    },
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | object | Объект с настройками линии (или `false`, если не существует) |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 400 | `CONFIG_ID_EMPTY` | Параметр `CONFIG_ID` не передан или некорректен |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## imopenlines.config.list.get

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь  
**Параметры:** `PARAMS` (объект), `OPTIONS` (объект)

**Описание:**  
Получает список открытых линий с поддержкой фильтрации, сортировки и постраничной выборки.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `PARAMS` | object | Параметры выборки |
| `OPTIONS` | object | Дополнительные опции |

**Структура `PARAMS`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `select` | array | Массив полей для выбора |
| `order` | object | Сортировка: `{"field": "ASC"}` или `{"field": "DESC"}` |
| `filter` | object | Фильтр: `{"field": "value"}` |
| `limit` | integer | Количество элементов (по умолчанию 50, макс. 200) |
| `offset` | integer | Смещение для постраничной выборки |

**Структура `OPTIONS`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `QUEUE` | char | Возвращать очередь операторов: `Y`/`N` |
| `CONFIG_QUEUE` | char | Возвращать очередь линии: `Y`/`N` |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{
    "PARAMS": {
      "select": ["ID", "LINE_NAME", "ACTIVE"],
      "order": {"ID": "ASC"},
      "filter": {"ACTIVE": "Y"},
      "limit": 50
    },
    "OPTIONS": {
      "QUEUE": "Y"
    }
  }' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.config.list.get.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": [
        {
            "ID": "15",
            "LINE_NAME": "Линия поддержки VIP",
            "ACTIVE": "Y",
            "QUEUE": [101, 205],
            ...
        }
    ],
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | array | Список открытых линий |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 400 | `INVALID_FORMAT` | Неверный формат полей `PARAMS.select`, `PARAMS.order` или `PARAMS.filter` |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## imopenlines.config.update

**Scope:** `imopenlines`  
**Кто может выполнять:** пользователь с правом изменения открытых линий  
**Параметры:** `CONFIG_ID` (обязательный), `PARAMS` (объект)

**Описание:**  
Изменяет открытую линию.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `CONFIG_ID` | integer | Идентификатор открытой линии |
| `PARAMS` | object | Объект с настройками для обновления |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{
    "CONFIG_ID": 15,
    "PARAMS": {
      "LINE_NAME": "Линия поддержки (обновленная)",
      "QUEUE_TIME": 60
    }
  }' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.config.update.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": true,
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | boolean | `true` — обновлена, `false` — не существует |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 400 | `CONFIG_ID_EMPTY` | Параметр `CONFIG_ID` не передан или некорректен |
| 403 | `CONFIG_WRONG_USER_PERMISSION` | Недостаточно прав для изменения линии |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## imopenlines.config.delete

**Scope:** `imopenlines`  
**Кто может выполнять:** пользователь с правом изменения открытых линий  
**Параметры:** `CONFIG_ID` (обязательный)

**Описание:**  
Удаляет открытую линию.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `CONFIG_ID` | integer | Идентификатор открытой линии |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"CONFIG_ID": 15}' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.config.delete.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": true,
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | boolean | `true` — удалена, `false` — не существует |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 400 | `CONFIG_ID_EMPTY` | Параметр `CONFIG_ID` не передан или некорректен |
| 403 | `CONFIG_WRONG_USER_PERMISSION` | Недостаточно прав для удаления линии |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## imopenlines.config.path.get

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь  
**Параметры:** нет

**Описание:**  
Получает ссылку на публичную страницу открытых линий портала.

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.config.path.get.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": {
        "SERVER_ADDRESS": "https://example.bitrix24.ru",
        "PUBLIC_PATH": "/contact_center/"
    },
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | object | Объект с адресом портала и публичным путем |
| `time` | time | Информация о времени выполнения запроса |

**Структура объекта `result`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `SERVER_ADDRESS` | string | Базовый адрес портала |
| `PUBLIC_PATH` | string | Относительный путь к публичной странице |

**Обработка ошибок:**

Специфичные ошибки: отсутствуют

Общие ошибки: см. [Обработка ошибок](../common/errors.md)
