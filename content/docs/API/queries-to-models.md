---
title: "[ POST ] Chat Completion - Запрос к модели"
type: docs
weight: 1
---

``` text
POST /chat/completions
```

Генерирует ответ модели на основе переданного диалога.

## Заголовки
- `Authorization: Bearer YOUR_API_KEY` — ваш API-ключ  
- `Content-Type: application/json`

## Параметры запроса

| Параметр | Тип | Обязательный | Описание |
|----------|-----|--------------|-----------|
| `model` | string | Да | ID модели |
| `messages` | array | Да | Массив сообщений |
| `temperature` | number | Нет | Креативность ответов (0.0-2.0) |
| `max_tokens` | number | Нет | Максимальная длина ответа |
| `stream` | boolean | Нет | Потоковый режим ответа |
| `functions` | array | Нет | Описание доступных функций |
| `function_call` | string | Нет | Принудительный вызов функции |
| `n` | number | Нет | Количество вариантов ответа |
| `presence_penalty` | number | Нет | Штраф за повторение тем (-2.0 до 2.0) |
| `frequency_penalty` | number | Нет | Штраф за повторение слов (-2.0 до 2.0) |
| `top_p` | number | Нет | Nucleus sampling (0.0-1.0) |
| `user` | string | Нет | ID пользователя для логирования |

## Пример запроса

```json
{
  "model": "gemini-2.5-flash",
  "messages": [
    {
      "role": "system",
      "content": "Ты - эксперт Python"
    },
    {
      "role": "user",
      "content": "Как создать виртуальное окружение?"
    }
  ],
  "temperature": 0.7,
  "max_tokens": 150
}
```

## Пример ответа

```json
{
  "choices": [
    {
      "message": {
        "content": "Для создания виртуального окружения используйте команду:\n\npython -m venv myenv",
        "role": "assistant"
      },
      "finish_reason": "stop",
      "index": 0
    }
  ],
  "created": 1692913639,
  "model": "gemini-2.5-flash",
  "usage": {
    "prompt_tokens": 20,
    "completion_tokens": 15,
    "total_tokens": 35
  }
}
```

## Статус-коды

- `200 [OK]`
- `400 [Bad Request]`
- `401 [Unauthorized]`
- `403 [Forbidden]`
- `429 [Too Many Requests]`
- `500 [Internal Server Error]`