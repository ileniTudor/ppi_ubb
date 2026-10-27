# LLMHub: AI Models Hosted by the Faculty

**LLMHub** is the faculty's AI platform: [**https://www.cs.ubbcluj.ro/apps/llmhub**](https://www.cs.ubbcluj.ro/apps/llmhub)

It serves open models on faculty servers through **OpenAI-compatible endpoints**, so any OpenAI library (Python, JavaScript, Java…) works with it.
Use it from your laptop while you develop and from your app when you deploy.

---

## 1. Sign in

1. Open [https://www.cs.ubbcluj.ro/apps/llmhub](https://www.cs.ubbcluj.ro/apps/llmhub).
2. Click **Login with Microsoft** and sign in with your **institutional Microsoft account**.
3. Open the **Connect a client** page. It shows the base URL, how to get your API key, and ready-made configuration examples.

> Need access or help? Contact IT support: [ticket.cs.ubbcluj.ro](https://ticket.cs.ubbcluj.ro/)

## 2. Available models

For now there are **2 models**:

| | **GPT-OSS 20B** | **Qwen3.8 Flash Next** |
|---|---|---|
| **Model id** | `gpt-oss-20b` | `qwen3.8-flash-next` |
| **Input** | text | text **and images** |
| **Tool calling** | ✔ | ✔ |
| **Reasoning (thinking)** | low, medium, high | none, low, medium, high |
| **Context** | ~131,000 tokens | ~131,000 tokens |
| **Maximum answer** | ~4,100 tokens | ~16,400 tokens |

Which one to pick:
* **Qwen3.8 Flash Next** if your product works with images (X-rays, CT slices, photos, scanned documents) or needs long answers.
* **GPT-OSS 20B** for text: summaries, extracting fields into JSON, classification, answers from documents (RAG).
* Not sure? Run both on your test set (`evals/`, Lab 3) and keep the better one.

## 3. Call a model

Take the **base URL** and your **API key** from the **Connect a client** page and put them in a `.env` file (add `.env` to `.gitignore`):

```
LLM_BASE_URL=<base URL from "Connect a client">
LLM_API_KEY=<your API key>
LLM_MODEL=gpt-oss-20b
```

### Python

```bash
pip install openai python-dotenv
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
)
print(response.choices[0].message.content)
```

### JavaScript / TypeScript (Node.js backend)

```javascript
import OpenAI from "openai";

const client = new OpenAI({ baseURL: process.env.LLM_BASE_URL, apiKey: process.env.LLM_API_KEY });

const response = await client.chat.completions.create({
  model: process.env.LLM_MODEL,
  messages: [{ role: "user", content: "What is a walking skeleton in software?" }],
});
console.log(response.choices[0].message.content);
```

### Send an image (Qwen3.8 Flash Next)

```python
import base64

with open("scan.png", "rb") as f:
    image = base64.b64encode(f.read()).decode()

response = client.chat.completions.create(
    model="qwen3.8-flash-next",
    messages=[{
        "role": "user",
        "content": [
            {"type": "text", "text": "Describe what you see in this image."},
            {"type": "image_url", "image_url": {"url": f"data:image/png;base64,{image}"}},
        ],
    }],
)
print(response.choices[0].message.content)
```

### Streaming (show the answer while it is written)

```python
stream = client.chat.completions.create(
    model=os.environ["LLM_MODEL"],
    messages=[{"role": "user", "content": "Explain RAG in three sentences."}],
    stream=True,
)
for chunk in stream:
    print(chunk.choices[0].delta.content or "", end="", flush=True)
```

How to set the **thinking level** and use **tool calling**: see the examples on the **Connect a client** page.

Because the code only reads `LLM_BASE_URL`, `LLM_API_KEY` and `LLM_MODEL`, you can switch models or providers by changing the `.env` file, without touching the code.

## 4. Use it for coding (Qwen3.8 Flash Next)

The same endpoint can power your **coding assistant**. **Qwen3.8 Flash Next** is the model to pick for code: it supports tool calling (needed by coding agents) and long answers (about 16,400 tokens).

Any editor extension or terminal agent that accepts an **OpenAI-compatible endpoint** works. You need the same three values as in your app:

* **base URL** and **API key**: from the **Connect a client** page
* **model id**: `qwen3.8-flash-next`

> These settings were written from each tool's documentation. If one does not work with LLMHub, tell the professor on MS Teams. Tools change often: check their docs if a field has been renamed.

### Continue (VS Code / JetBrains)

In `config.yaml`:

```yaml
name: LLMHub
version: 1.0.0
schema: v1
models:
  - name: Qwen3.8 Flash Next
    provider: openai
    model: qwen3.8-flash-next
    apiBase: <base URL from "Connect a client">
    apiKey: <your API key>
    roles: [chat, edit, apply]
```

### Cline (VS Code)

In the Cline settings choose **API Provider: OpenAI Compatible**, then fill in **Base URL**, **API Key** and **Model ID** (`qwen3.8-flash-next`).

### OpenCode (terminal)

In `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "llmhub": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "LLMHub",
      "options": { "baseURL": "<base URL>", "apiKey": "{env:LLM_API_KEY}" },
      "models": { "qwen3.8-flash-next": { "name": "Qwen3.8 Flash Next" } }
    }
  }
}
```

### Aider (terminal)

```bash
export OPENAI_API_BASE=<base URL>
export OPENAI_API_KEY=<your API key>
aider --model openai/qwen3.8-flash-next
```

### Good habits when AI writes the code

* Give it your `SPECS.md` first and ask it to work task by task.
* Run the code, read the diff and test it before you commit. Anyone in the team may be asked to explain any part of the code.
* The API key stays in the tool's settings or an environment variable. Never commit it, and do not paste secrets or real patient data into the chat.

## 5. Rules

* Your API key is a password: keep it in an environment variable or `.env`, **never** in git and **never** in frontend code (anyone can read it in the browser). Do not share it.
* Use it for your PPI project.
* Use public, synthetic or anonymised data. **No real patient data.**
* The models are shared by all students of the faculty: avoid large batch jobs (thousands of requests) and keep prompts reasonably short.
* Show a waiting and an error state in your UI, and set a timeout (Lab 2).
