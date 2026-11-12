# Python Projects Suite

A production-ready collection of modular, standalone Python applications engineered with industry best practices, clean architecture, and robust error handling.

[![Python Version](https://img.shields.io/badge/Python-3.10%2B-blue.svg?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=for-the-badge)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey.svg?style=for-the-badge)](#-prerequisites--quick-start)
[![Code Style: Black](https://img.shields.io/badge/Code%20Style-Black-000000.svg?style=for-the-badge)](https://github.com/psf/black)
[![Contributions Welcome](https://img.shields.io/badge/Contributions-Welcome-brightgreen.svg?style=for-the-badge)](#-contributing)

---

## 📑 Table of Contents

- [Overview](#-overview)
- [Projects Matrix](#-projects-matrix)
- [Prerequisites & Quick Start](#-prerequisites--quick-start)
- [Projects](#-projects)
  - [1. Aura - Intelligent Voice Assistant](#1--aura---intelligent-voice-assistant)
  - [2. Random Password Generator CLI](#2--random-password-generator-cli)
  - [3. Real-Time Multi-Client Chat](#3--real-time-multi-client-chat)
- [Repository Structure](#-repository-structure)
- [Troubleshooting & FAQ](#-troubleshooting--faq)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🌟 Overview

This repository showcases three diverse, fully decoupled Python implementations spanning Natural Language Processing & Speech, CLI Security Utilities, and Low-Level Network Concurrency:

1. **Aura Voice Assistant:** Modular speech-to-text and natural language command executor with multi-modal fallback (voice/text/silent).
2. **Password Generator CLI:** Cryptographically sound, rule-enforced password generation utility with interactive terminal interface.
3. **Multi-Client Chat System:** Thread-safe TCP socket server and interactive client supporting real-time concurrent messaging.

---

## 📊 Projects Matrix

| Project | Directory | Focus Domain | Key Technologies | External Dependencies |
| :--- | :--- | :--- | :--- | :--- |
| **Aura Voice Assistant** | [`voice-assistant/`](voice-assistant/) | Voice Automation & NLU | `SpeechRecognition`, `pyttsx3`, `requests`, `nltk` | Yes (`requirements.txt`) |
| **Password Generator** | [`password-generator/`](password-generator/) | Security & CLI Utility | `random`, `string`, `sys` | None (Standard Library) |
| **Real-Time Chat** | [`chat-application/`](chat-application/) | Networking & Concurrency | `socket`, `threading`, `datetime` | None (Standard Library) |

---

## 💻 Prerequisites & Quick Start

Ensure **Python 3.10 or higher** is installed and accessible from your terminal:

```bash
# Verify Python version
python --version   # or: py --version / python3 --version
```

### Clone the Repository

```bash
git clone https://github.com/<your-username>/python-projects.git
cd python-projects
```

---

## 🚀 Projects

### 1. 🎙️ Aura - Intelligent Voice Assistant

> **Directory:** [`voice-assistant/`](voice-assistant/)

A modular, extensible voice assistant that processes natural language voice or text commands, interacts via speech synthesis, and automates common daily tasks.

#### Key Features
- **Dual Mode Operation:** Runs seamlessly in standard **Voice Mode** (microphone input) or **Interactive Text Mode** (`--text`) for silent/headless environments.
- **Speech Synthesis & Mute Option:** Windows SAPI5 / cross-platform text-to-speech engine with silence support (`--mute`).
- **Natural Language Parsing:** Intent detection powered by token analysis and rule-based NLU heuristics.
- **Dynamic Capabilities:**
  - 🕒 Live time, date, and calendar reporting
  - 🌐 Google Search queries and instant Wikipedia summary retrieval
  - 🌦️ Real-time weather reporting via OpenWeatherMap (with auto fallback to `wttr.in`)
  - ⏰ Background non-blocking timers and audible reminder alerts
  - 📧 Automated email dispatch via `smtplib` (includes safe mock mode by default)
  - ⚙️ User-defined custom command registry backed by persistent JSON (`custom_commands.json`)
  - 🧪 Automated feature tour via demo mode (`--demo`)

#### Setup & Execution

1. **Navigate to the module directory:**
   ```bash
   cd voice-assistant
   ```

2. **Create and activate a virtual environment:**
   - **Windows (PowerShell):**
     ```powershell
     python -m venv venv
     .\venv\Scripts\Activate.ps1
     ```
   - **Windows (Command Prompt):**
     ```cmd
     python -m venv venv
     venv\Scripts\activate.bat
     ```
   - **macOS / Linux:**
     ```bash
     python3 -m venv venv
     source venv/bin/activate
     ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Environment Configuration (Optional):**
   Copy the example environment configuration:
   ```bash
   # Windows (CMD / PowerShell)
   copy .env.example .env

   # Linux / macOS
   cp .env.example .env
   ```
   *Modify `.env` to configure assistant name, custom OpenWeatherMap API keys, or SMTP email parameters. By default, `MOCK_EMAIL=true` ensures safe execution without exposing real credentials.*

5. **Run the Assistant:**
   ```bash
   # Standard Voice Mode (Speak into your microphone)
   python main.py

   # Interactive Text Mode (Type commands in terminal)
   python main.py --text

   # Silent Mode (Text input and terminal output only, no audio)
   python main.py --text --mute

   # Automated Feature Demo
   python main.py --demo
   ```

6. **Run Test Suite:**
   ```bash
   python -m unittest discover tests
   ```

---

### 2. 🔐 Random Password Generator CLI

> **Directory:** [`password-generator/`](password-generator/)

A secure command-line tool for generating customizable passwords adhering to complexity constraints and cybersecurity recommendations.

#### Key Features
- **Strict Complexity Enforcement:** Requires at least 2 distinct character categories and enforces an 8-character minimum length.
- **Customizable Character Sets:** Granular control over inclusion of Uppercase (`A-Z`), Lowercase (`a-z`), Digits (`0-9`), and Symbols (`!@#$%...`).
- **Guaranteed Entropy:** Guarantees minimum representation of each selected character category before applying cryptographic shuffling.
- **Continuous Session:** Allows repeated password generation within a single interactive session.
- **Zero External Dependencies:** Implemented purely with Python standard libraries (`random`, `string`, `sys`).

#### Setup & Execution

1. **Navigate to the module directory:**
   ```bash
   cd password-generator
   ```

2. **Execute the generator:**
   ```bash
   python password_generator.py
   ```

3. **Sample Interactive Walkthrough:**
   ```text
   ==================================================
              RANDOM PASSWORD GENERATOR
   ==================================================
   Enter total password length (min: 8): 14
   Include Uppercase letters? (y/n): y
   Include Lowercase letters? (y/n): y
   Include Numbers? (y/n): y
   Include Special Symbols? (y/n): y

   --------------------------------------------------
   Generated Password:
     >>> k(cYwv8N|+VF9Q <<<
   Length: 14 characters
   --------------------------------------------------
   Generate another password? (y/n): n
   ```

---

### 3. 💬 Real-Time Multi-Client Chat

> **Directory:** [`chat-application/`](chat-application/)

A client-server messaging architecture built on low-level TCP sockets, enabling concurrent multi-user group chat in real-time.

#### Key Features
- **Concurrent Connection Handling:** Multi-threaded server assigns dedicated client listener threads for seamless bidirectional communication.
- **Real-Time Broadcast Engine:** Thread-safe relay mechanism delivers broadcast messages across all active sessions with low latency.
- **Graceful Lifecycle Management:** Detects disconnects, cleans up socket descriptors, and notifies remaining participants.
- **Timestamped Formatting:** Automatically prefixes broadcast communications with clean time indicators (`[HH:MM]`).
- **Standard Library Only:** Zero external dependencies; built using `socket`, `threading`, and `datetime`.

#### Multi-Terminal Execution Guide

Open at least two terminal windows to observe client-server communication:

#### Terminal 1 — Start Server
```bash
cd chat-application
python server.py
```
*Server binds to `127.0.0.1:5000` by default.*

#### Terminal 2 — Connect Client 1 (e.g., Alice)
```bash
cd chat-application
python client.py -u Alice
```

#### Terminal 3 — Connect Client 2 (e.g., Bob)
```bash
cd chat-application
python client.py -u Bob
```

#### Commands & Options
- **Exit Room:** Send `/quit` or press `Ctrl + C` to disconnect gracefully.
- **Custom Host & Port:**
  ```bash
  python server.py --host 0.0.0.0 --port 6000
  python client.py --host 127.0.0.1 --port 6000 -u Alice
  ```

---

## 📂 Repository Structure

```text
python-projects/
│
├── README.md                           # Master project documentation
│
├── voice-assistant/                    # Project 1: Intelligent Voice Assistant (Aura)
│   ├── assistant/                      # Modular assistant package
│   │   ├── __init__.py                 # Package initializer
│   │   ├── actions.py                  # Task handlers (weather, email, reminder, search)
│   │   ├── audio.py                    # C-level audio stream & stderr management
│   │   ├── config.py                   # Environment and settings parser
│   │   ├── custom_cmds.py              # Persistent custom command registry
│   │   ├── nlu.py                      # Rule-based Natural Language Understanding
│   │   └── speech.py                   # Speech-to-Text and Text-to-Speech engines
│   ├── tests/                          # Automated unit test suite
│   │   ├── __init__.py                 # Test package initializer
│   │   ├── test_actions.py             # Action execution unit tests
│   │   ├── test_custom_cmds.py         # Custom command persistence tests
│   │   └── test_nlu.py                 # NLU intent parsing tests
│   ├── custom_commands.json            # Dynamic user command registry
│   ├── .env.example                    # Template environment variable configuration
│   ├── requirements.txt                # External package dependencies
│   └── main.py                         # Voice Assistant CLI entry point
│
├── password-generator/                 # Project 2: Password Generator CLI
│   └── password_generator.py           # Interactive password generation script
│
└── chat-application/                   # Project 3: Real-Time Multi-Client Chat
    ├── server.py                       # Multi-threaded TCP broadcast server
    └── client.py                       # Interactive TCP chat client
```

---

## 🛠️ Troubleshooting & FAQ

| Problem | Root Cause | Recommended Fix |
| :--- | :--- | :--- |
| `python : The term 'python' is not recognized` | Python is not registered in system environment variables (`PATH`) | Re-run Python installer, select **Modify**, and check **"Add Python to PATH"**; or invoke via `py` on Windows / `python3` on Unix. |
| `PSSecurityException: File cannot be loaded` | PowerShell execution policy restricts running activation scripts | Run `Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned` in PowerShell. |
| `error: Microsoft Visual C++ 14.0 is required` | PyAudio wheel compilation triggered due to missing binary wheels | PyAudio provides pre-built wheels for Python 3.10-3.12 (64-bit). Alternatively, run the assistant in text mode: `python main.py --text`. |
| `OSError: [Errno 98/10048] Address already in use` | Another process is holding port `5000` | Start server on an alternate port: `python server.py --port 5050` and point clients accordingly: `python client.py --port 5050`. |
| Microphone fails to detect input | OS privacy policy prevents terminal microphone access | Check system Privacy & Security settings and ensure microphone access is granted for command-line tools / apps. |

---

## 🤝 Contributing

Contributions, issues, and feature suggestions are welcome!

1. **Fork** the repository
2. **Create** your feature branch (`git checkout -b feature/AmazingFeature`)
3. **Commit** your changes (`git commit -m 'feat: add AmazingFeature'`)
4. **Push** to the branch (`git push origin feature/AmazingFeature`)
5. **Open** a Pull Request

---

## 📄 License

This repository is licensed under the [MIT License](LICENSE). You are free to use, modify, and distribute this software in accordance with the license conditions.
