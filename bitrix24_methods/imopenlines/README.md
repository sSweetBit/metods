# Открытые линии в Битрикс24: обзор методов imopenlines

> **Примечание:** Документация обновляется. Некоторые данные могут быть добавлены позже.

## Обзор методов

### Конфигурация открытых линий

| Метод | Описание |
|-------|----------|
| [imopenlines.config.add](config.md#imopenlinesconfigadd) | Добавляет новую открытую линию |
| [imopenlines.config.delete](config.md#imopenlinesconfigdelete) | Удаляет открытую линию |
| [imopenlines.config.get](config.md#imopenlinesconfigget) | Получает открытую линию по ID |
| [imopenlines.config.list.get](config.md#imopenlinesconfiglistget) | Получает список открытых линий |
| [imopenlines.config.path.get](config.md#imopenlinesconfigpathget) | Получает ссылку на публичную страницу открытых линий портала |
| [imopenlines.config.update](config.md#imopenlinesconfigupdate) | Изменяет открытую линию |
| [imopenlines.network.join](network.md#imopenlinesnetworkjoin) | Подключает внешнюю открытую линию к порталу |
| [imopenlines.revision.get](revision.md#imopenlinesrevisionget) | Получает информацию о ревизиях API |

### Чат-боты в открытых линиях

| Метод | Описание |
|-------|----------|
| [imopenlines.bot.session.finish](bot.md#imopenlinesbotsessionfinish) | Завершает диалог |
| [imopenlines.bot.session.message.send](bot.md#imopenlinesbotsessionmessagesend) | Отправляет приветственное сообщение |
| [imopenlines.bot.session.operator](bot.md#imopenlinesbotsessionoperator) | Переключает диалог на свободного оператора |
| [imopenlines.bot.session.transfer](bot.md#imopenlinesbotsessiontransfer) | Переключает диалог на оператора по ID |

### Чаты в открытых линиях

| Метод | Описание |
|-------|----------|
| [imopenlines.crm.chat.getLastId](crm.md#imopenlinescrmchatgetlastid) | Получает ID последнего чата |
| [imopenlines.crm.chat.get](crm.md#imopenlinescrmchatget) | Получает чат для объекта CRM |
| [imopenlines.crm.chat.user.add](crm.md#imopenlinescrmchatuseradd) | Добавляет пользователя к существующему чату |
| [imopenlines.crm.chat.user.delete](crm.md#imopenlinescrmchatuserdelete) | Удаляет пользователя из чата |

### Сообщения в открытых линиях

| Метод | Описание |
|-------|----------|
| [imopenlines.crm.message.add](crm.md#imopenlinescrmmessageadd) | Отправляет сообщение в открытую линию |
| [imopenlines.message.quick.save](message.md#imopenlinesmessagequicksave) | Сохраняет сообщение в качестве быстрого ответа |

### Операторы открытых линий

| Метод | Описание |
|-------|----------|
| [imopenlines.operator.another.finish](operator.md#imopenlinesoperatoranotherfinish) | Завершает диалог другого оператора |
| [imopenlines.operator.answer](operator.md#imopenlinesoperatoranswer) | Забирает диалог себе |
| [imopenlines.operator.finish](operator.md#imopenlinesoperatorfinish) | Завершает свой диалог |
| [imopenlines.operator.skip](operator.md#imopenlinesoperatorskip) | Пропускает диалог |
| [imopenlines.operator.spam](operator.md#imopenlinesoperatorspam) | Отмечает диалог в качестве «спама» |
| [imopenlines.operator.transfer](operator.md#imopenlinesoperatortransfer) | Передает диалог другому оператору или в другую линию |

### Диалоги открытых линий

| Метод | Описание |
|-------|----------|
| [imopenlines.crm.lead.create](crm.md#imopenlinescrmleadcreate) | Создает лид на основании диалога |
| [imopenlines.dialog.get](dialog.md#imopenlinesdialogget) | Получает информацию о диалоге (чате) оператора |
| [imopenlines.message.session.start](message.md#imopenlinesmessagesessionstart) | Начинает новый диалог на основании сообщения |
| [imopenlines.session.head.vote](session.md#imopenlinessessionheadvote) | Ставит оценку работе сотрудника в диалоге |
| [imopenlines.session.history.get](session.md#imopenlinessessionhistoryget) | Получает сообщения чата и диалога |
| [imopenlines.session.intercept](session.md#imopenlinessessionintercept) | Забирает диалог у текущего оператора |
| [imopenlines.session.join](session.md#imopenlinessessionjoin) | Присоединяется к диалогу |
| [imopenlines.session.mode.pinAll](session.md#imopenlinessessionmodepinall) | Закрепляет все доступные диалоги за оператором |
| [imopenlines.session.mode.pin](session.md#imopenlinessessionmodepin) | Закрепляет или открепляет диалог |
| [imopenlines.session.mode.silent](session.md#imopenlinessessionmodesilent) | Переключает диалог в «скрытый» режим |
| [imopenlines.session.mode.unpinAll](session.md#imopenlinessessionmodeunpinall) | Открепляет все диалоги от оператора |
| [imopenlines.session.open](session.md#imopenlinessessionopen) | Получает чат по символьному коду |
| [imopenlines.session.start](session.md#imopenlinessessionstart) | Начинает новый диалог |

## Обработка ошибок

| Статус | Код | Описание |
|--------|-----|----------|
| 400 | `CHAT_ID` | Указан некорректный идентификатор чата |
| 400 | `CHAT_TYPE` | Указанный чат не является открытой линией |
| 400 | `ACCESS_DENIED` | Недостаточно прав на диалог |
| 400 | `CONFIG_ID_EMPTY` | Параметр `CONFIG_ID` не передан или некорректен |
| 403 | `CONFIG_WRONG_USER_PERMISSION` | Недостаточно прав для изменения/удаления линии |
| 400 | `MISSING_REQUIRED_PARAM` | Не переданы обязательные параметры |

Общие ошибки: см. [Обработка ошибок](../common/errors.md)
