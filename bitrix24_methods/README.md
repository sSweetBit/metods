# Документация по методам Bitrix24 REST API

## Оглавление

### Общие разделы

- [Обработка ошибок](common/errors.md)
- [Форматы запросов и ответов](common/formats.md)
- [Проверка методов](method.md) — `method.get`

### Группы методов

#### im (Внутренний мессенджер)

**Пользователи:**
- [im.user.get](im/user.md#imuserget) — Получить данные о пользователе
- [im.user.list.get](im/user.md#imuserlistget) — Получить данные о списке пользователей
- [im.user.status.get](im/user.md#imuserstatusget) — Получить статус пользователя
- [im.user.status.idle.start](im/user.md#imuserstatusidlestart) — Включить автостатус «Отошел»
- [im.user.status.idle.end](im/user.md#imuserstatusidleend) — Выключить автостатус «Отошел»

**Чаты:**
- [im.recent.get](im/recent.md#imrecentget) — Получить сокращенный список последних чатов
- [im.recent.list](im/recent.md#imrecentlist) — Получить список чатов (с пагинацией)
- [im.recent.pin](im/recent.md#imrecentpin) — Закрепить чат вверху списка
- [im.recent.hide](im/recent.md#imrecenthide) — Удалить чат из списка последних
- [im.recent.unread](im/recent.md#imrecentunread) — Установить/снять метку «прочитано»

**Подразделения:**
- [im.department.get](im/department.md#imdepartmentget) — Получить информацию о подразделении
- [im.department.colleagues.list](im/department.md#imdepartmentcolleagueslist) — Получить список коллег
- [im.department.managers.get](im/department.md#imdepartmentmanagersget) — Получить список руководителей
- [im.department.employees.get](im/department.md#imdepartmentemployeesget) — Получить список сотрудников

#### imconnector (Пользовательские коннекторы)

- [Обзор методов](imconnector/README.md)

**Регистрация и управление:**
- [imconnector.register](imconnector/register.md#imconnectorregister) — Зарегистрировать коннектор
- [imconnector.unregister](imconnector/unregister.md#imconnectorunregister) — Отменить регистрацию
- [imconnector.list](imconnector/connector.md#imconnectorlist) — Получить список коннекторов
- [imconnector.activate](imconnector/activate.md#imconnectoractivate) — Активировать/деактивировать
- [imconnector.status](imconnector/status.md#imconnectorstatus) — Получить статус коннектора
- [imconnector.send.status.delivery](imconnector/status.md#imconnectorsendstatusdelivery) — Обновить статус «доставлено»
- [imconnector.connector.data.set](imconnector/connector.md#imconnectorconnectordataset) — Установить настройки канала

**Чаты:**
- [imconnector.chat.name.set](imconnector/chat.md#imconnectorchatnameset) — Установить имя чата

**Сообщения:**
- [imconnector.send.messages](imconnector/send.md#imconnectorsendmessages) — Отправить сообщения
- [imconnector.update.messages](imconnector/send.md#imconnectorupdatemessages) — Изменить сообщения
- [imconnector.delete.messages](imconnector/send.md#imconnectordeletemessages) — Удалить сообщения

#### imopenlines (Открытые линии)

- [Обзор методов](imopenlines/README.md)

**Конфигурация:**
- [imopenlines.config.add](imopenlines/config.md#imopenlinesconfigadd) — Добавить открытую линию
- [imopenlines.config.get](imopenlines/config.md#imopenlinesconfigget) — Получить настройки линии
- [imopenlines.config.list.get](imopenlines/config.md#imopenlinesconfiglistget) — Получить список линий
- [imopenlines.config.update](imopenlines/config.md#imopenlinesconfigupdate) — Изменить линию
- [imopenlines.config.delete](imopenlines/config.md#imopenlinesconfigdelete) — Удалить линию
- [imopenlines.config.path.get](imopenlines/config.md#imopenlinesconfigpathget) — Получить ссылку на публичную страницу
- [imopenlines.network.join](imopenlines/network.md#imopenlinesnetworkjoin) — Подключить внешнюю линию
- [imopenlines.revision.get](imopenlines/revision.md#imopenlinesrevisionget) — Получить информацию о ревизиях API

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

---

*Документ сгенерирован для использования с нейронной сетью. При добавлении новых методов информация о повторяющихся разделах (например, обработка ошибок) ссылается на соответствующие общие разделы.*
