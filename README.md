# Lakshya Project - Multi-Task Python Suite

Welcome to the **Lakshya Project** repository. This workspace contains three production-grade, standalone Python applications developed to meet beginner and advanced specifications.

All task folders have been renamed to their actual application names:

| Task | Original Folder | Renamed Folder | Application Name | Key Technologies | External Dependencies |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Task 1** | `task 1` | [`voice-assistant/`](voice-assistant/) | **Aura - Intelligent Voice Assistant** | `speech_recognition`, `pyttsx3`, `requests`, `nltk`, `smtplib` | Yes (`requirements.txt`) |
| **Task 2** | `task2` | [`password-generator/`](password-generator/) | **Random Password Generator CLI** | `random`, `string`, `sys` | None (Standard Library) |
| **Task 3** | `task3` | [`chat-application/`](chat-application/) | **Real-Time Multi-Client Chat** | `socket`, `threading`, `datetime` | None (Standard Library) |

---

## 💻 Windows Quick-Start Guide (Prerequisites)

This guide is optimized for **Windows 10 and Windows 11** using **Command Prompt (CMD)**, **PowerShell**, or **Windows Terminal**.

### 1. Verify Python Installation
Open **Command Prompt** or **PowerShell** and verify that Python 3.10+ is installed and registered in your system `PATH`:

```cmd
python --version
```
*(If `python` is not recognized, try `py --version`. Ensure **"Add python.exe to PATH"** was checked during Python installation).*

### 2. Enable PowerShell Script Execution (PowerShell Users Only)
If you plan to use PowerShell and virtual environments, ensure script execution is enabled:
```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

---

## 🎙️ Task 1: Intelligent Voice Assistant (`voice-assistant`)

### Overview
**Aura** is a modular Python voice assistant featuring:
- **Speech Recognition & Text-to-Speech:** Uses Google Speech Recognition (STT) and Windows native SAPI5 text-to-speech engine via `pyttsx3`.
- **Text & Mute Fallbacks:** Run fully in terminal text mode (`--text`) or mute voice audio (`--mute`).
- **Core Commands:** Conversational greetings, live time, date, and Google web searches.
- **Live Weather Updates:** Weather reports for any city using OpenWeatherMap or automatic wttr.in fallback.
- **Background Reminders:** Non-blocking countdown reminders with audible and visual alerts.
- **Email Sending:** Send emails using Python's `smtplib` (includes safe test/mock mode enabled by default).
- **Knowledge QA:** Wikipedia summary lookup for historical and technical questions.
- **Custom Commands:** Persistent JSON-backed custom command manager (`custom_commands.json`).
- **Automated Feature Demo:** Automated end-to-end demonstration mode (`--demo`).

---

### Windows Setup & Execution

#### Step 1: Open Terminal & Navigate to the Directory
In **Command Prompt** or **PowerShell**:
```cmd
cd voice-assistant
```

#### Step 2: Create and Activate Virtual Environment
- **Using Command Prompt (CMD):**
  ```cmd
  python -m venv venv
  venv\Scripts\activate.bat
  ```

- **Using PowerShell:**
  ```powershell
  python -m venv venv
  .\venv\Scripts\Activate.ps1
  ```

*(Your prompt will now show `(venv)` indicating the virtual environment is active).*

#### Step 3: Install Required Dependencies
```cmd
pip install -r requirements.txt
```

> [!TIP]
> **Windows PyAudio Installation Note:**
> On Windows, `pip install pyaudio` installs pre-compiled binary wheels out of the box for Python 3.10, 3.11, and 3.12. If you do not have a microphone connected or prefer typing, you can run the assistant anytime using `--text` mode without needing PyAudio or a microphone!

#### Step 4: Configure Environment Variables (Optional)
A `.env.example` file is included. Create your local `.env`:
- **Command Prompt:**
  ```cmd
  copy .env.example .env
  ```
- **PowerShell:**
  ```powershell
  Copy-Item .env.example .env
  ```
You can edit `.env` using Notepad (`notepad .env`) to set your assistant name, OpenWeatherMap API key, or SMTP email credentials. By default, `MOCK_EMAIL=true` is enabled so email testing is completely safe and requires no real credentials.

#### Step 5: Run the Assistant

- **Voice Mode (Default - Speak into microphone):**
  ```cmd
  python main.py
  ```

- **Interactive Text Mode (Recommended for testing or quiet environments):**
  ```cmd
  python main.py --text
  ```

- **Text Mode with Muted Speech (Silent Terminal Output):**
  ```cmd
  python main.py --text --mute
  ```

- **Automated End-to-End Demo (Runs all features automatically):**
  ```cmd
  python main.py --demo
  ```

#### Step 6: Run Unit Tests
```cmd
python -m unittest discover tests
```

---

### Example Voice / Text Prompts
- `"Hello"` / `"Hi Aura"`
- `"What time is it?"`
- `"What is today's date?"`
- `"Search for Alan Turing"`
- `"What is the weather in London?"` / `"Weather in Tokyo"`
- `"Remind me in 10 seconds to drink water"`
- `"Send an email to alex@example.com with subject Project Demo and body Hello world"`
- `"Who was Ada Lovelace?"`
- `"List custom commands"`
- `"Tell me a joke"`
- `"Goodbye"` / `"Exit"`

---

## 🔐 Task 2: Random Password Generator (`password-generator`)

### Overview
A robust, interactive command-line password generator that meets strict security and validation requirements:
- **Configurable Length:** Supports any password length (enforces a minimum of 8 characters).
- **Character Pool Selection:** Toggle uppercase (`A-Z`), lowercase (`a-z`), digits (`0-9`), and punctuation symbols (`!@#$%...`).
- **Strict Validation:** Requires at least 2 character types to ensure password strength.
- **Guaranteed Inclusion:** Ensures at least one character from each selected category is included, then shuffles characters randomly.
- **Looping CLI:** Generate multiple passwords in a single session without restarting.
- **Zero External Dependencies:** Built entirely with Python's built-in standard library (`random`, `string`, `sys`).

---

### Windows Setup & Execution

#### Step 1: Navigate to the Directory
In **Command Prompt** or **PowerShell**:
```cmd
cd password-generator
```

#### Step 2: Run the Script
No external libraries or virtual environment required! Simply run:
```cmd
python password_generator.py
```

#### Step 3: Interactive Walkthrough
1. Enter the desired password length (e.g., `16`).
2. Answer `y` or `n` to include:
   - Uppercase letters (`A-Z`)
   - Lowercase letters (`a-z`)
   - Numbers (`0-9`)
   - Special symbols (`!@#$%^&*...`)
3. The generated password will be displayed with length confirmation:
   ```text
   --------------------------------------------------
   Generated Password:
     >>> k(cYwv8N|+VF <<<
   Length: 12 characters
   --------------------------------------------------
   ```
4. Choose whether to generate another password or exit.

---

## 💬 Task 3: Real-Time Multi-Client Chat Application (`chat-application`)

### Overview
A real-time, multi-threaded client-server chat system using low-level TCP sockets:
- **Server (`server.py`):**
  - Listens for incoming TCP connections.
  - Handles concurrent clients using multi-threading (`threading.Thread`).
  - Broadcasts messages to all connected clients in real-time.
  - Automatically detects client disconnects and notifies peers.
  - Thread-safe client connection management with `threading.Lock`.
- **Client (`client.py`):**
  - Connects to the server over TCP.
  - Background worker thread listens for incoming messages without blocking user input.
  - Formats messages with clean `[HH:MM]` timestamps.
  - Graceful exit via `/quit` or `Ctrl + C`.
- **Zero External Dependencies:** Built entirely using Python standard libraries (`socket`, `threading`, `sys`, `argparse`, `datetime`).

---

### Windows Setup & Execution (Multi-Terminal Walkthrough)

To simulate a real-time chat room, open **at least 2 or 3 separate terminal windows** (Command Prompt, PowerShell, or Windows Terminal tabs).

#### Step 1: Start the Chat Server (Terminal 1)
```cmd
cd chat-application
python server.py
```
*Expected Server Output:*
```text
============================================================
           REAL-TIME CHAT SERVER (ACTIVE)
============================================================
Server listening on 127.0.0.1:5000
Press Ctrl+C to shut down the server safely.
============================================================
```

> [!NOTE]
> **Windows Defender Firewall Alert:**
> If Windows Firewall prompts a popup asking to allow Python network access, click **"Allow access"** for Private networks.

---

#### Step 2: Start Client 1 - Alice (Terminal 2)
Open a new terminal window:
```cmd
cd chat-application
python client.py -u Alice
```
*(Or run `python client.py` and enter your username when prompted).*

---

#### Step 3: Start Client 2 - Bob (Terminal 3)
Open another terminal window:
```cmd
cd chat-application
python client.py -u Bob
```

---

#### Step 4: Chat in Real-Time!
- In **Alice's window**, type: `Hello Bob!` and press **Enter**.
- In **Bob's window**, the message appears instantly:
  ```text
  [12:15] Alice: Hello Bob!
  ```
- In **Bob's window**, type: `Hey Alice! How are you?` and press **Enter**.
- Alice's window updates immediately with the response.

#### Step 5: Disconnect
To exit a client chat session cleanly:
- Type `/quit` and press **Enter**, or press `Ctrl + C`.
- The server and other connected clients will be notified that the user has left.

#### Custom Host and Port Configuration
By default, the server binds to `127.0.0.1:5000`. You can customize the port:
```cmd
python server.py --port 6000
python client.py -u Alice --port 6000
```

#### Optional: Local Area Network (LAN) Chat on Windows
To chat between two different computers connected to the same Wi-Fi router:
1. Find the host computer's IPv4 address by running `ipconfig` in Command Prompt (e.g., `192.168.1.50`).
2. On Host PC, run:
   ```cmd
   python server.py --host 0.0.0.0 --port 5000
   ```
3. On other PCs on the same Wi-Fi, run:
   ```cmd
   python client.py --host 192.168.1.50 --port 5000 -u YourName
   ```

---

## 🛠️ Windows Troubleshooting Guide

| Issue | Cause | Solution |
| :--- | :--- | :--- |
| `'python' is not recognized as an internal or external command` | Python was installed without checking "Add python.exe to PATH" | Re-run Python installer, choose "Modify", and check **"Add Python to environment variables"**; or use the Windows Python launcher `py`. |
| `File ... cannot be loaded because running scripts is disabled` | PowerShell default execution policy blocks virtual environment activation script | In PowerShell (as current user), run: `Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned` |
| `error: Microsoft Visual C++ 14.0 or greater is required` when installing PyAudio | No C++ compiler installed for PyAudio compilation from source | PyAudio wheels exist for Python 3.10-3.12. Ensure you have 64-bit Python, or simply run the assistant in text mode: `python main.py --text`. |
| `Address already in use` error in Chat Server | Another process is already using port 5000 | Specify an alternate port: `python server.py --port 5500` and `python client.py --port 5500`. |
| Microphone not capturing speech | Windows microphone privacy permission disabled | Open **Windows Settings > Privacy & Security > Microphone**, enable **"Let apps access your microphone"**, and ensure desktop apps have access. |

---

## 📂 Project Structure

```text
lakshya project/
│
├── README.md                           # Main documentation and Windows guide
│
├── voice-assistant/                    # Task 1: Intelligent Voice Assistant (Aura)
│   ├── assistant/                      # Core assistant package
│   │   ├── actions.py                  # Action execution (weather, reminders, email, search)
│   │   ├── audio.py                    # C-level stderr audio suppression
│   │   ├── config.py                   # Configuration and environment loader
│   │   ├── custom_cmds.py              # Persistent custom commands management
│   │   ├── nlu.py                      # Natural language understanding and intent parsing
│   │   └── speech.py                   # Speech-to-text (STT) and text-to-speech (TTS)
│   ├── tests/                          # Automated unit test suite
│   │   ├── test_actions.py             # Action handler unit tests
│   │   ├── test_custom_cmds.py         # Custom command storage tests
│   │   └── test_nlu.py                 # NLU intent parser tests
│   ├── custom_commands.json            # Persistent custom command definitions
│   ├── .env.example                    # Sample environment configuration template
│   ├── requirements.txt                # Python package dependencies
│   └── main.py                         # Voice Assistant CLI entry point
│
├── password-generator/                 # Task 2: Random Password Generator CLI
│   └── password_generator.py           # Self-contained password generator script
│
└── chat-application/                   # Task 3: Real-Time Multi-Client Chat
    ├── server.py                       # Multi-threaded TCP chat server
    └── client.py                       # Interactive TCP chat client
```
