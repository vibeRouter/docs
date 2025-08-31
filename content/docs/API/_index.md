---
title: API Reference
type: docs
sidebar:
  open: true
weight: 50
---

## Обзор

VibeRouter предоставляет REST API для взаимодействия с различными языковыми моделями. API построено с учетом современных стандартов и практик разработки.

## Базовая информация

- **Base URL**: `https://api.viberouter.dev/v1`
- **Формат данных**: JSON
- **Аутентификация**: Bearer token
- **Версионирование**: через URL path

## Эндпоинты

### Chat Completions API

[Запросы к моделям](/docs/api/queries-to-models)
- `POST /chat/completions`
- Создание диалога с моделью
- Поддержка streaming режима
- Функции (function calling)
- Управление контекстом

### Models API

[Список моделей](/docs/api/list-of-models)
- `GET /models`
- Получение списка доступных моделей
- Информация о возможностях
- Статус доступности

## Аутентификация

Все запросы должны содержать заголовок:
```text
Authorization: Bearer YOUR_API_KEY
```

API ключ можно получить в [личном кабинете](https://viberouter.dev/dashboard/api-keys).

## Обработка ошибок

### Формат ошибок
```json
{
  "error": "string"
}
```

### Общие коды ошибок

#### 400 Bad Request
- `invalid_request`: Некорректные параметры
- `invalid_model`: Модель не существует
- `context_length_exceeded`: Превышен размер контекста
- `content_filter`: Контент не прошел фильтрацию

#### 401 Unauthorized
- `invalid_api_key`: Неверный API ключ
- `expired_api_key`: Ключ истек
- `account_not_active`: Аккаунт не активирован

#### 429 Too Many Requests
- `rate_limit_exceeded`: Превышен лимит запросов
- `quota_exceeded`: Превышена квота
- `concurrent_requests`: Превышен лимит параллельных запросов

#### 500 Internal Server Error
- `server_error`: Ошибка сервера
- `model_error`: Ошибка модели
- `timeout`: Таймаут

<!-- 
## Rate Limiting

API использует два типа ограничений:
1. Запросы в минуту (RPM)
2. Токены в минуту (TPM)

### Заголовки rate limit
- `X-RateLimit-Limit`: Максимум запросов
- `X-RateLimit-Remaining`: Осталось запросов
- `X-RateLimit-Reset`: Время сброса (Unix timestamp)

-->

## Streaming

Для получения ответов в реальном времени используйте параметр `stream: true`. Ответ приходит в формате server-sent events (SSE). Более подробно в разделе [параметров запроса к моделям](/docs/api/queries-to-models/#параметры-запроса).

## SDK и библиотеки

Примеры использования API в разных языках программирования доступны в разделе [примеров использования](/docs/examples).