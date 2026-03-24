# Методы списка чатов im

---

## im.recent.get

**Scope:** `im`  
**Кто может выполнять:** любой пользователь  
**Параметры:** все опциональные

**Описание:**  
Получает список последних чатов пользователя.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `SKIP_OPENLINES` | string | Пропустить чаты открытых линий: `Y` или `N` |
| `SKIP_CHAT` | string | Пропустить групповые чаты: `Y` или `N` |
| `SKIP_DIALOG` | string | Пропустить диалоги один-на-один: `Y` или `N` |
| `LAST_UPDATE` | datetime | Выборка с указанной даты в формате ATOM (ISO-8601) |
| `ONLY_OPENLINES` | string | Только чаты открытых линий: `Y` или `N` |
| `LAST_SYNC_DATE` | datetime | Дата предыдущей выборки для загрузки изменений (не старше 7 дней) |

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"SKIP_OPENLINES":"Y","LAST_UPDATE":"2026-02-25T18:30:00+01:00"}' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/im.recent.get.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": [
        {
            "id": "chat1451",
            "chat_id": 1451,
            "type": "chat",
            "avatar": {
                "url": "",
                "color": "#df532d"
            },
            "title": "Максимально полный шаблон задачи",
            "message": {...},
            "counter": 0,
            "last_id": 84501,
            "pinned": false,
            "unread": false,
            "has_reminder": false,
            "date_update": "2026-02-26T00:01:26+03:00",
            "date_last_activity": "2026-02-26T00:01:26+03:00",
            "chat": {...},
            "user": {...},
            "options": []
        }
    ],
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | array | Список последних диалогов |
| `time` | time | Информация о времени выполнения запроса |

**Структура элемента `result[]`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `id` | string | Идентификатор диалога: число для пользователя, `chatXXX` для чата |
| `type` | string | Тип записи: `user` или `chat` |
| `avatar` | object | Описание аватара |
| `title` | string | Заголовок: имя для пользователя, название для чата |
| `message` | object | Описание последнего сообщения |
| `counter` | integer | Счетчик непрочитанных сообщений |
| `chat_id` | integer | Идентификатор чата |
| `last_id` | integer | Идентификатор последнего прочитанного сообщения |
| `pinned` | boolean | Признак закрепленного диалога |
| `unread` | boolean | Признак ручной отметки «не прочитано» |
| `has_reminder` | boolean | Признак установленного напоминания |
| `date_update` | datetime | Дата обновления в списке (ATOM) |
| `date_last_activity` | datetime | Дата последней активности (ATOM) |
| `user` | object | Описание пользователя (для типа `user`) |
| `chat` | object | Описание чата (для типа `chat`) |
| `options` | array | Дополнительные параметры |

**Объект `avatar`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `url` | string | Ссылка на аватар |
| `color` | string | Цвет диалога (HEX) |

**Объект `message`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `id` | integer | Идентификатор сообщения |
| `text` | string | Текст без BB-кодов |
| `file` | boolean | Признак наличия файлов |
| `attach` | boolean | Признак наличия вложений |
| `author_id` | integer | ID автора |
| `date` | datetime | Дата сообщения (ATOM) |
| `sticker` | integer | ID стикера или `null` |
| `status` | string | Статус доставки |
| `uuid` | string | Внешний ID или `null` |

**Объект `user`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `id` | integer | Идентификатор пользователя |
| `name` | string | Имя и фамилия |
| `first_name` | string | Имя |
| `last_name` | string | Фамилия |
| `work_position` | string | Должность |
| `color` | string | Цвет (HEX) |
| `avatar` | string | Ссылка на аватар |
| `gender` | string | Пол |
| `birthday` | string | День рождения (`DD-MM`) |
| `extranet` | boolean | Признак экстранета |
| `network` | boolean | Признак Network |
| `bot` | boolean | Признак бота |
| `connector` | boolean | Признак коннектора |
| `external_auth_id` | string | ID внешней авторизации |
| `status` | string | Статус пользователя |
| `idle` | datetime | Дата, когда отошел (ATOM) или `false` |
| `last_activity_date` | datetime | Дата последней активности (ATOM) |
| `mobile_last_date` | datetime | Дата активности в мобильном (ATOM) или `false` |
| `absent` | datetime | Дата окончания отпуска (ATOM) или `false` |

**Объект `chat`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `id` | integer | Идентификатор чата |
| `name` | string | Название чата |
| `owner` | integer | ID владельца |
| `extranet` | boolean | Признак участия экстранет-пользователя |
| `parent_chat_id` | integer | ID родительского чата |
| `parent_message_id` | integer | ID родительского сообщения |
| `contains_collaber` | boolean | Признак участия коллаб-пользователей |
| `color` | string | Цвет (HEX) |
| `avatar` | string | Ссылка на аватар |
| `type` | string | Тип чата |
| `entity_type` | string | Внешний код типа |
| `entity_id` | string | Внешний ID |
| `entity_data_1` | string | Внешние данные |
| `entity_data_2` | string | Внешние данные |
| `entity_data_3` | string | Внешние данные |
| `date_create` | datetime | Дата создания (ATOM) |
| `message_type` | string | Тип сообщений |
| `mute_list` | array | Пользователи с отключенными уведомлениями |
| `manager_list` | array | ID менеджеров чата |
| `user_counter` | integer | Количество участников |
| `restrictions` | object | Ограничения в чате |
| `role` | string | Роль текущего пользователя |
| `text_field_enabled` | boolean | Доступность поля ввода |
| `background_id` | integer | ID фона чата |
| `entity_link` | object | Ссылка на связанный объект |
| `permissions` | object | Права действий в чате |
| `public` | string | Признак публичности |

**Объект `restrictions`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `avatar` | boolean | Доступность изменения аватара |
| `rename` | boolean | Доступность изменения названия |
| `extend` | boolean | Доступность расширения чата |
| `call` | boolean | Доступность звонков |
| `mute` | boolean | Доступность отключения уведомлений |
| `leave` | boolean | Доступность выхода из чата |
| `leave_owner` | boolean | Доступность выхода владельца |
| `send` | boolean | Доступность отправки сообщений |
| `user_list` | boolean | Доступность просмотра списка участников |

**Объект `entity_link`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `type` | string | Тип связанного объекта |
| `url` | string | Ссылка на объект |
| `id` | string | ID связанного объекта |

**Объект `permissions`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `manage_users_add` | string | Право на добавление участников |
| `manage_users_delete` | string | Право на удаление участников |
| `manage_ui` | string | Право на управление интерфейсом |
| `manage_settings` | string | Право на управление настройками |
| `manage_messages` | string | Право на управление сообщениями |
| `can_post` | string | Право на отправку сообщений |

**Обработка ошибок:**

Специфичные ошибки метода: отсутствуют

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## im.recent.list

**Scope:** `im`  
**Кто может выполнять:** любой пользователь  
**Параметры:** все опциональные

**Описание:**  
Получает список последних диалогов пользователя с поддержкой пагинации.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `SKIP_OPENLINES` | string | Пропускать чаты открытых линий: `Y` или `N` |
| `SKIP_DIALOG` | string | Пропускать диалоги один-на-один: `Y` или `N` |
| `SKIP_CHAT` | string | Пропускать групповые чаты: `Y` или `N` |
| `LAST_MESSAGE_DATE` | datetime | Дата последнего элемента предыдущей выборки (ATOM) |
| `UNREAD_ONLY` | string | Только диалоги с непрочитанными: `Y` или `N` |
| `PARSE_TEXT` | string | Парсить текст сообщения: `Y` или `N` |
| `GET_ORIGINAL_TEXT` | string | Вернуть оригинальный текст: `Y` или `N` |
| `SKIP_UNDISTRIBUTED_OPENLINES` | string | Пропускать нераспределенные чаты: `Y` или `N` |
| `ONLY_COPILOT` | string | Только чаты BitrixGPT: `Y` или `N` |
| `ONLY_CHANNEL` | string | Только каналы: `Y` или `N` |
| `CAN_MANAGE_MESSAGES` | string | Только с правом управления сообщениями: `Y` или `N` |
| `OFFSET` | integer | Смещение для постраничной выборки (по умолчанию 0) |
| `LIMIT` | integer | Количество элементов (по умолчанию 50, макс. 200) |

> **Рекомендации по пагинации:**
> - Для перехода на следующую страницу увеличивайте `OFFSET` на значение `LIMIT` (0, 50, 100)
> - Между страницами могут повторяться одни и те же диалоги
> - Если чаты открытых линий не нужны, передавайте `SKIP_OPENLINES = Y`
> - Для небольшого списка запрашивайте одним вызовом с увеличенным `LIMIT`

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{
    "LAST_MESSAGE_DATE":"2026-02-25T18:30:00+03:00",
    "SKIP_OPENLINES":"N",
    "UNREAD_ONLY":"Y",
    "OFFSET":0,
    "LIMIT":20
  }' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/im.recent.list.json
```

**Пример ответа (HTTP 200):**
```json
{
    "result": {
        "items": [...],
        "hasMorePages": false,
        "hasMore": false,
        "copilot": {...},
        "messagesAutoDeleteConfigs": []
    },
    "total": -1,
    "time": {...}
}
```

**Возвращаемые данные:**

| Название | Тип | Описание |
|----------|-----|----------|
| `result` | object | Корневой объект результата |
| `total` | integer | Общее количество элементов (обычно -1) |
| `time` | time | Информация о времени выполнения запроса |

**Структура объекта `result`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `items` | array | Список последних диалогов |
| `hasMorePages` | boolean | Устаревающий алиас поля `hasMore` |
| `hasMore` | boolean | Признак наличия следующей страницы |
| `copilot` | object | Данные для BitrixGPT |
| `messagesAutoDeleteConfigs` | array | Настройки автоудаления сообщений |

**Структура элемента `items[]`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `id` | string | Идентификатор диалога |
| `chat_id` | integer | Идентификатор чата |
| `type` | string | Тип записи: `user` или `chat` |
| `avatar` | object | Объект аватара |
| `title` | string | Заголовок записи |
| `message` | object | Последнее сообщение |
| `counter` | integer | Счетчик непрочитанных |
| `last_id` | integer | ID последнего прочитанного |
| `pinned` | boolean | Признак закрепленного |
| `unread` | boolean | Признак ручной метки «не прочитано» |
| `has_reminder` | boolean | Признак напоминания |
| `date_update` | datetime | Дата изменения (ISO 8601) |
| `date_last_activity` | datetime | Дата последней активности |
| `user` | object | Данные пользователя |
| `chat` | object | Данные чата |
| `lines` | object | Данные открытой линии |
| `options` | array | Дополнительные параметры |

**Объект `avatar`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `url` | string | Ссылка на аватар |
| `color` | string | Цвет диалога (HEX) |

**Объект `message`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `id` | integer | Идентификатор сообщения |
| `text` | string | Текст сообщения |
| `file` | boolean | Признак наличия файлов |
| `author_id` | integer | ID автора |
| `attach` | boolean | Признак наличия вложений |
| `date` | datetime | Дата сообщения (ATOM) |
| `status` | string | Статус доставки |
| `sticker` | integer | ID стикера или `null` |
| `uuid` | string | Внешний ID или `null` |

**Объект `user`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `id` | integer | ID пользователя |
| `active` | boolean | Признак активного |
| `name` | string | Имя и фамилия |
| `first_name` | string | Имя |
| `last_name` | string | Фамилия |
| `work_position` | string | Должность |
| `color` | string | Цвет (HEX) |
| `avatar` | string | Ссылка на аватар |
| `avatar_hr` | string | Ссылка на аватар высокого разрешения |
| `gender` | string | Пол |
| `birthday` | string | День рождения (`DD-MM`) |
| `extranet` | boolean | Признак экстранета |
| `network` | boolean | Признак Network |
| `bot` | boolean | Признак бота |
| `connector` | boolean | Признак коннектора |
| `external_auth_id` | string | ID внешней авторизации |
| `status` | string | Статус пользователя |
| `idle` | datetime | Дата, когда отошел |
| `last_activity_date` | datetime | Дата последней активности |
| `departments` | array | Список ID отделов |
| `phones` | object | Телефоны |
| `bot_data` | object | Данные бота |
| `type` | string | Тип пользователя |
| `website` | string | Сайт |
| `email` | string | Email |

**Объект `chat`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `id` | integer | ID чата |
| `parent_chat_id` | integer | ID родительского чата |
| `parent_message_id` | integer | ID родительского сообщения |
| `name` | string | Название чата |
| `owner` | integer | ID владельца |
| `extranet` | boolean | Признак экстранета |
| `contains_collaber` | boolean | Признак коллаб-пользователей |
| `avatar` | string | Ссылка на аватар |
| `color` | string | Цвет (HEX) |
| `type` | string | Тип чата |
| `entity_type` | string | Внешний код типа |
| `entity_id` | string | Внешний ID |
| `entity_data_1` | string | Внешние данные 1 |
| `entity_data_2` | string | Внешние данные 2 |
| `entity_data_3` | string | Внешние данные 3 |
| `mute_list` | array | Пользователи с отключенными уведомлениями |
| `manager_list` | array | ID менеджеров |
| `date_create` | datetime | Дата создания (ATOM) |
| `message_type` | string | Тип сообщений |
| `user_counter` | integer | Количество участников |
| `restrictions` | object | Ограничения |
| `role` | string | Роль пользователя |
| `text_field_enabled` | boolean | Доступность поля ввода |
| `background_id` | integer | ID фона |
| `entity_link` | object | Ссылка на объект |
| `permissions` | object | Права действий |
| `public` | string | Признак публичности |

**Объект `lines`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `id` | integer | ID открытой линии |
| `status` | integer | Статус линии |
| `date_create` | datetime | Дата создания (ATOM) |

**Объект `restrictions`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `avatar` | boolean | Изменение аватара |
| `rename` | boolean | Изменение названия |
| `extend` | boolean | Расширение чата |
| `call` | boolean | Звонки |
| `mute` | boolean | Отключение уведомлений |
| `leave` | boolean | Выход из чата |
| `leave_owner` | boolean | Выход владельца |
| `send` | boolean | Отправка сообщений |
| `user_list` | boolean | Просмотр списка участников |

**Объект `entity_link`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `type` | string | Тип объекта |
| `url` | string | Ссылка |
| `id` | string | ID объекта |

**Объект `permissions`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `manage_users_add` | string | Добавление участников |
| `manage_users_delete` | string | Удаление участников |
| `manage_ui` | string | Управление интерфейсом |
| `manage_settings` | string | Управление настройками |
| `manage_messages` | string | Управление сообщениями |
| `can_post` | string | Отправка сообщений |

**Объект `copilot`:**

| Название | Тип | Описание |
|----------|-----|----------|
| `chats` | object | Данные BitrixGPT-чатов |
| `messages` | object | Данные BitrixGPT-сообщений |
| `roles` | object | Описание доступных ролей |
| `recommendedRoles` | array | Список рекомендуемых ролей |

**Обработка ошибок:**

Специфичные ошибки метода: отсутствуют

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## im.recent.pin

**Scope:** `im`  
**Кто может выполнять:** участник чата  
**Параметры:** `DIALOG_ID` (обязательный), `PIN` (опциональный)

**Описание:**  
Закрепляет или открепляет диалог вверху списка чатов пользователя.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `DIALOG_ID` | string | Идентификатор чата: `chatXXX` — чат, `sgXXX` — чат группы, `XXX` — ID пользователя |
| `PIN` | string | `Y` — закрепить, `N` — открепить (по умолчанию `Y`) |

> **Примечание:** ID чата можно получить через `im.chat.get`, ID пользователя — через `user.get` или `user.search`.

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"DIALOG_ID":"chat1489","PIN":"Y"}' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/im.recent.pin.json
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
| `result` | boolean | `true`, если диалог успешно закреплен/откреплен |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 400 | `DIALOG_ID_EMPTY` | `DIALOG_ID` не передан, пустой или в неверном формате |
| 400 | `ACCESS_ERROR` | Нет доступа к чату |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## im.recent.hide

**Scope:** `im`  
**Кто может выполнять:** любой пользователь  
**Параметры:** `DIALOG_ID` (обязательный)

**Описание:**  
Удаляет диалог из списка последних чатов текущего пользователя.

> **Примечание:** Получить список последних чатов можно методом `im.recent.get`.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `DIALOG_ID` | string | Идентификатор чата: `chatXXX` — чат, `sgXXX` — чат группы, `XXX` — ID пользователя |

> **Примечание:** ID чата можно получить через `im.chat.get`, ID пользователя — через `user.get` или `user.search`.

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"DIALOG_ID":"chat1489"}' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/im.recent.hide.json
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
| `result` | boolean | `true`, если диалог успешно удален из списка последних чатов |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 400 | `DIALOG_ID_EMPTY` | `DIALOG_ID` не передан, пустой или в неверном формате |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)

---

## im.recent.unread

**Scope:** `im`  
**Кто может выполнять:** любой пользователь  
**Параметры:** `DIALOG_ID` (обязательный), `ACTION` (опциональный)

**Описание:**  
Устанавливает или снимает признак «прочитано» у чата.

**Параметры метода:**

| Название | Тип | Описание |
|----------|-----|----------|
| `DIALOG_ID` | string | Идентификатор чата: `chatXXX` — чат, `sgXXX` — чат группы, `XXX` — ID пользователя |
| `ACTION` | string | `Y` — установить метку, `N` — снять метку (по умолчанию `Y`) |

> **Примечание:** ID чата можно получить через `im.chat.get`, ID пользователя — через `user.get` или `user.search`.

**Пример запроса:**
```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Accept: application/json" \
  -d '{"DIALOG_ID":"chat2941","ACTION":"Y"}' \
  https://your-domain.bitrix24.ru/rest/1/webhook_key/im.recent.unread.json
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
| `result` | boolean | `true`, если метка установлена/снята. `false` — чат не найден |
| `time` | time | Информация о времени выполнения запроса |

**Обработка ошибок:**

| Статус | Код | Описание |
|--------|-----|----------|
| 400 | `DIALOG_ID_EMPTY` | `DIALOG_ID` не передан или в неверном формате |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)
