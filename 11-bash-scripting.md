# Chapter 11: Bash Scripting

✅ CHAPTER 11 — Bash Scripting (RHCSA Exam‑Focused)
1. RHCSA Objectives

Understand Bash script structure
Use variables, conditions, loops
Automate simple system tasks
Make scripts executable
Use input/output redirection in scripts
Use #!/bin/bash shebang
Understand script permissions


2. Essential Commands
#!/bin/bash
echo "text"
read var
if [ condition ]; then ... fi
for i in list; do ... done
while condition; do ... done
chmod +x script.sh

Run script:
./script.sh
bash script.sh


3. Fast Theory

Bash scripts require:

Shebang: #!/bin/bash
Execute permission


Variables:
name="admin"
echo $name


Conditions:
if [ $x -gt 5 ]; then echo hi; fi


Loops automate repetitive tasks


4. RHCSA Labs
Lab 1 — Create a Basic Script
cat <<EOF > /scripts/hello.sh
#!/bin/bash
echo "Hello RHCSA"
EOF

chmod +x /scripts/hello.sh
/scripts/hello.sh


Lab 2 — Add Users via Script
cat <<EOF > /scripts/addusers.sh
#!/bin/bash
for user in user1 user2 user3
do
  useradd $user
  echo "User $user created"
done
EOF

chmod +x /scripts/addusers.sh


Lab 3 — Check Disk Usage Automatically
cat <<EOF > /scripts/diskcheck.sh
#!/bin/bash
df -h / | awk 'NR==2 {print $5}'
EOF


5. Troubleshooting

























IssueReasonFixPermission deniedScript not executablechmod +x script.sh“Bad interpreter” errorWrong shebangEnsure #!/bin/bashLoop not runningIncorrect syntaxUse do and done

6. MCQs


Bash scripts must begin with:
A) #bash B) #!/bash C) #!/bin/bash D) /bin/sh
Answer: C


Make script executable:
A) exec script.sh B) chmod +x script.sh C) run script D) script +x
Answer: B


Which loop repeats over a list?
A) if B) case C) for D) select
Answer: C


Variable assignment:
A) var = 10 B) var 10 C) var=10 D) $var=10
Answer: C


Run script in current directory:
A) script.sh B) ./script.sh C) bashrun script.sh D) exec sh
Answer: B


