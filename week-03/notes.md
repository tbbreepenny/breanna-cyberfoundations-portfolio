# Week 3 Notes — Windows, Linux, and Your First Commands

**Student Name:** Breanna Pennywell

**Date Completed:** 09/08/2026

Summarize this week's key concepts in your own words — not copy-pasted definitions.

## Key Concepts This Week

- Files, folders, and the file-system tree
- Windows vs. Linux file system differences (paths, case-sensitivity, drives)
- Navigating the shell: `pwd`/`Get-Location`, `ls`/`dir`, `cd`
- Reading files and getting help: `cat`/`type`, `--help`/`man`/`Get-Help`
- Creating and organizing: `mkdir`/`touch`, `cp`/`mv`, `rm`

## In My Own Words

**What's the difference between a file and a folder, and how do they form a tree together?**

```
A file is a single item that holds actual content while a folder doesn't hold content itself but instead holds other files and/or other folders. Because folders can contain more folders inside them, they form a branching structure called a tree: starting from a root or home directory at the top, each folder can branch into subfolders, which can branch further, all the way down to individual files at the "leaves" of the tree. In this lab, that structure was visible directly — /home/agent contained the archive folder, which contained the incident-42 folder, which finally contained the actual file, access-log.txt.
```

**How does a Windows-style file path differ from a Linux-style file path?**

```
A Windows path starts with a drive letter and uses backslashes to separate folder names, for example C:\Users\agent\Documents. A Linux-style path has no drive letter at all — it starts from a single root (/) and uses forward slashes (/) to separate folders, like /home/agent/archive/incident-42.
```

**One command from this week you feel most confident with — and why?**

```
The command I feel most confident with is Get-Content. I used it directly on access-log.txt and it did exactly what I expected right away without any confusion about syntax or arguments. It also mapped cleanly onto cat, which I'd already used earlier in the bash pass, so seeing the same task done with a different command name made the concept stick rather than feeling like something new to learn from scratch.
```

---

## Submission Checklist

- [x] I summarized each concept in my own words, not copied definitions

- [x] I answered all three "In My Own Words" prompts

- [x] This file is committed to my portfolio repo at `week-03/notes.md`
