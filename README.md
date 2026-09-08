# OpenCode Mobile

> Run your AI coding assistant from your phone.

OpenCode Mobile is a native Flutter mobile client for
[opencode](https://opencode.ai), the open-source AI coding assistant.
It connects to your own private server through an encrypted SSH tunnel —
no terminal emulator hacks, no third-party cloud. Review code, chat with
agents, approve tool calls and track token costs from anywhere: on the
metro, in a café, on the couch.

## Features

### Connection & security

- **SSH tunnel** — password and PEM key authentication, local port
  forwarding over `dartssh2`
- **Secure local storage** — server passwords and private keys encrypted
  with Android Keystore, never stored in plain text
- **Zero privacy leak** — the whole AI session runs on your own server;
  the app never talks to third-party services

### Immersive AI conversation

- **SSE streaming** — typewriter-style rendering of AI thinking and
  replies, automatic reconnection on network drops
- **Dark mode by design** — a deep, high-contrast theme built for long
  coding sessions
- **Markdown & syntax highlighting** — full Markdown rendering with
  multi-language highlighting
- **Multi-model & multi-mode** — dynamically lists the models available on
  your server; switch between `plan` and `build` modes anytime

### Deep integration with opencode

- **Tool execution cards** — when the agent runs `bash`, `read_file`,
  `write_file`, `webfetch` and friends, results render as collapsible
  cards with commands and output
- **Native permission interception** — replaces the agent's own security
  policy: dangerous commands or external file writes trigger a native
  bottom-sheet asking **Allow once / Always allow / Deny**
- **Question sheet** — handles single- and multi-choice questions the
  agent asks, right from your phone
- **Token & cost tracking** — per-session token consumption and estimated
  spend, in a monospace, geek-friendly layout

## How it works

```
📱 Phone (Flutter native UI)
  │
  ├─ 1. SSH connect (port 22)
  ├─ 2. Remote exec: opencode serve --port 4096
  ├─ 3. SSH local port forwarding (localhost:14096 -> remote:4096)
  │
☁️ Your server
  │
  └─ 4. HTTP / SSE over the native OpenAPI protocol (no terminal parsing)
```

## Quick start

**Prerequisite** — install opencode on your server:

```bash
curl -fsSL https://opencode.ai/install | sh
```

**Get the app:**

- Download the latest APK from
  [Releases](https://github.com/Zhucan123/opencode-app/releases), or
- Build it yourself and grab the artifact from
  [Actions](https://github.com/Zhucan123/opencode-app/actions)

**Use it:**

1. Tap **+** on the home screen to add a server
2. Enter host IP, SSH port, username and credentials (optional working
   directory)
3. Tap the card to connect — the tunnel and opencode start automatically
4. Start coding from your pocket

## Build from source

Requirements: Flutter 3.24+, Android SDK.

```bash
git clone https://github.com/Zhucan123/opencode-app.git
cd opencode-app
flutter pub get
flutter run            # with a device or Android emulator attached
flutter build apk --release
```

## Privacy

No personal data is collected. All sessions and credentials stay between
your phone and the server you configure. See the [privacy policy](https://zhucan.cloud/privacy.html).

## License

MIT License — self-host it, fork it, improve it.
