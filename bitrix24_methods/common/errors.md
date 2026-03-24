# Обработка ошибок Bitrix24 REST API

> **Примечание:** Данный раздел описывает стандартные коды ошибок, которые могут возникнуть при вызове **любого** метода API. В описании конкретных методов ссылки на этот раздел приводятся без повторения информации.

## Формат ответа при ошибке

| Название | Тип | Описание |
|----------|-----|----------|
| `error` | string | Строковый код ошибки (цифры, латинские буквы, знак подчеркивания) |
| `error_description` | string | Текстовое описание ошибки (не предназначено для показа конечному пользователю) |

## Статусы и коды системных ошибок

| Статус | Код | Текст ошибки | Описание |
|--------|-----|--------------|----------|
| 500 | `INTERNAL_SERVER_ERROR` | Internal server error | Возникла внутренняя ошибка сервера |
| 500 | `ERROR_UNEXPECTED_ANSWER` | Server returned an unexpected response | Возникла внутренняя ошибка сервера |
| 503 | `QUERY_LIMIT_EXCEEDED` | Too many requests | Превышен лимит на интенсивность запросов |
| 405 | `ERROR_BATCH_METHOD_NOT_ALLOWED` | Method is not allowed for batch usage | Метод не разрешён для вызова через batch |
| 400 | `ERROR_BATCH_LENGTH_EXCEEDED` | Max batch length exceeded | Превышена максимальная длина параметров batch |
| 401 | `NO_AUTH_FOUND` | Wrong authorization data | Неверный access-токен или код вебхука |
| 400 | `INVALID_REQUEST` | Https required | Требуется использование HTTPS |
| 503 | `OVERLOAD_LIMIT` | REST API is blocked due to overload | REST API заблокирован из-за перегрузки |
| 403 | `ACCESS_DENIED` | REST API is available only on commercial plans | REST API доступен только на коммерческих планах |
| 403 | `INVALID_CREDENTIALS` | Invalid request credentials | Недостаточно прав у пользователя |
| 404 | `ERROR_MANIFEST_IS_NOT_AVAILABLE` | Manifest is not available | Манифест недоступен |
| 403 | `insufficient_scope` | The request requires higher privileges | Запрос требует более высоких привилегий |
| 401 | `expired_token` | The access token provided has expired | Access-токен истёк |
| 403 | `user_access_error` | The user does not have access to the application | Пользователь не имеет доступа к приложению |
| 500 | `PORTAL_DELETED` | Portal was deleted | Публичная часть сайта закрыта |
