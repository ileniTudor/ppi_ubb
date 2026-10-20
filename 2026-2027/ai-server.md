# AI Server for PPI Teams

The faculty runs an open language model for your projects: **gpt-oss-20b** (OpenAI, open weights), on a university server.
It is free, it speaks the same protocol as the OpenAI API, and your data stays inside the faculty.
You can use it from home while you develop, and from the server when you deploy.

---

## 1. Connect to the faculty VPN

The server is only reachable through the faculty VPN (WireGuard).

1. Open [**https://www.cs.ubbcluj.ro/vpn/**](https://www.cs.ubbcluj.ro/vpn/) and click **Sign in with Microsoft**, with your university account.
2. Generate and download your WireGuard configuration file.
3. Install **WireGuard** from [wireguard.com/install](https://www.wireguard.com/install/) (Windows, macOS, Linux, Android, iOS).
4. In WireGuard: **Import tunnel(s) from file**, choose the downloaded file, then click **Activate**.

> The configuration file is personal. Do not share it and do not commit it to git.

Check that the VPN works (it should answer `{"status":"ok"}`):

```bash
curl http://172.30.249.193:8080/llm/health
```

## 2. Get your team's API key

Each team has **one API key**. One member of the team asks the professor for it in a **private message on MS Teams**, with the team number (e.g. *Echipa 7*).

The key is a password:
* Keep it in an **environment variable** or in a `.env` file listed in `.gitignore`.
* **Never** commit it to git and **never** put it in frontend code (anyone can read it in the browser).
* Do not share it with other teams.
* If it leaks, ask for a new one. The old key is disabled.

## 3. Call the model

| | |
|---|---|
| **Base URL** | `http://172.30.249.193:8080/llm/v1` |
| **Model** | `gpt-oss-20b` |
| **Protocol** | OpenAI Chat Completions (any OpenAI library works) |
| **Authentication** | header `Authorization: Bearer <your team key>` |

### Quick test (terminal)

```bash
curl http://172.30.249.193:8080/llm/v1/chat/completions \
  -H "Authorization: Bearer $LLM_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model": "gpt-oss-20b", "messages": [{"role": "user", "content": "Say hello in Romanian"}]}'
```

### Python

```bash
pip install openai python-dotenv
```

`.env` (add `.env` to `.gitignore`):

```
LLM_BASE_URL=http://172.30.249.193:8080/llm/v1
LLM_API_KEY=ppi-teamX-...
LLM_MODEL=gpt-oss-20b
```

```python
import os
from dotenv import load_dotenv
from openai import OpenAI

load_dotenv()
client = OpenAI(base_url=os.environ["LLM_BASE_URL"], api_key=os.environ["LLM_API_KEY"])

response = client.chat.completions.create(
    model=os.environ["LLM_MODEL"],
    messages=[
        {"role": "system", "content": "You are a helpful assistant. Answer briefly."},
        {"role": "user", "content": "What is a walking skeleton in software?"},
    ],
    timeout=120,
)
print(response.choices[0].message.content)
```

### JavaScript / TypeScript (Node.js backend)

```bash
npm install openai
```

```javascript
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: process.env.LLM_BASE_URL,
  apiKey: process.env.LLM_API_KEY,
});

const response = await client.chat.completions.create({
  model: process.env.LLM_MODEL,
  messages: [{ role: "user", content: "What is a walking skeleton in software?" }],
});
console.log(response.choices[0].message.content);
```

### Streaming (show the answer as it is written)

```python
stream = client.chat.completions.create(
    model=os.environ["LLM_MODEL"],
    messages=[{"role": "user", "content": "Explain RAG in three sentences."}],
    stream=True,
)
for chunk in stream:
    print(chunk.choices[0].delta.content or "", end="", flush=True)
```

### JSON answers

Ask for JSON in the prompt and add `response_format={"type": "json_object"}`; then read it with `json.loads(...)`.

### More reasoning

The model thinks briefly before it answers (`reasoning_effort: low` by default, which is faster).
For harder questions, ask for more:

```python
client.chat.completions.create(..., extra_body={"chat_template_kwargs": {"reasoning_effort": "medium"}})
```

Because the code only reads `LLM_BASE_URL`, `LLM_API_KEY` and `LLM_MODEL`, you can switch to another provider (or to a local model with Ollama) by changing the `.env` file, without touching the code.

## 4. What to expect

The model runs on CPUs, shared by all teams.

* **Speed:** about 40 tokens/s when you are alone, about 15 tokens/s each when 4 requests run at the same time.
* **Long prompts are slow:** the server reads about 150–190 tokens/s, so a 3,000-token prompt waits about 20 s before the answer starts. Keep prompts short; for RAG, send a few relevant chunks, not whole documents.
* **4 requests at a time.** Others wait in a queue (they do not fail).
* **Context:** about 16,000 tokens per request (prompt + answer).
* **Text only:** no images or audio.
* **Limit:** about 60 requests per minute from the same IP address.
* Use **streaming** and a **timeout** (e.g. 120 s), and show a waiting and an error state in your UI (Lab 2).

## 5. Rules

* Use it only for your PPI project.
* Use public, synthetic or anonymised data. No real patient data.
* Large batch jobs (thousands of requests) slow down every team: ask the professor first.
* The server may restart now and then. If it does not answer for a long time, tell the professor on MS Teams.
