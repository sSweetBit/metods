# Документация по методам Bitrix24 REST API

## Оглавление

### Общие разделы

- [Обработка ошибок](common/errors.md)
- [Форматы запросов и ответов](common/formats.md)

### Группы методов

#### imopenlines (Открытые линии)

**Операторы:**
- [imopenlines.operator.answer](imopenlines/operator.md#imopenlinesoperatoranswer) — Забрать диалог себе
- [imopenlines.operator.skip](imopenlines/operator.md#imopenlinesoperatorskip) — Пропустить диалог
- [imopenlines.operator.spam](imopenlines/operator.md#imopenlinesoperatorspam) — Отметить как спам
- [imopenlines.operator.transfer](imopenlines/operator.md#imopenlinesoperatortransfer) — Передать другому оператору
- [imopenlines.operator.finish](imopenlines/operator.md#imopenlinesoperatorfinish) — Завершить свой диалог
- [imopenlines.operator.another.finish](imopenlines/operator.md#imopenlinesoperatoranotherfinish) — Завершить диалог другого оператора

**Сессии:**
- [imopenlines.session.intercept](imopenlines/session.md#imopenlinessessionintercept) — Забрать диалог у текущего оператора
- [imopenlines.session.open](imopenlines/session.md#imopenlinessessionopen) — Получить чат по коду пользователя
- [imopenlines.session.join](imopenlines/session.md#imopenlinessessionjoin) — Присоединиться к диалогу
- [imopenlines.session.start](imopenlines/session.md#imopenlinessessionstart) — Начать новый диалог
- [imopenlines.session.history.get](imopenlines/session.md#imopenlinessessionhistoryget) — Получить историю сообщений
- [imopenlines.session.mode.silent](imopenlines/session.md#imopenlinessessionmodesilent) — Скрытый режим
- [imopenlines.session.mode.pin](imopenlines/session.md#imopenlinessessionmodepin) — Закрепить/открепить диалог
- [imopenlines.session.mode.pinAll](imopenlines/session.md#imopenlinessessionmodepinall) — Закрепить все диалоги
- [imopenlines.session.mode.unpinAll](imopenlines/session.md#imopenlinessessionmodeunpinall) — Открепить все диалоги
- [imopenlines.session.head.vote](imopenlines/session.md#imopenlinessessionheadvote) — Оценка работы сотрудника

**Боты:**
- [imopenlines.bot.session.operator](imopenlines/bot.md#imopenlinesbotsessionoperator) — Переключить на оператора
- [imopenlines.bot.session.message.send](imopenlines/bot.md#imopenlinesbotsessionmessagesend) — Отправить авто-сообщение
- [imopenlines.bot.session.transfer](imopenlines/bot.md#imopenlinesbotsessiontransfer) — Перевести на оператора/очередь
- [imopenlines.bot.session.finish](imopenlines/bot.md#imopenlinesbotsessionfinish) — Завершить диалог

**Конфигурация:**
- [imopenlines.config.add](imopenlines/config.md#imopenlinesconfigadd) — Добавить открытую линию
- [imopenlines.config.get](imopenlines/config.md#imopenlinesconfigget) — Получить настройки линии
- [imopenlines.config.list.get](imopenlines/config.md#imopenlinesconfiglistget) — Получить список линий
- [imopenlines.config.update](imopenlines/config.md#imopenlinesconfigupdate) — Изменить линию
- [imopenlines.config.delete](imopenlines/config.md#imopenlinesconfigdelete) — Удалить линию
- [imopenlines.config.path.get](imopenlines/config.md#imopenlinesconfigpathget) — Получить ссылку на публичную страницу

**CRM:**
- [imopenlines.crm.chat.get](imopenlines/crm.md#imopenlinescrmchatget) — Получить чаты для объекта CRM
- [imopenlines.crm.chat.getLastId](imopenlines/crm.md#imopenlinescrmchatgetlastid) — Получить ID последнего чата
- [imopenlines.crm.chat.user.add](imopenlines/crm.md#imopenlinescrmchatuseradd) — Добавить пользователя в чат
- [imopenlines.crm.chat.user.delete](imopenlines/crm.md#imopenlinescrmchatuserdelete) — Удалить пользователя из чата
- [imopenlines.crm.message.add](imopenlines/crm.md#imopenlinescrmmessageadd) — Отправить сообщение в чат
- [imopenlines.crm.lead.create](imopenlines/crm.md#imopenlinescrmleadcreate) — Создать лид

**Network:**
- [imopenlines.network.join](imopenlines/network.md#imopenlinesnetworkjoin) — Подключить внешнюю линию
- [imopenlines.network.message.add](imopenlines/network.md#imopenlinesnetworkmessageadd) — Отправить сообщение

**Сообщения:**
- [imopenlines.message.session.start](imopenlines/message.md#imopenlinesmessagesessionstart) — Начать диалог на основании сообщения
- [imopenlines.message.quick.save](imopenlines/message.md#imopenlinesmessagequicksave) — Сохранить как быстрый ответ

**Диалоги:**
- [imopenlines.dialog.get](imopenlines/dialog.md#imopenlinesdialogget) — Получить информацию о диалоге

**Системные:**
- [imopenlines.revision.get](imopenlines/revision.md#imopenlinesrevisionget) — Получить информацию о ревизиях API

---

*Документ сгенерирован для использования с нейронной сетью. При добавлении новых методов информация о повторяющихся разделах (например, обработка ошибок) ссылается на соответствующие общие разделы.*
