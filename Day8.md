VIM is a modal editor.
This means: what you type depends on the mode you are in.

📌 VIM MODES – QUICK OVERVIEW
+------------+     i / a / o     +-----------+
| NORMAL     | ---------------> | INSERT    |
| (Default)  |                  | Mode      |
+------------+ <--------------- +-----------+
       |             ESC
       |
       |  : (colon)
       v
+------------+
| EXECUTE    |
| (Command)  |
+------------+

Visual Mode: v / V / Ctrl+v (from Normal Mode)

1️⃣ Entering Execute Mode (Command Mode)
🔹 What is Execute Mode?

Execute Mode is used to run commands like:

Save file

Quit file

Search text

Replace text

Set line numbers

🔹 How to Enter Execute Mode

👉 Press : from Normal Mode

ESC  →  :


You will see this at the bottom of the screen:

:

🔹 Common Execute Mode Commands
Command	Purpose
:w	Save file
:q	Quit
:wq	Save and quit
:q!	Force quit
:set nu	Show line numbers
:set nonu	Hide line numbers
🧪 Real-Time Example

You are editing /etc/nginx/nginx.conf

ESC
:w


✅ File saved

:q


✅ Exit editor

📝 Practice Questions

How do you force quit without saving?

Which command saves and exits together?

How do you enable line numbers?

2️⃣ Executing Basic Commands
🔹 File Operations
Task	Command
Open file	vim file.txt
Save	:w
Save as	:w newfile.txt
Quit	:q
Save + Quit	:wq

📌 DevOps Example
Editing Kubernetes YAML:

vim deployment.yaml

🔹 Searching Text
Command	Meaning
/word	Search forward
?word	Search backward
n	Next match
N	Previous match

🧪 Example:

/server


Finds all occurrences of server

🔹 Line Numbering
Command	Use
:set nu	Show line numbers
:set nonu	Hide line numbers
:10	Jump to line 10

📌 Real Scenario
Error log shows:

Error at line 245


You do:

:245

📝 Practice Questions

How do you search for the word error?

How do you jump to line 100?

How do you save file with a new name?

3️⃣ Entering Visual Mode

Visual Mode is used to select text.

🔹 Types of Visual Mode
Key	Mode
v	Character-wise
V	Line-wise
Ctrl + v	Block-wise
🔹 Visual Mode Diagram
Normal Mode
     |
     v
Press v / V / Ctrl+v
     |
     v
+--------------------+
| SELECT TEXT HERE   |
+--------------------+

🧪 Real-Time Example

Select a paragraph:

V


Move arrow keys ↓ ↑
Entire lines get selected

📝 Practice Questions

Which key selects full lines?

Which mode is used for column editing?

How do you exit visual mode?

4️⃣ Manipulating Text in Visual Mode

Once text is selected, you can operate on it.

🔹 Common Operations
Key	Action
d	Delete
y	Copy (yank)
p	Paste
>	Indent
<	Un-indent
🧪 Real-Time Examples
🔸 Delete a block
v
(select text)
d

🔸 Copy & Paste
V
(select lines)
y
p

🔸 Indent Code (Python / YAML)
V
(select lines)
>


📌 DevOps Use Case
Indenting YAML blocks properly to avoid pipeline failures.

📝 Practice Questions

How do you copy selected text?

How do you indent selected lines?

How do you paste copied content?

5️⃣ Revisioning the Complete VIM Editor (Quick Recap)
🔁 Mode Summary
Mode	Purpose
Normal	Navigation
Insert	Writing text
Execute	Commands
Visual	Selection
🔑 Most Important Keys (Must Remember)
ESC   → Normal Mode
i     → Insert Mode
:     → Execute Mode
v     → Visual Mode

🧠 VIM Cheat Diagram
ESC
 |
 |-- i --> INSERT
 |
 |-- v --> VISUAL
 |
 |-- : --> EXECUTE

🎯 Final Practice (Hands-On)

Create a file:

vim test.txt


Insert text using i

Save using :w

Search a word using /

Enable line numbers

Select lines and delete them

Save and exit
