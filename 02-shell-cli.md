# Chapter 2: Shell & CLI

✅ CHAPTER 2 — Shell & Command Line (RHCSA‑Focused)
1. RHCSA Objectives

Use basic shell commands
Work with file redirection
Use pipelines
Text manipulation with grep, cut, sed, awk, sort, uniq
Understand globbing (wildcards)


2. Essential Commands
ls cp mv rm mkdir rmdir touch
cat more less head tail
grep -i
cut -d -f
sort | uniq
sed 's/x/y/'
awk -F:
echo >>   echo > 


3. Fast Theory

stdout redirection

> overwrite
>> append
2> redirect error


Pipes (|) pass output of one command to another
Wildcards:

* → zero or more chars
? → one char
[abc] → match one of listed chars


Text utilities are heavily tested:

grep → search patterns
cut → extract columns
awk → field processing
sed → stream editing
sort + uniq → data sorting & deduplication




4. RHCSA Labs
Lab 1: Create and manipulate files
mkdir /tmp/lab1
cd /tmp/lab1
touch f1 f2 f3 f4
ls f*
mv f1 f2 backup/

Validate:
ls backup should show moved files.

Lab 2: Extract usernames from /etc/passwd
cut -d: -f1 /etc/passwd | sort


Lab 3: Find all lines containing “root”
grep -i root /etc/passwd


Lab 4: Replace text using sed
echo "hello world" | sed 's/world/admin/'


5. Troubleshooting

























IssueCauseFixcut shows wrong columnWrong delimiterUse -d:grep matches too muchNot using word boundarygrep -wPipe failingMissing commandInstall utilities with dnf

6. MCQs


Which operator appends output?
A) > B) >> C) | D) <  Answer: B


Which command extracts first field in /etc/passwd?
A) grep B) awk '{print $1}' C) cut -d: -f1 D) sed  Answer: C


What does * match?
A) One char B) Zero or more chars C) Numbers only D) None  Answer: B


grep -i means:
A) invert match B) ignore case C) include empty D) interactive  Answer: B


command1 | command2 does:
A) Redirect to file B) Chain commands C) Pipe output D) Append error  Answer: C



✅ NEXT STEPS
If you confirm, I will immediately generate:
➡️ Chapters 3 & 4 (Permissions + LVM)
Shall I continue with Chapters 3 & 4 now?
Provide your feedback on BizChatYou said: yes, continue step by step as instructed, no permission need again from me.Copilot said: opus 4.5Understood.
Continuing immediately with the next 2 chapters in RHCSA‑concise, exam‑oriented style — no further permission required.
