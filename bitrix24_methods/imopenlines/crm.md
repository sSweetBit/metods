# Методы CRM imopenlines

---

## imopenlines.crm.chat.get

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь с доступом к объекту CRM  
**Параметры:** `CRM_ENTITY_TYPE`, `CRM_ENTITY` (обязательные), `ACTIVE_ONLY` (опциональный)

**Описание:**  
Получает список чатов, которые привязаны к объекту CRM.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `CRM_ENTITY_TYPE` | string | Тип объекта CRM: `lead`, `deal`, `company`, `contact` |
| `CRM_ENTITY` | integer | Идентификатор объекта CRM |
| `ACTIVE_ONLY` | char | Только активные чаты: `Y` (по умолчанию), `N` — все |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"CRM_ENTITY_TYPE":"lead","CRM_ENTITY":1205,"ACTIVE_ONLY":"N"}' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.crm.chat.get.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": [
        {
            "CHAT_ID": "1763",
            "CONNECTOR_ID": "livechat",
            "CONNECTOR_TITLE": "Онлайн-чат"
        }
    ],
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | array | Список объектов чатов (пустой массив, если объект не существует) |
| `time` | time | Информация о времени выполнения запроса |

**Структура элемента `result`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `CHAT_ID` | string | Идентификатор чата |
| `CONNECTOR_ID` | string | Идентификатор коннектора |
| `CONNECTOR_TITLE` | string | Название коннектора |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 403 | `ACCESS_DENIED` | Нет доступа к объекту CRM |
| 400 | `ERROR_ARGUMENT` | Не передан или пустой параметр `CRM_ENTITY_TYPE` |
| 400 | `ERROR_ARGUMENT` | Не передан или пустой параметр `CRM_ENTITY` |
| 400 | `ERROR_ARGUMENT` | Параметр `CRM_ENTITY` передан в неверном формате |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## imopenlines.crm.chat.getLastId

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь с доступом к объекту CRM  
**Параметры:** `CRM_ENTITY_TYPE`, `CRM_ENTITY` (обязательные)

**Описание:**  
Получает идентификатор последнего чата, который привязан к объекту CRM.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `CRM_ENTITY_TYPE` | string | Тип объекта CRM: `lead`, `deal`, `company`, `contact` |
| `CRM_ENTITY` | integer | Идентификатор объекта CRM |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"CRM_ENTITY_TYPE":"lead","CRM_ENTITY":1205}' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.crm.chat.getLastId.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": 1763,
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | integer | Идентификатор последнего чата |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 400 | `CRM_CHAT_EMPTY_CRM_DATA` | Не переданы `CRM_ENTITY_TYPE` и `CRM_ENTITY` |
| 400 | `CRM_CHAT_EMPTY_CRM_DATA` | Чат не найден, неверный тип, несуществующий объект или нет доступа |
| 400 | `ERROR_ARGUMENT` | Параметр `CRM_ENTITY` передан в неверном формате |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## imopenlines.crm.chat.user.add

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь с доступом к объекту CRM  
**Параметры:** `CRM_ENTITY_TYPE`, `CRM_ENTITY`, `USER_ID` (обязательные), `CHAT_ID` (опциональный)

**Описание:**  
Добавляет пользователя в чат, привязанный к объекту CRM.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `CRM_ENTITY_TYPE` | string | Тип объекта CRM: `lead`, `deal`, `company`, `contact` |
| `CRM_ENTITY` | integer | Идентификатор объекта CRM |
| `USER_ID` | integer | Идентификатор пользователя или бота для добавления |
| `CHAT_ID` | integer | Идентификатор чата (по умолчанию — последний чат объекта CRM) |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"CRM_ENTITY_TYPE":"lead","CRM_ENTITY":1205,"USER_ID":503,"CHAT_ID":1763}' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.crm.chat.user.add.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": 1763,
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | integer | Идентификатор чата, в который добавлен пользователь (или `0`, если чат не найден) |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 403 | `ACCESS_DENIED` | Нет прав на добавление пользователей в чат объекта CRM |
| 403 | `ACCESS_DENIED` | У пользователя `USER_ID` нет доступа к объекту CRM |
| 400 | `ERROR_ARGUMENT` | Не передан обязательный параметр |
| 400 | `IM_NOT_INSTALLED` | Не установлен модуль `im` |
| 400 | `CHAT_NOT_IN_CRM` | Чат не связан с объектом CRM |
| 400 | `CRM_CHAT_USER_NOT_ACTIVE` | Нет доступа к списку пользователей вне линии |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## imopenlines.crm.chat.user.delete

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь с доступом к объекту CRM  
**Параметры:** `CRM_ENTITY_TYPE`, `CRM_ENTITY`, `USER_ID` (обязательные), `CHAT_ID` (опциональный)

**Описание:**  
Удаляет пользователя из чата, привязанного к объекту CRM.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `CRM_ENTITY_TYPE` | string | Тип объекта CRM: `lead`, `deal`, `company`, `contact` |
| `CRM_ENTITY` | integer | Идентификатор объекта CRM |
| `USER_ID` | integer | Идентификатор пользователя для удаления |
| `CHAT_ID` | integer | Идентификатор чата (по умолчанию — последний чат объекта CRM) |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"CRM_ENTITY_TYPE":"lead","CRM_ENTITY":1205,"USER_ID":503,"CHAT_ID":1763}' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.crm.chat.user.delete.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": 1763,
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | integer | Идентификатор чата, из которого удален пользователь (или `0`, если чат не найден) |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 403 | `ACCESS_DENIED` | Нет доступа к объекту CRM или неверный `CRM_ENTITY_TYPE` |
| 400 | `CRM_CHAT_EMPTY_USER` | Не указан параметр `USER_ID` |
| 400 | `CRM_CHAT_EMPTY_CRM_DATA` | Не переданы `CRM_ENTITY_TYPE` и `CRM_ENTITY` |
| 400 | `ERROR_ARGUMENT` | Параметр `CRM_ENTITY` передан в неверном формате |
| 400 | `IM_NOT_INSTALLED` | Не установлен модуль `im` |
| 400 | `CHAT_NOT_IN_CRM` | Чат не связан с объектом CRM или не существует |
| 403 | `CHAT_DELETE_USER_PERMISSION_DENIED` | Нет прав на удаление участника из чата |
| 400 | `CRM_CHAT_USER_NOT_ACTIVE` | Удаляемый пользователь не активен или не существует |
| 400 | `WRONG_REQUEST` | Пользователь уже удален или недоступен |
| 400 | `USER_NOT_FOUND` | Пользователь не состоит в указанном чате |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## imopenlines.crm.message.add

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь  
**Параметры:** `CRM_ENTITY_TYPE`, `CRM_ENTITY`, `USER_ID`, `CHAT_ID`, `MESSAGE` (все обязательные)

**Описание:**  
Отправляет сообщение от имени сотрудника или бота в чат, который привязан к элементу CRM.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `CRM_ENTITY_TYPE` | string | Тип объекта CRM: `lead`, `deal`, `company`, `contact` |
| `CRM_ENTITY` | integer | Идентификатор элемента CRM |
| `USER_ID` | integer | Идентификатор отправителя (пользователя или бота) |
| `CHAT_ID` | integer | Идентификатор чата открытой линии |
| `MESSAGE` | string | Текст сообщения |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"CRM_ENTITY_TYPE":"lead","CRM_ENTITY":1195,"USER_ID":27,"CHAT_ID":1341,"MESSAGE":"Текст сообщения"}' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.crm.message.add.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": 19880117,
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | integer | Идентификатор созданного сообщения в чате |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 400 | `CHAT_NOT_IN_CRM` | Чат не связан с CRM |
| 400 | `CANCELED` | Нет доступа к чату для отправки сообщений |
| 403 | `ACCESS_DENIED` | Нет доступа к объекту CRM |
| 400 | `ERROR_ARGUMENT` | Неверно указан обязательный параметр |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## imopenlines.crm.lead.create

**Scope:** `imopenlines`  
**Кто может выполнять:** любой пользователь с правом на доступ к диалогу  
**Параметры:** `CHAT_ID` (обязательный)

**Описание:**  
Создает лид CRM по текущему чату открытой линии.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `CHAT_ID` | integer | Идентификатор чата открытой линии |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"CHAT_ID":2043}' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/imopenlines.crm.lead.create.json
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
| `result` | boolean | `true`, если лид успешно создан |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 400 | `CHAT_ID` | Указан не корректный идентификатор чата |
| 400 | `CHAT_TYPE` | Указанный чат не является открытой линией |
| 400 | `ACCESS_DENIED` | Недостаточно прав на диалог |
| 400 | `USER_ID` | Не определен пользователь |
| 400 | `ERROR_USER_NOT_OPERATOR` | Метод вызван пользователем, который не является текущим оператором сессии |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)
