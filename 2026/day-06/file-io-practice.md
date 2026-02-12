# Day 06 – Linux Fundamentals: File Read & Write Practice

## 1️⃣ Create File

$ touch notes.txt

Observation:
Created an empty file named notes.txt.

---

## 2️⃣ Write to File (Overwrite Mode)

$ echo "Linux is powerful." > notes.txt

Observation:
Used `>` which overwrites the file content.

---

## 3️⃣ Append to File

$ echo "DevOps requires Linux skills." >> notes.txt
$ echo "Practice builds confidence." >> notes.txt

Observation:
Used `>>` which appends content without deleting existing lines.

---

## 4️⃣ Use tee (Write + Display)

$ echo "File handling is important." | tee -a notes.txt

Output:
File handling is important.

Observation:
`tee -a` appended text and displayed it on the terminal at the same time.

---

## 5️⃣ Read Full File

$ cat notes.txt

root@vagrant:/home/vagrant# touch notes.txt
root@vagrant:/home/vagrant# echo "Linux is powerful." > notes.txt
root@vagrant:/home/vagrant# echo "DevOps requires Linux skills." >> notes.txt
root@vagrant:/home/vagrant# echo "Practice builds confidence." >> notes.txt
root@vagrant:/home/vagrant# echo "File handling is important." | tee -a notes.txt
File handling is important.
root@vagrant:/home/vagrant# cat notes.txt
Linux is powerful.
DevOps requires Linux skills.
Practice builds confidence.
File handling is important.
root@vagrant:/home/vagrant#

Observation:
`cat` displays the entire file content.

---

## 6️⃣ Read First 2 Lines

root@vagrant:/home/vagrant# head -n 2 notes.txt
Linux is powerful.
DevOps requires Linux skills.


Observation:
`head` shows the beginning of the file.

---

## 7️⃣ Read Last 2 Lines

root@vagrant:/home/vagrant# tail -n 2 notes.txt
Practice builds confidence.
File handling is important.

Observation:
`tail` shows the last lines of the file.

