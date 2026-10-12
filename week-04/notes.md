# Week 4 Notes — Permissions, Searching, and Virtual Machines

**Student Name:** BREANNA PENNYWELL

**Date Completed:** 10/11/2026

Summarize this week's key concepts in your own words — not copy-pasted definitions.

## Key Concepts This Week

- File permissions: read/write/execute × owner/group/other, and reading `ls -l`
- Changing permissions with `chmod` (symbolic and numeric) — and THE GATEKEEPER'S RULE
- Windows ACLs, read with `Get-Acl` (the real-world `icacls` tool does the same job, but is not available in the simulator)
- Wildcards (`*`, `?`, `[ ]`) and searching inside files with `grep`/`Select-String`
- Virtual machines: host vs. guest, the hypervisor, Type 1 vs. Type 2, isolation
- The VM lifecycle: create, start, stop (deallocate), snapshot, delete — and what each costs
- Golden snapshots — how your Weeks 6–12 lab machines are made

## In My Own Words

**Decode `-rw-r-----` audience by audience: who can do what to this file?**

```
The owner can read and write the file but not execute it; the group can only read it; and everyone else can't read, write, or execute it.
```

**What is a hypervisor, and what are its two jobs?**

```
A hypervisor is the software that runs on a physical host computer and lets it host virtual machines. Its two jobs are to carve up the host's real resources (CPU, memory, and disk) into slices and allocate them to each VM, and to keep the VMs isolated from each other so one can't see or interfere with another.
```

**A stopped VM still costs a little money. What is it paying for, and what's the only way to reach a true zero?**

```
A stopped (deallocated) VM is still paying for its disk storage, about $0.002/hr in the simulator, because the virtual disk still exists even though CPU and RAM billing has paused. The only way to reach a true zero is to delete the VM, which destroys the disk, and that is why a snapshot should be taken first if you might want to rebuild.
```

---

## Submission Checklist

- [x] I summarized each concept in my own words, not copied definitions

- [x] I answered all three "In My Own Words" prompts

- [x] This file is committed to my portfolio repo at `week-04/notes.md`
