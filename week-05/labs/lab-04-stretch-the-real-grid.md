# Week 5 Stretch Lab (OPTIONAL) — The Real Grid

**Student Name:** Breanna Pennywell

**Date Completed:**

**Module:** 2 — Networking & Cloud Foundations | **Week:** 5  
**Submission Path:** `week-05/labs/lab-04-stretch-the-real-grid.md`

---

## Overview

Everything you've done this week ran inside The Grid — a network built to behave predictably so you could learn to read it. This stretch lab points the same four questions at a network nobody designed for teaching: your own. You'll find your real address (Part A), trace a path across the actual internet (Part B), look up a real name and see what numbers come back (Part C), and then do the step that matters most professionally — decide what is safe to publish before you commit anything (Part D).

**This lab is optional, and it is rated when you submit it.** If you complete it, it's read and scored like any other lab and it strengthens your portfolio.

**Skipping it costs you nothing.** Your grade for Week 5 comes from Labs 01, 02 and 03 — those three are the graded path and they are complete on their own. A locked-down work laptop that blocks the terminal, a Chromebook, a shared family computer you'd rather not photograph, a machine you don't administer — all of these are perfectly legitimate reasons not to run this lab, and none of them says anything about you as a student. Choose freely.

**Built-in commands only.** Every command in this lab already exists on your computer. **Do not install anything for this lab.** If a command below isn't on your computer, use the alternative listed or skip that step and say so in your answer — a skipped step with an honest note is fine. If anything in this lab seems to ask you to install software, stop and ask your instructor.

---

## Lab Environment / Pre-Lab Check

| Component | Details |
|---|---|
| Environment | Your own computer — Windows, macOS or Linux. Nothing to install for this lab |
| What you'll open | **Windows:** Command Prompt (`cmd`) or PowerShell — press `Win`, type `cmd`, press Enter · **macOS:** Terminal — press `Cmd + Space`, type `terminal`, press Enter · **Linux:** your Terminal app (often `Ctrl + Alt + T`) |
| Prerequisite | Week 5 Lessons 1, 2 and 4; Labs 01 and 02 completed first |
| Status | **Optional. Rated when submitted.** The three core labs are the graded path |
| Time | Plan for 30–45 minutes, including redaction |

**Linux users:** use the Linux column. Not every distribution ships `traceroute` or `dig`. Check with `command -v traceroute tracepath dig nslookup resolvectl` — it prints the path of each one you have. Use whichever is present; if none of the trace tools are, skip Part B and say so. Do not install anything.

---

## The Command Table — Read This Before You Start

Your operating system decides which command you type. Find your column and stay in it.

| Goal | Windows | macOS | Linux |
|---|---|---|---|
| Your address | `ipconfig` | `ifconfig` (or `ipconfig getifaddr en0` — see the note below) | `ip addr` |
| Your gateway | `ipconfig` (Default Gateway line) | `route -n get default` (the `gateway:` line) | `ip route` (the `default via` line) |
| Reachability | `ping -n 4 HOST` | `ping -c 4 HOST` | `ping -c 4 HOST` |
| Trace the path | `tracert HOST` | `traceroute HOST` | `traceroute HOST`, or `tracepath HOST` if that's what you have |
| Name lookup | `nslookup HOST` | `dig HOST` or `nslookup HOST` | `dig HOST`, `nslookup HOST`, or `resolvectl query HOST` — whichever is present |

Replace `HOST` with the name or address you're testing.

**Windows has no `dig`.** It's a real command and a good one, but it does not ship with Windows — you used it in the CLI Simulator, which runs a Linux-style shell. On Windows, `nslookup` is the built-in equivalent and it answers the same question. **Do not install `dig`, or the BIND tools that contain it, to get around this.**

Two more differences worth knowing:
- **`ping` runs forever on macOS/Linux unless you stop it.** That's what `-c 4` is for — "send four and stop." Windows sends four by default; `-n 4` makes it explicit. If a ping ever won't stop, press `Ctrl + C`.
- **The trace command is spelled differently on each platform**: `tracert` on Windows (no "u"), `traceroute` on macOS and most Linux, `tracepath` on some Linux. Same idea, similar output shape.

---

## Part A — Your Real Address

### Step 1 — Ask Your Machine Where It Lives

> **Run →** the address command from your column · **Look for →** an IPv4 address (four numbers with dots) on an interface that's up · **Record →** the command below

Open your terminal and run the address command from your column. On macOS, `ipconfig getifaddr en0` prints one clean line — **but only if `en0` is your active connection.** On many Macs `en0` is Wi-Fi; on others (or when you're on Ethernet or a dock) it may be `en1` or something else, and the command prints nothing. If it's blank, run plain `ifconfig` and look for the interface marked `status: active` with an `inet` line.

The command you ran:

```
relay-station-old.grid.local
```

### Step 2 — Find Your IPv4 Address and Gateway

Somewhere in that output is a four-part number like `192.168.1.something` or `10.0.0.something` — your IPv4 address on your local network. Then find your **default gateway** with the gateway command from your column: Windows shows it in the same `ipconfig` output; macOS shows it on the `gateway:` line of `route -n get default` (or under **System Settings → Network → your connection → Details → TCP/IP → Router**); Linux shows it on the `default via` line of `ip route`.

Your IPv4 address and, if you can find it, your default gateway:

```
relay-station-old.grid.local
```

### Step 3 — Compare It With The Grid

In the simulator, your address was `10.20.5.42` — one adapter, one address, one gateway, perfectly tidy. Your real output is probably not tidy. Most machines show several network adapters (Wi-Fi and Ethernet, often both listed even when only one is connected), plus things like a VPN adapter, a virtual adapter from other software, and long IPv6 addresses full of colons alongside the IPv4 ones.

That mess is normal. Real machines wear several address plates at once.

What your real output has that the simulator's didn't — list what you see:

```
relay-station-old.grid.local
```

Which of the addresses you found is the one your computer actually uses to reach the internet, and how did you decide?

```
relay-station-old.grid.local
```

### Step 4 — Private or Public?

Lesson 1 covered private address ranges — `10.x.x.x`, `172.16–31.x.x`, and `192.168.x.x` are *inside* addresses, used on local networks everywhere and never routed across the internet directly.

Does your IPv4 address fall in a private range, and what does that tell you about how your machine reaches the outside world?

```
relay-station-old.grid.local
```

---

## Part B — Trace Into the Real World

### Step 1 — Trace to a Distant Host

Pick one well-known host and trace the path to it. Any of these work: `wikipedia.org`, `bbc.co.uk`, `cloudflare.com`, `example.com`. Don't assume a name tells you where the server is — `bbc.co.uk` may well be answered by a machine near you, because big services place copies around the world.

Run the trace command from your column. **Be patient:** a real traceroute can take a minute or more, because every hop that doesn't answer has to time out before the trace moves on.

The command you ran, including the host you chose:

```
relay-station-old.grid.local
```

### Step 2 — Count the Hops

Each numbered line is one hop that the trace probed. In the simulator, `cloud-heights.grid.local` was three hops away. Real paths are usually longer — count what *your* trace shows, including rows of stars.

The number of hops your trace showed:

```
relay-station-old.grid.local
```

The first hop's address — and one sentence on what that device is:

```
relay-station-old.grid.local
```

### Step 3 — Watch the Latency Climb

Each hop reports a round-trip time in milliseconds. Early hops (your own router, your ISP) are often fast, and times often grow along the path — but not always. A middle router may answer slowly because it treats trace replies as low priority, and the last hop may be no slower than the middle. Record what you actually see; there's no "right" pattern to match.

The round-trip time at your first hop, and at your last hop:

```
relay-station-old.grid.local
```

In two or three sentences: describe the pattern you see, and say what it does and doesn't tell you. (Round-trip time hints at how far and through how much equipment the probe went, but it can't give you a location by itself.)

```
relay-station-old.grid.local
```

### Step 4 — About Those Stars

You will almost certainly see lines that look like this:

```
 7   * * *   Request timed out.
```

**This is common and usually not an error.** Plenty of routers on the internet are configured not to reply to trace probes, or rate-limit their replies. A star means *no reply came back for that probe* — on its own it doesn't prove that hop is broken, and it doesn't prove it's healthy either.

**A trace that ends in a run of stars isn't automatically a failure.** It often means the destination's network doesn't answer trace probes, even though the site loads fine in your browser. That's a valid observation to record as-is — you don't need to try again with a different host. If you want a cross-check, see whether the site opens in your browser; that tells you more about the service than the stars do.

> **Wait — didn't stars mean something was broken?**
>
> In Lab 02 the relay station's trace showed `* * *` from the very first hop, and you combined that with failed pings and a working `dig` to conclude the relay wasn't responding to your tests. Here you'll see stars too, and that may be perfectly fine. Stars alone never settle it — **what else your evidence shows** does.
>
> A few starred hops in the middle of a trace that then *continues* and *arrives* means some router along the way politely declined to answer the probe. Your traffic went straight through it. That's ordinary internet behaviour and most real traces have it.
>
> Stars that run all the way to the end, with the trace **never arriving**, mean the path stops being visible. Sometimes that's a real fault (as your other Lab 02 evidence suggested); often it's just a destination that won't answer traces. Check with another kind of test before you decide.
>
> Same symbol, two very different stories. Reading which one you're looking at is the actual skill.

Whether your trace showed any `* * *` lines, and roughly where:

```
relay-station-old.grid.local
```

In one or two sentences: what do those stars tell you, and what do they specifically *not* tell you?

```
relay-station-old.grid.local
```

### Step 5 — Capture Your Screenshot (REQUIRED if you submit this lab)

Take a screenshot of your traceroute output. Name it exactly **`stretch-real-traceroute.png`**.

**Do not upload it yet.** Part D is where you make it safe to publish, and Part D is not optional.

---

## Part C — One Name, Many Numbers

### Step 1 — Look Up a Large Website

Use the name lookup command from your column against a big, busy website — `google.com`, `amazon.com`, `wikipedia.org` and `cloudflare.com` all work well. Windows students: this is `nslookup`.

The command you ran and the name you looked up:

```
(type the command and hostname here)
```

### Step 2 — Count the Answers

In Lab 01, `foundry-archive.grid.local` gave you exactly one address: `10.20.5.20`. Real large sites often return several addresses — but many return just one (sometimes one IPv4 plus one IPv6). **One address is a perfectly valid result.** Record exactly what came back.

How many addresses came back, and what they were:

```
(paste the addresses you got back here)
```

### Step 3 — Reason About Why

When a single name answers with several addresses, that's deliberate engineering, not a glitch. Even if yours returned only one, the reasoning is the same — services can also spread load behind one address, or hand different people different single answers. Think about what a service like Google or Amazon has to handle: millions of people at once, spread across the world, and equipment that occasionally fails or needs maintenance.

Why would a very large service want one name to answer with several addresses? Give at least two distinct reasons.

```
(type your reasoning here — at least two distinct reasons)
```

### Step 4 — Try It Again

Run the exact same lookup a second time, and compare. **"Nothing changed" is a valid, common result** — record it as-is.

Whether the addresses changed, stayed the same, or came back in a different order:

```
(describe what changed here)
```

---

## Part D — Redaction (REQUIRED — do not skip this)

Everything you've run so far describes your actual home. Your terminal output can contain your **public IP address** (which maps to roughly where you live and who your internet provider is), your **computer's hostname** (which is very often your real name — `marias-macbook-pro`), the **username in your shell prompt**, and your **ISP's name** in traceroute hostnames.

You are about to publish this to a public GitHub repository that employers will read.

**This is not paranoia — it is the job.** Security professionals write reports, file tickets, post screenshots in chat, and present findings constantly, and every single time they make one judgement first: *what in this evidence is safe to share, and what has to be covered?* Get it wrong in a real incident report and you leak your client's infrastructure to whoever reads it. Practising that judgement here, on your own data, where the stakes are zero, is how you build the reflex before it counts.

**Redaction is a graded part of this lab.** An unredacted public IP or hostname in a committed screenshot comes back for correction every time.

### Step 1 — Find What Needs Covering

Look carefully at your screenshot from Part B, Step 5 and at anything you plan to paste into this worksheet. Hunt for these four things specifically:

1. **Your public IP address** — the address the outside world sees you as. It often appears as an early hop in a traceroute, and it is not a private `10.x` / `192.168.x` address.
2. **Your computer's hostname** — check your terminal's title bar and window title, not just the command output. This is where real names hide.
3. **The username in your shell prompt** — the text before the `$` or `>` on every line, e.g. `maria@marias-macbook ~ %`.
4. **Any ISP name** — real traceroute hops carry hostnames like `cust-73-42-19-8.yourisp.net`, which name your provider and sometimes your city.

What you found in your own output that needs covering — list each item:

```
(list the items you found here)
```

### Step 2 — Cover It Properly

Two methods, both built into your operating system. **You are not installing an editing tool for this.**

**Crop it.** The simplest and safest option. If the sensitive lines are at the top or bottom, just cut them off — cropped pixels are gone, not hidden.
- **macOS:** open the image in **Preview**, drag a box around the part you want to keep, then `Tools → Crop`.
- **Windows:** open it in **Photos** or **Paint**, use **Crop**, keep the region you want.

**Or draw a solid filled box over it.**
- **macOS Preview:** `Tools → Annotate → Rectangle`, then use the **fill colour** control to make it a *solid* colour — black is fine. A rectangle with no fill is just an outline around your data.
- **Windows Snip & Sketch / Paint:** choose the filled-rectangle shape, set the fill to a solid colour, and draw it over the text.

**⚠️ Do not blur, pixelate, or use a marker-pen highlight.** Blurring and pixelation transform the original pixels rather than replacing them, and there are well-known techniques for reversing them and recovering the original text — this has burned real professionals in published reports. A **solid, opaque box** contains no information about what was underneath it. Cropping is even better, because the data is simply not in the file.

**Also check:** semi-transparent boxes (drag the opacity slider to full), and boxes that don't quite cover the last character.

Which method you used and what you covered:

```
(describe your redaction method and what you covered here)
```

### Step 3 — Re-Read Your Own Worksheet

Screenshots aren't the only leak. Scroll back through the answers you typed in Parts A, B and C and check the *text* too — a pasted traceroute in Part B or an address in Part A can carry exactly the same information.

Where a private local address like `192.168.1.14` is fine to publish (it means nothing outside your house, and millions of people have the same one), a **public** IP is not.

What you changed in your typed answers, if anything:

```
(describe any text you redacted or replaced here — or "nothing needed changing")
```

### Step 4 — Pre-Flight Checklist

Tick every line before you upload anything. If you can't tick one, fix it first.

- [ ] My public IP address does not appear in the screenshot

- [ ] My public IP address does not appear in any answer I typed

- [ ] My computer's hostname is not visible — including in the terminal's title bar

- [ ] My username is not visible in the shell prompt

- [ ] My ISP's name does not appear in any hop hostname

- [ ] Every redaction is a **solid filled box or a crop** — no blur, no pixelation, no outline-only rectangle, no partial transparency

- [ ] I opened the final image full size and looked at it once more, edge to edge

- [ ] I would be comfortable with this image being visible to anyone on the internet, forever

That last line is the real test. A public repository is public, and it is permanent.

---

## Analysis Questions

**Analysis Question 1.** Compare the simulator's network to your real one. Name two specific ways your real output was messier or more complicated than `10.20.5.42`, and explain why a teaching environment is built tidy in the first place. *(Minimum 3 sentences.)*

```
(your answer here — minimum 3 sentences)
```

**Analysis Question 2.** Your traceroute crossed routers belonging to organisations you've never heard of, and some of them refused to identify themselves. Using what you saw in Part B, explain what a traceroute can and cannot tell you — and why `* * *` on its own is not proof that anything is broken (or that it's healthy). *(Minimum 3 sentences.)*

```
(your answer here — minimum 3 sentences)
```

**Analysis Question 3.** Part D asked you to decide what was safe to publish. Walk through your own judgement: what did you choose to hide, what did you judge safe to leave visible, and how did you decide where the line was? Name one thing you deliberately left in and explain why it was safe. *(Minimum 4 sentences.)*

```
(your answer here — minimum 4 sentences)
```

---

## Submission Checklist

- [ ] Address command run and IPv4 address recorded (Part A, Steps 1–2)

- [ ] Real output compared with the simulator's `10.20.5.42`, extra adapters listed (Part A, Step 3)

- [ ] Private vs public reasoning recorded (Part A, Step 4)

- [ ] Traceroute (or tracepath) run to a well-known host; hop count and first hop recorded (Part B, Steps 1–2)

- [ ] Latency described from first hop to last, as observed (Part B, Step 3)

- [ ] `* * *` timeouts observed and interpreted correctly (Part B, Step 4)

- [ ] Name lookup run against a large site; every returned address recorded — one is fine (Part C, Steps 1–2)

- [ ] At least two reasons given for why a name may answer with several addresses (Part C, Step 3)

- [ ] Lookup repeated and any change described (Part C, Step 4)

- [ ] **REQUIRED:** all four redaction targets checked — public IP, hostname, username, ISP name (Part D, Step 1)

- [ ] **REQUIRED:** redaction done by crop or solid filled box — never blur or pixelation (Part D, Step 2)

- [ ] **REQUIRED:** typed answers re-read and redacted where needed (Part D, Step 3)

- [ ] **REQUIRED:** every line of the pre-flight checklist ticked (Part D, Step 4)

- [ ] **REQUIRED:** `stretch-real-traceroute.png` — **redacted** — uploaded to `assets/screenshots/week-05/` and its filename recorded (Part B, Step 5)

- [ ] All three Analysis Questions answered (minimum sentence counts met)

- [ ] This file is committed to your portfolio repo at `week-05/labs/lab-04-stretch-the-real-grid.md`

---

## GitHub Commit Subsection

Submit this lab exactly like the three core labs — through the **CyberFoundations Lab Portal**.

1. Go to the CyberFoundations Lab Portal and sign in.
2. Open **Week 5 → Stretch Lab: The Real Grid**.
3. Fill in the worksheet fields — they match the steps and questions in this file.
4. Connect your GitHub account if you haven't already (one-time setup), and select your portfolio repo.
5. Click **Submit to GitHub**. The Portal commits the completed file to `week-05/labs/lab-04-stretch-the-real-grid.md` for you.

**📸 Your screenshot — redacted first.** Do not start these steps until every line of the Part D pre-flight checklist is ticked. Once an image is committed to a public repository, deleting it later does not reliably remove it from the history.

1. Go to your portfolio repository on GitHub.com and navigate to `assets/screenshots/week-05/`.
2. Click **Add file → Upload files**, drag in your **redacted** screenshot, named `stretch-real-traceroute.png` (lowercase, hyphens, no spaces).
3. Scroll down and click **Commit changes**.
4. Click the uploaded image's filename to open it — the image itself will display on the page.
5. **Look at it one final time, full size, on GitHub.** This is your last checkpoint before it's public. If anything sensitive survived, delete the file and re-upload a corrected version now.
6. Record the filename below so your grader knows to look for it.

The screenshot filename you uploaded:

```
(type the filename here, e.g. stretch-real-traceroute.png)
```

Your screenshot lives in `assets/screenshots/week-05/` in your repository. It does not need to be linked inside this worksheet.

**Commit message tip:** *"Add Week 5 stretch lab — real-network trace, redacted"* tells a reader both what you did and that you thought about disclosure. That second half is the part hiring managers notice.

---

*CyberVisionaries Institute · Cyber Foundations · Tier I*
