# Week 3 Lab 03 — Command Line Scavenger Hunt (CLI Simulator)

**Student Name:** BREANNA PENNYWELL

**Date Completed:** 09/08/2026

**Module:** 1 — Digital Infrastructure & CLI | **Week:** 3  
**Submission Path:** `week-03/labs/lab-03-command-line-scavenger-hunt.md`

---

## Overview

Labs 01 and 02 walked you through each command step by step. This lab is Week 3's wrap-up challenge: a deeper, more independent folder structure with three hidden files to track down, using the navigating and reading commands from Lessons 3A/3B, the creating and organizing commands from Lesson 3C, and your own judgment about when to ask for help. There's less hand-holding here on purpose — this is your chance to prove to yourself that the blinking cursor from the start of Lesson 3A doesn't intimidate you anymore.

**Nothing here can break anything real.** Same consequence-free CLI Simulator as Labs 01 and 02. Getting "lost" in the folder tree costs you nothing but a few extra `cd` moves.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | CyberFoundations CLI Simulator (browser-based, inside the Lab Portal) |
| Shell | Your choice — bash or PowerShell |
| Prerequisite | Labs 01 and 02 completed |

**Before you start:** log into the Lab Portal, open **Week 3 → CLI Simulator**, and load the **"Foundry District Archive Room"** scenario. This tree goes several folders deeper than Labs 01 and 02, and includes a few similarly-named folders on purpose — read carefully before you `cd` into anything.

---

## Part A — The Hunt

Find all three of the following, hidden at different depths in the Archive Room tree:

- A file related to a **shift log**
- A file related to a **maintenance note**
- A file related to a **supply inventory**

For each one, use `pwd`/`Get-Location` and `ls`/`dir` as many times as you need while you search, then record the **full path** once you find it.

Shift log file — full path once found:

```
	/home/archivist/operations/ops-log/shift-log.txt
```

Maintenance note file — full path once found:

```
/home/archivist/records/records-2025/maintenance-note.txt
```

Supply inventory file — full path once found:

```
/home/archivist/records/records-2024/supply-inventory.txt
```

---

## Part B — Read and Report

For each of the three files you found in Part A, use `cat`/`type` to read it and record what it says.

Shift log contents:

```
PS /home/archivist> cd /home/archivist/operations/ops-log
PS /home/archivist/operations/ops-log> cat shift-log.txt
Shift Log - Foundry District Archive Room
07:00 - Archive opened, no incidents overnight.
15:00 - Routine filing complete.
```

Maintenance note contents:

```
PS /home/archivist/operations/ops-log> cd /home/archivist/records/records-2025
PS /home/archivist/records/records-2025> cat maintenance-note.txt
Maintenance Note - Conveyor belt 3 serviced, next check due in 90 days.
```

Supply inventory contents:

```
PS /home/archivist/records/records-2025> cd /home/archivist/records/records-2024
PS /home/archivist/records/records-2024> cat supply-inventory.txt
Supply Inventory - Q4 2024
Gloves - 400 units
Masks - 250 units
Tape - 60 rolls
```

---

## Part C — Organize Your Findings

Now that you've located and read all three files, clean up after yourself the way a professional would — don't leave your findings scattered across the tree.

### Step 1 — Create a Sorted-Findings Folder

Create a new folder called `sorted-findings` in your home directory.

Command you ran:

```
mkdir /home/archivist/sorted-findings
```

### Step 2 — Move All Three Files Into It

Move the shift log, maintenance note, and supply inventory files — the same three you found in Part A — into `sorted-findings`.

Commands you ran:

```
mv /home/archivist/operations/ops-log/shift-log.txt /home/archivist/sorted-findings/
mv /home/archivist/records/records-2025/maintenance-note.txt /home/archivist/sorted-findings/
mv /home/archivist/records/records-2024/supply-inventory.txt /home/archivist/sorted-findings/
```

### Step 3 — Confirm the Move

List the contents of `sorted-findings` to confirm all three files are now there.

Command you ran:

```
cd /home/archivist/sorted-findings
ls
```

Output:

```
PS /home/archivist/sorted-findings> ls
Mode                 Name
-a----               maintenance-note.txt
-a----               shift-log.txt
-a----               supply-inventory.txt
```

---

## Part D — When You Get Stuck

At some point in the Archive Room, you'll likely run across a command or folder name you don't immediately recognize.

### Step 1 — Ask the Terminal

When that happens, use `--help`, `man`, or `Get-Help` instead of guessing. Record what you looked up and what you learned.

Command or term you looked up:

```
Get-Help mkdir
```

What the help text (or the folder's contents) told you:

```
So I tried mkdir --help first, thinking it'd work like it does in bash, but instead I got this weird error: New-Item : missing -Path. Turns out mkdir in PowerShell isn't really its own command — it's just a shortcut for New-Item, and --help isn't a thing PowerShell understands, so it tried to treat --help as a real argument and freaked out because it was missing the -Path part it needed. Once I ran Get-Help mkdir instead, it made way more sense: the actual syntax is New-Item -Path <path>, with some optional extras like -ItemType to say whether you want a file or folder, and -Value if you want to stick some text in it right away.
```

### Step 2 — Describe a Wrong Turn

Everyone takes at least one wrong turn in a tree this size. Describe one moment you ended up somewhere unexpected, and how you used `pwd`/`Get-Location` and `cd ..` to recover.

```
While I was hunting for the supply inventory file, I tried cd records-2025 straight from /home/archivist, but got smacked with bash: cd: records-2025: No such file or directory — twice, because I just assumed it'd be sitting right there in my home folder. I ran ls again to double check what was actually around me, realized records-2025 was tucked one level deeper inside records, and just did cd records first, confirmed with pwd, then cd records-2025 from there — no more errors after that.
```

---

## Analysis Questions

### Analysis Question 1

Which of the three files in Part A took the longest to find, and what was it about the tree's structure (depth, similarly-named folders, etc.) that made it harder?

```
Honestly, the maintenance note gave me the most trouble, even though I found the supply inventory file first without any issues. The problem was the "records" folder split into two similarly-named subfolders, records-2024 and records-2025, and I just assumed the second file would be sitting in my home directory instead of realizing it was nested inside records too. That mix of similarly-named folders plus an extra layer of depth is exactly what tripped me up.
```

### Analysis Question 2

Compare how you felt starting this lab to how you felt at the very start of Lesson 3A, looking at a blank blinking cursor for the first time. What changed?

```
Back at the start of Lesson 3A, staring at that blinking cursor felt intimidating, since I had no idea what to even type or why any of it mattered. By the time I got to this lab, that same blank prompt didn't feel scary anymore.. I automatically thought "okay, pwd first, then ls" instead of freezing up. What really changed is that I now have a mental checklist and the terminal went from feeling like a wall to feeling more like a tool.
```

### Analysis Question 3

Week 4 moves from managing your own files to controlling who's allowed to do what to them — permissions — plus your first look at what a virtual machine is. Based on everything you've practiced this week, what's one thing you're curious about or looking forward to?

```
The thing I'm most curious about going into permissions is why some files/folders need different access levels in the first place. I'm also looking forward to trying out a virtual machine, since it feels like the next real step toward actually working in IT/security.
```

---

## Submission Checklist

- [x] All three target files located, with full paths recorded (Part A)

- [x] All three target files read and their contents recorded (Part B)

- [x] `sorted-findings` folder created and all three files moved into it, confirmed with a listing (Part C)

- [x] At least one command or term looked up with `--help`/`man`/`Get-Help`, with what you learned recorded (Part D, Step 1)

- [x] One wrong-turn moment described, including how you recovered (Part D, Step 2 — minimum 2 sentences)

- [x] All three Analysis Questions answered (minimum sentence counts met)

- [x] This file is committed to your portfolio repo at `week-03/labs/lab-03-command-line-scavenger-hunt.md`

---

## GitHub Commit Subsection

Same mechanism as Labs 01 and 02: fill out this lab's worksheet in the **CyberFoundations Lab Portal** (Week 3 → Lab 03) and click **Submit to GitHub** — the Portal commits the completed file to `week-03/labs/lab-03-command-line-scavenger-hunt.md` automatically. No manual typing or commit needed.

**📌 Optional:** a CLI Simulator session screenshot can be added the same way as Labs 01 and 02 — upload to `assets/screenshots/week-03/`, then right-click the uploaded image and choose **Copy image address**/**Copy Image Link** to embed it — but it isn't required and won't affect your grade.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
