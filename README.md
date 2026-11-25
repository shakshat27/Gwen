# G.W.E.N.

**Genius Woman for Everyday Needs**: a private study assistant that runs entirely on your own machine with local LLMs through Ollama.

<!-- screenshot: docs/chat.png -->

## Features

- Chat UI with **streamed responses** (Server-Sent Events), rendered as Markdown
- Model switcher: custom `gwen` model, Qwen2 0.5B or DeepSeek Coder
- Reads answers aloud with the browser's speech synthesis
- No cloud API: prompts never leave the computer

## How it works

```
Browser (index.html) ──EventSource /chat?message=…&model=…──► Flask (app.py)
                                                              │ streams POST /api/chat
                                                              ▼
                                                    Ollama (localhost:11434)
```

`app.py` adds a system prompt, forwards the message to Ollama with streaming enabled and relays each token chunk back to the page as an SSE event.

## Tech stack

Python · Flask · Ollama · JavaScript · Server-Sent Events · marked.js · Web Speech API

## Run

```bash
ollama pull qwen2:0.5b          # and/or deepseek-coder
pip install flask requests
python app.py                   # http://127.0.0.1:5000
```
