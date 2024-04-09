## help command to get supported models by local-ai:

```
curl 127.0.0.1:8080/v1/models | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   372  100   372    0     0   305k      0 --:--:-- --:--:-- --:--:--  363k
{
  "object": "list",
  "data": [
    {
      "id": "gpt4all-j",
      "object": "model"
    },
    {
      "id": "text-embedding-ada-002",
      "object": "model"
    },
    {
      "id": "whisper-1",
      "object": "model"
    },
    {
      "id": "stablediffusion",
      "object": "model"
    },
    {
      "id": "gpt-4-vision-preview",
      "object": "model"
    },
    {
      "id": "tts-1",
      "object": "model"
    },
    {
      "id": "gpt-4",
      "object": "model"
    },
    {
      "id": "ggml-gpt4all-j",
      "object": "model"
    },
    {
      "id": "yaml",
      "object": "model"
    }
  ]
}
```

## test model gpt4all-j
```
curl 127.0.0.1:8080/v1/chat/completions -H "Content-Type: application/json" -d '{ "model": "gpt4all-j",  "messages": [{"role": "user", "content": "How are you?"}], "temperature": 0.1 }' | jq

```

## logs from local-ai:
```
2:53AM INF Loading model 'ggml-gpt4all-j.bin' with backend gpt4all-j
```

## logs from client:
```
curl 127.0.0.1:8080/v1/chat/completions -H "Content-Type: application/json" -d '{ "model": "gpt4all-j",  "messages": [{"role": "user", "content": "How are you?"}], "temperature": 0.1 }' | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   423  100   319  100   104     17      5  0:00:20  0:00:18  0:00:02    79
{
  "created": 1712025900,
  "object": "chat.completion",
  "id": "99a5396c-ac68-40f2-9e8e-8ba135ebb09f",
  "model": "gpt4all-j",
  "choices": [
    {
      "index": 0,
      "finish_reason": "stop",
      "message": {
        "role": "assistant",
        "content": "I'm doing well, thank you. How about yourself?\n"
      }
    }
  ],
  "usage": {
    "prompt_tokens": 0,
    "completion_tokens": 0,
    "total_tokens": 0
  }
}
```

## ask to write a short story
```
curl 127.0.0.1:8080/v1/chat/completions -H "Content-Type: application/json" -d '{ "model": "gpt4all-j",  "messages": [{"role": "user", "content": "tell a story about candle for me, short in 100 words"}], "temperature": 0.1 }' | jq
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  1476  100  1332  100   144     23      2  0:01:12  0:00:56  0:00:16   295
{
  "created": 1712025900,
  "object": "chat.completion",
  "id": "99a5396c-ac68-40f2-9e8e-8ba135ebb09f",
  "model": "gpt4all-j",
  "choices": [
    {
      "index": 0,
      "finish_reason": "stop",
      "message": {
        "role": "assistant",
        "content": "Once upon a time, there was an old candle who lived in a small village. The villagers would often light the candle to keep warm during winter nights. The old candle would watch as the villagers went about their daily lives, but it longed for something more.\nThe old candle yearned to be seen, heard and appreciated. One day it decided to take matters into its own hands and started a campaign to become the most popular candle in town. The old candle started by spreading the word about its unique qualities and how it could bring warmth to anyone who used it.\nThe old candle's efforts paid off, and soon it became the most sought-after candle in town. The villagers would often come to the old candle's home and admire it, telling stories about how the old candle had brought them warmth and comfort during their darkest nights.\nThe old candle was overjoyed, and it continued to spread its light wherever possible. It had finally found the purpose it was meant to fulfill, and nothing could stop its journey towards becoming the most beloved candle in town."
      }
    }
  ],
  "usage": {
    "prompt_tokens": 0,
    "completion_tokens": 0,
    "total_tokens": 0
  }
}
```