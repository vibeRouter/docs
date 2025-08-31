---
title: Быстрый старт
next: API
---

## Начало работы

1. Зарегистрируйтесь на [VibeRouter](https://viberouter.dev) и подтвердите email
2. Перейдите в [Dashboard](https://viberouter.dev/dashboard/api-keys) для получения API ключа
3. Выберите подходящую модель на [странице моделей](https://viberouter.dev/models)

## API Ключ

В разделе [API Keys](https://viberouter.dev/dashboard/api-keys) вы найдете автоматически созданный API ключ. Для безопасности:

- Храните ключ только на сервере, не в клиентском коде
- При компрометации ключа сразу создайте новый через "О ключе" → "Обновить ключ"

## Примеры использования

### Python (используя OpenAI SDK)

```python
import openai

client = openai.OpenAI(
    api_key='YOUR_VIBEROUTER_API_KEY',
    base_url="https://api.vibeRouter.dev/v1"
)

completion = client.chat.completions.create(
    model="gemini-2.5-flash",
    messages=[
        {"role": "user", "content": "Hello world"}
    ]
)
print(completion.choices[0].message.content)
```

### JavaScript/Node.js

```javascript
const apiKey = 'YOUR_VIBEROUTER_API_KEY';
const apiUrl = 'https://api.vibeRouter.dev/v1/chat/completions';

async function getCompletion() {
  const response = await fetch(apiUrl, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${apiKey}`
    },
    body: JSON.stringify({
      model: 'gemini-2.5-flash',
      messages: [{ role: 'user', content: 'Hello world' }]
    })
  });

  const data = await response.json();
  console.log(data.choices[0].message.content);
}

getCompletion();
```

### Go

```go
package main

import (
    "bytes"
    "fmt"
    "io/ioutil"
    "net/http"
)

func main() {
    apiKey := "YOUR_VIBEROUTER_API_KEY"
    url := "https://api.vibeRouter.dev/v1/chat/completions"

    jsonData := []byte(`{
        "model": "gemini-2.5-flash",
        "messages": [{"role": "user", "content": "Hello world"}]
    }`)

    req, _ := http.NewRequest("POST", url, bytes.NewBuffer(jsonData))
    req.Header.Set("Authorization", "Bearer "+apiKey)
    req.Header.Set("Content-Type", "application/json")

    client := &http.Client{}
    resp, err := client.Do(req)
    if err != nil {
        panic(err)
    }
    defer resp.Body.Close()

    body, _ := ioutil.ReadAll(resp.Body)
    fmt.Println(string(body))
}
```

## Баланс и оплата

У платформы два типа баланса:

- **Основной баланс**: пополняется при оплате, доступны все модели
- **Бонусный баланс**: начисляется за регистрацию и рефералов, доступны базовые модели

При использовании сначала расходуется бонусный баланс (где применимо), затем основной.

[Подробнее о тарификации и способах оплаты →](https://viberouter.dev/support)
