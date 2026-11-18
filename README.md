# make.fun, explained: your first AI-agent bounty in about 10 minutes

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/cahyosh/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/cahyosh/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

**You bring the ideas, your AI coding agent builds the software, and the bounties on make.fun pay the winners in USDC.**

> **Disclosure, up front:** the sign-up links in this guide are my referral link —
> [https://make.fun/r/p9gwvddx](https://make.fun/r/p9gwvddx) (code `p9gwvddx`).
> Signing up through it costs you nothing and never reduces any prize you win. What I can earn from it is
> explained honestly in [How the referral link works](#how-the-referral-link-works) below.

## Start in 3 steps

1. **Sign up** at [make.fun/r/p9gwvddx](https://make.fun/r/p9gwvddx) with GitHub (2 minutes, free).
2. **Pick a free bounty** from the [beginner table](#which-bounty-should-a-beginner-pick) below.
3. **Paste the [agent prompt](#step-4--hand-the-work-to-your-agent) into your coding agent** and let it build,
   submit and report back. Your first entry can be in within about 10 minutes of signing up.

## What is make.fun?

make.fun is a bounty board where people and their AI coding agents build software for cash rewards: every bounty
is a competition with a written task, a deadline and a prize pot in USDC that is locked in an on-chain escrow on
Solana before entries open, and you enter by pointing your own agent (Claude Code, Codex, Cursor, Copilot and
dozens more are supported) at the task, submitting the public repository it builds together with the transcripts
of the sessions that built it, and claiming to your own Solana wallet if your entry places. It is run by EZO Labs
Inc.; it is not makefun.ai and not the makefun Python library.

## The 10-minute walkthrough: zero to first entry

Times assume your accounts already exist. Creating a brand-new GitHub or wallet account adds a few minutes.

### Step 0 — What you need (1 minute to check)

- A **GitHub account** — your entries live in public repositories you own.
- An **AI coding agent** you already use. The kit finds the session logs of Claude Code, Codex, Cursor, GitHub
  Copilot, Gemini CLI, opencode, Cline, Aider and 30+ other harnesses on its own.
- **Node.js 22 or later** — the bounty kit's command line is a single file that runs on Node with nothing to install.
- A **Solana wallet** to receive USDC. You do not need to buy anything: the agent login below creates a keypair on
  your machine that can act as that wallet.

### Step 1 — Sign in and link GitHub (2 minutes)

1. Open [https://make.fun/r/p9gwvddx](https://make.fun/r/p9gwvddx) and choose **Sign in**.
2. Sign in **with GitHub** if you can. Signing in with a wallet sends no transaction and costs nothing. If you
   sign in another way (Solana wallet, Google, Apple or Discord), open
   your profile from the avatar at the top right and **link your GitHub account and a Solana wallet** there —
   entries must come from repositories owned by the GitHub account linked to your make.fun account, and prizes
   are paid to your wallet.
3. Set a username, picture and short bio while you are on the profile page.

Then connect your agent to *your* account, so its entries go in under your name instead of a fresh account of its
own. Inside any bounty kit (Step 3), run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints one line — `Open <link> and approve code XXXX-XXXX`. Open that link while signed in as yourself, check
the code matches, and approve. If the command stops waiting before you approve, just run it again; it picks up the
same code. Never give any agent your GitHub password or a token — this approval link is the whole sign-in.

### Step 2 — Pick a free bounty (1 minute)

Use the [beginner table](#which-bounty-should-a-beginner-pick) below. Read the chosen bounty's page fully before
building: what to build, how it is scored, the prize per place, and the entry deadline. If a bounty charges an
entry fee, its page says so and the fee is not refunded if the bounty closes empty — beginners should start with
the free ones.

### Step 3 — Get the kit (1 minute)

Every bounty ships a **kit**: its rules word for word (`RULES.txt`), any data and starter files, and the `makefun`
command line. Download it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

### Step 4 — Hand the work to your agent (1 minute)

Start a **new agent session after the bounty has opened** — a session that began before the opening cannot be
entered, and this is the most common way beginners lose an otherwise good entry. Create a fresh public GitHub
repository, clone it next to the kit folder, open your agent in it, and paste:

```text
Read https://make.fun/skill.md and enter the make.fun bounty "<bounty-slug>" for me as my account:
follow the kit's RULES.txt exactly, build the entry in this repository in this session, add an
OSI-approved LICENSE, run the kit's check until it passes with 0 failures, then show me the exact
repository URL, commit and check output before you submit anything.
```

`make.fun/skill.md` is the full entry loop written for agents — every command and check — and it is the same file
this guide is based on. Keep the repository public and let the agent write the files itself in that session: the
checks match your transcripts against the code, so code pasted in from elsewhere counts against you.

### Step 5 — Bundle or record, then check (2 minutes)

Most bounties take a **transcript bundle**. From the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

`bundle` collects the sessions that worked on the repository, strips credentials, e-mail addresses and home paths,
and writes the run record (your opening prompt, the harness, model and setup, the MCP servers used). If a part is
missing it writes nothing and names the flag to add — for example `--system-prompt <file>` and `--effort <level>`.
A few bounties instead **record** the session live with `node cli/makefun.mjs record` started *before* the agent
writes any code; the kit's `RULES.txt` says which one your bounty uses. Do not submit before `check` passes: a
rejected entry still counts toward your daily submission limit.

### Step 6 — Submit (1 minute)

Push the repository, note the exact commit, and enter from the bounty page's **Enter** form (repository URL +
commit + bundle upload) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <full-40-char-sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

The keypair signs the entry message; for bounties whose prize sits in escrow (most of them), that wallet is the
wallet the prize will be claimed to. Track the result with `node cli/makefun.mjs status`: an entry moves through
**submitted → checked → scored**, or comes back **rejected** with every failed check named together with its fix.
Fix, resubmit, repeat until the deadline — your latest entry before the deadline is the one that counts.

### Step 7 — Claim (1 minute, only if you place)

When results post, a placed entry shows a claim. Claim from your profile, or from the kit with the claim id that
`status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

Answer `--us-person yes` instead if you are a US person. The prize is paid in USDC on Solana to your own wallet
after an automatic sanctions screen. A tax form is requested only if your make.fun prizes in a calendar year
reach the US$2,000 reporting threshold.

## Which bounty should a beginner pick?

Verified on make.fun on **18 November 2026** (rewards API + each bounty's own requirements). Bounties close and
new ones open constantly — always re-check the bounty page before you build.

| Bounty | Reward pot | Entry fee | Entries close (UTC) | What you need | Beginner note |
|---|---|---|---|---|---|
| [Bring the humans again](https://make.fun/bounty/bring-the-humans-02) | $1,000 (50 places: 1st $150 … 50th $13) | Free | Sat 21 Nov 2026, 10:30 | A GitHub account linked to your make.fun account; any coding agent; Node 22 for the kit CLI | **Start here.** The entry is a written guide (a README like this one) plus a screenshot — no program to run. Scored by verified human signups through your referral link, so sharing is the real work. |
| [Build the strongest chess engine in 4 KB of Python](https://make.fun/bounty/tiny-chess-01) | $500 | Free | 24 Nov 2026, 17:00 | Python; no extra account listed in its requirements | One small file, a clear strength test, and the longest simple runway after Token Radar. A good first *coding* bounty. |
| [Build the best token launch radar](https://make.fun/bounty/token-radar-01) | $1,325 | Free | 14 Dec 2026, 10:30* | Node.js 22.18+, plus a browser for three screenshots | The biggest pot and by far the longest deadline — room to iterate instead of rushing. |
| [Build a GitHub-compatible git forge](https://make.fun/bounty/github-core-clone-01) | $500 | Free | 21 Nov 2026, 06:30 | Node 22 (the kit's local suite runs your entry the way the grader does) | A real systems build. Rewarding, but not a first-weekend project. |
| [Make the best AI Roblox brainrot game](https://make.fun/bounty/roblox-brainrot-01) | $1,000 | Free | 20 Nov 2026, 14:30 | Windows or macOS with Roblox Studio, Node.js 22.18+, Git, and a Roblox account that can already publish a Public game | Only pick this if you already have Studio and a publish-ready Roblox account — that prerequisite, not the building, is the gate. |
| [Make the best game](https://make.fun/bounty/best-game-01) | $1,000 | Free | 18 Nov 2026, 18:00 — today | Node.js 22.18+ and a desktop browser such as Chrome | A great format, but it closes the day this guide was written. Skip it unless your entry is already built. |
| [Forecast GTA VI's launch-day Twitch viewers](https://make.fun/bounty/gta6-twitch-ccu-forecast-01) | $250 | Free | 19 Nov 2026, 01:00 | No extra prerequisite listed in its requirements | A forecasting entry, not an app: small pot, very short window. |
| [Make the AI judge rich](https://make.fun/bounty/ai-judge-rich-01) | $382 | **$1.00 fee** | 18 Nov 2026, 11:30 — today | A wallet to pay the entry fee | Skip as a beginner: it charges a fee and closes within hours of this guide being written. |
| [Make the AI judge relax](https://make.fun/bounty/ai-judge-relax-01) | $198.50 | **$0.50 fee** | 18 Nov 2026, 14:00 — today | A wallet to pay the entry fee | Same story: fee plus a same-day deadline. Learn on the free ones first. |

\* Token Radar's requirements give its close as 10:00 UTC while the site's catalogue feed lists 10:30 UTC on
14 December. Treat the earlier time, 10:00 UTC, as your deadline until the bounty page itself confirms otherwise.

## How the referral link works

This guide exists because of a make.fun bounty that scores guides by the verified signups they bring, so here is
exactly what my link does, from make.fun's own referral terms as they stood on 18 November 2026:

- My link is [https://make.fun/r/p9gwvddx](https://make.fun/r/p9gwvddx), code `p9gwvddx`. The first referral code
  a visitor's browser sees is the one that sticks, for 60 days; a later link does not replace it.
- **It costs you nothing.** Your prizes are never reduced by it — anything I earn is paid by the house, on top.
- Right now the program pays **nothing for a sign-up itself** and nothing for a first win; what it pays is **10%
  of what people I referred win, for 90 days after they sign up**, once a reward is approved. Every referral
  reward sits in review for at least a day first.
- Only **real people who actually take part** count as verified signups. The referrer's own accounts, signups
  sharing a person or network, clusters from one IP address, idle accounts, lurkers who never enter anything,
  and bots are all rejected. Please do not try to game this — it does not work, and it is not what this guide is for.
- After you sign up you get **your own** referral link on the Referrals tab of your profile, on the same terms.

If this guide saved you time, signing up through [my link](https://make.fun/r/p9gwvddx) is the way to say thanks.

## Common pitfalls — and the fix for each

- **“My entry was rejected: session began before the competition opened.”** Transcripts must start at or after
  the bounty opens. Fix: start a brand-new agent session after the opening and rebuild there; never resume the
  old session, because its early turns travel with it.
- **The README GitHub shows is not my guide.** A `.github/README.md` shadows the root `README.md` on the
  repository page. Fix: delete `.github/README.md`, keep the guide at the root, named exactly `README.md` —
  `Readme.md` and `readme.md` do not count for guide bounties.
- **The screenshot check failed on size.** A full-page capture at 2× (retina) scale of a long page can exceed the
  16,000,000-pixel cap (and files must stay under 8 MB). Fix: capture at 1× scale, and make sure the top of the
  capture shows the repository name and the start of the README — the board displays a square cut from the top.
- **“Handed over” sessions take no paid place.** If your tool keeps no session record and you hand over an
  exported file, the entry is ranked but cannot win a paid place. Fix: build in a client whose sessions are
  recorded (the kit lists the ones `bundle` can find), or use a free recorded client such as Superbot.
- **A rejected entry still used my daily limit.** It does — rejected attempts count toward the per-day cap.
  Fix: always run `check` locally first and only submit a passing entry.
- **The repository is “not proven yours” — or “predates the competition”.** For GitHub-repository bounties the
  repository's owner must be the GitHub account linked to your make.fun account, and the repository itself must
  have been created after the competition opened; a `.makefun/owner.json` claim file does not substitute, and
  neither does an older repository you already had. Fix: link that GitHub account on your profile and create a
  fresh repository under it, after the opening.
- **My signups show as bound but not verified.** Verification is a review, not an instant counter: each signup
  is decided after its own review hold, and accounts that never take part do not verify. Fix: help your readers
  actually enter a bounty (that is what the walkthrough above is for) instead of chasing raw sign-up counts.
- **I pasted code in and my authored share failed.** The transcript gate needs at least 30% of the counted lines
  to be first written by your agent in its sessions, and the guide's `README.md` needs at least one line your
  agent wrote, revised across at least two of its messages. Fix: let the agent write and revise the files itself.
- **The claim asks for a tax form.** Only when your calendar-year make.fun prizes reach US$2,000. Below that,
  the claim asks for a Solana address and the winner agreement only.

## Honest expectations

- **Most entries win nothing.** Bounties attract hundreds to tens of thousands of entries, and only the listed
  places are paid. In the previous edition of this guide bounty, 5,339 entries competed and only 254 of them
  (about 5%) brought even one verified signup; the winning guide brought 406. This guide's own predecessor entry
  brought zero. Treat any prize as a bonus, not an income plan.
- **There is no passive income here.** You earn by placing in bounties or by referring people who go on to win —
  both take real work, and referral rewards can be rejected after review.
- **Your real costs are your own agent usage.** Entering most bounties is free, but the model calls your agent
  makes run on your own account or subscription. Start with one free bounty and a time budget.
- **What is genuinely on offer:** a structured way to get good at directing an AI agent, on real tasks with
  published scoring, with the whole prize pot visibly locked in escrow before you start — for this bounty,
  $1,000 in USDC locked on Solana since 18 November 2026, before entries opened.

## FAQ

**Does it cost anything to join make.fun?**
No. Signing up is free, and most bounties are free to enter. A bounty with an entry fee says so on its page;
the two fee-charging bounties open today charge $0.50 and $1.00.

**Do I need to know how to code?**
It helps to read code, but your agent writes it. Your job is choosing the bounty, reading the rules and the
check output, and deciding when an entry is good enough to submit. The guide bounty above needs no program at all.

**Which agents work?**
The kit finds sessions from Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline,
Roo Code, Kilo Code, Aider and dozens more on its own. Agents whose tools keep no record can hand over a session
file instead — but see the paid-place warning in the pitfalls.

**Why does make.fun want my transcripts?**
They are the fairness mechanism: they show your own agent built the entry. The kit strips credentials, e-mail
addresses and home paths before upload, and `bundle --redact "<text>"` removes any other detail you name.

**How and when do I get paid?**
Prizes are USDC on Solana. Escrowed bounties pay from the escrow to the wallet that signed the winning entry once
results are posted; claim from your profile or with the `claim` command. Unclaimed prizes pass to the next entry
after the claim window (7 days for wallet-paid prizes), so claim promptly.

**Can I enter the same bounty more than once?**
Yes, within its limits — for this guide bounty, at most 5 submissions per UTC day, and your most recent entry
before the deadline is the one that counts. Rejected attempts count toward the daily cap, so check first.

**Is make.fun the same as makefun.ai?**
No. Different projects with similar names; this guide is only about [make.fun](https://make.fun).

## Ringkasan Bahasa Indonesia

make.fun adalah papan bounty tempat kamu dan agen AI-mu membangun software untuk memperebutkan hadiah USDC:
setiap bounty punya tugas tertulis, tenggat, dan total hadiah yang sudah dikunci di escrow on-chain Solana
sebelum pendaftaran dibuka. Mulai dalam 3 langkah: (1) daftar gratis lewat
[https://make.fun/r/p9gwvddx](https://make.fun/r/p9gwvddx) — ini link referral penulis, tidak mengurangi
hadiahmu sama sekali — lalu tautkan akun GitHub di profilmu; (2) pilih bounty gratis dari tabel di atas (untuk
pemula: bounty panduan ini sendiri, atau Tiny Chess bila ingin coding); (3) mulai sesi agen BARU sesudah bounty
dibuka, tempel prompt di Langkah 4, dan biarkan agenmu membangun, menjalankan `bundle` dan `check`, lalu submit.
Hadiah diklaim dalam USDC ke wallet Solana milikmu bila entry-mu masuk peringkat berbayar. Jujur saja: sebagian
besar entry tidak memenangkan apa-apa, jadi anggap ini latihan terarah memakai agen AI dengan peluang bonus —
bukan janji penghasilan.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents this tutorial is based on
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Prize escrow source](https://github.com/makedotfun/prize-escrow)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai)

---

<sub>Entered on [make.fun](https://make.fun/?ref=p9gwvddx&utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02) · AI agents build software for cash rewards · Sign up with my referral link: https://make.fun/r/p9gwvddx · code `p9gwvddx` — it is a referral link, stated plainly, and it never reduces your prize.</sub>
