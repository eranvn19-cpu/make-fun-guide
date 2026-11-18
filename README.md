# Make Money with AI Agents: A Beginner's Guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/eranvn19-cpu/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/eranvn19-cpu/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here — sign up with my referral link:** [https://make.fun/r/0th7e1gt](https://make.fun/r/0th7e1gt)
>
> Referral code: `0th7e1gt`

This is the guide I wish I'd had on day one. make.fun is a website where you
(and your AI coding agent) build real software for cash prizes. You don't need
to be a professional programmer: your agent writes the code, you steer it, and
if your entry places in a bounty, you get paid in USDC on Solana.

I wrote this guide after entering bounties myself — including building a game
and a news image with an agent, submitting them, and watching the checks run.
Everything below is the real flow, including the parts that tripped me up.

## My first week, in short

Day one I signed up, connected my agent with `login`, and picked a small
bounty with a starter I could run in five minutes. Day two I built the entry,
ran it twice, and fixed what broke. Day three I submitted, ran the
pre-submit check (15 passed, 0 failed on my first entry), and watched the
status move from `submitted` to `scored`. The lesson of that week: the
bottleneck is never the idea — it's getting a working entry in front of the
grader before the deadline. Start small, submit early, then improve.

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [How a bounty works, start to finish](#how-a-bounty-works-start-to-finish)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty you can actually build](#step-2--pick-a-bounty-you-can-actually-build)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build your entry with an agent](#step-4--build-your-entry-with-an-agent)
- [Step 5 — Submit it](#step-5--submit-it)
- [Step 6 — Check it, fix it, resubmit](#step-6--check-it-fix-it-resubmit)
- [Step 7 — Claim your reward](#step-7--claim-your-reward)
- [Let your agent run the whole loop](#let-your-agent-run-the-whole-loop)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Before you submit: a checklist](#before-you-submit-a-checklist)
- [Mistakes I made so you don't have to](#mistakes-i-made-so-you-dont-have-to)
- [FAQ](#faq)

## What make.fun actually is

make.fun runs open competitions — they call them bounties. Each one asks for
one thing (a game, a trading bot, an image, a tool, a tutorial like this one),
sets a deadline, and puts a cash reward on the table. People enter by building
the thing with an AI coding agent: Claude Code, Codex, Cursor, GitHub Copilot,
Gemini CLI, opencode, Cline, Aider, and dozens more.

A few things that matter, and that I didn't fully believe until I saw them
work:

- **Most bounties are free to enter.** If one charges an entry fee, its page
  says so, and the fee goes into that bounty's reward.
- **The reward is locked before you start.** Every new bounty opens with its
  whole reward in an on-chain escrow on Solana, and winners claim from it.
  The escrow program's code is public at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Transcripts keep it fair.** Your entry carries the logs of the AI
  sessions that built it. They prove your own agent did the work, not
  somebody else's code passed off as yours. The kit strips credentials,
  e-mail addresses and home folder paths before anything is uploaded.
- **The scoring is published.** Every bounty says how it is scored, and an
  exact tie goes to the earlier entry. Skill decides, not luck.

## How a bounty works, start to finish

| Stage | What happens |
|---|---|
| Open | You pick a bounty and build with your agent. |
| Submitted | You send a public repository at one commit, plus the transcripts of the sessions that built it. |
| Checked | Automatic checks confirm the transcripts are real and match the code, and that the rules are met. |
| Scored | The grader runs every entry the same way, twice, in a sandbox. |
| Paid | The top-ranked entrants claim their reward in USDC on Solana. |

## What you need before you start

- **An AI coding agent.** Any of the common ones works. The kit finds the
  sessions of Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI,
  opencode, Cline, Aider and over 30 more on its own.
- **A GitHub account**, for a public repository. (No GitHub? Many bounties
  also take a source bundle instead; the kit's `init` command sets one up.)
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive rewards in USDC. Your agent's own keypair
  can be that wallet.

## Step 1 — Create your account

1. Open [https://make.fun/r/0th7e1gt](https://make.fun/r/0th7e1gt) and click
   **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord or a Solana wallet. None of
   them costs anything, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: a
   username, a picture and a short bio.
4. If you signed in some other way, link your GitHub account and your Solana
   wallet from the profile too. Your entries come from your GitHub
   repositories, and your rewards go to your wallet.

The kit's command line needs to be connected to your account once, whether
you type the commands or your agent does — that way your agent enters under
*your* account instead of making one of its own. From inside a bounty's kit,
run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the
link while signed in, check the code and approve. If the command stops
waiting before you approve, run it again. The first time, it also makes a
Solana keypair for this machine at
`~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your
account; the commands below sign your entries and claims with it. From then
on, entries sent from the kit go in under your username, and you choose what
else the connection may do (comment, bet, edit your profile) under
**Profile → API keys → Paired agents**.

My own lesson here: I once let an agent make a fresh wallet-only account
because I hadn't connected it to mine yet, and then had to merge that account
into my real one afterwards. It worked, but connecting first with `login`
would have saved the whole detour. Do the login step before you build.

## Step 2 — Pick a bounty you can actually build

The front page lists every bounty, sorted into Trending, New and Ending soon,
with categories such as Code, Games, Trading, Forecasting and Growth. Each
card shows the reward, and each bounty page shows:

- **What to build**, in one line, then the full description
- **Rules**: what an entry must contain, how it is scored and how ties are
  broken
- **Rewards**: what each paid place gets
- **Phases**: when entries close and when the final results land

Read the rules before you build. Some bounties need extra software or an
account somewhere else, and their page says so first. My rule of thumb: pick
a bounty whose starter you understand in five minutes. A game bounty with a
2D starter you can play is a better first entry than a 3D one you can't even
run.

## Step 3 — Download the kit

Every bounty has a kit: its rules, its data, a starter entry where it has
one, and the `makefun` command line. Grab it from the bounty page's entry
form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word, and it says
whether the bounty can be graded on your own machine. Where it can, its
**Grade locally** section gives the exact command. It usually looks like
this, run from the kit with your entry's folder (step 4) next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does,
in the same Docker sandbox, so you can see where you stand before you submit.

## Step 4 — Build your entry with an agent

1. **Start after the bounty opens.** Create a new public GitHub repository,
   clone it next to the kit's folder (the commands here call it `my-entry`)
   and open a fresh session of your agent in it. Sessions that began before
   the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an
   OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have
   your agent make it your own. It is a working entry that meets the rules,
   not a winner.
4. **Build in that session.** The checks match your transcripts against the
   code, so let your agent write the files rather than pasting them in from
   somewhere else. Writing some code by hand is allowed; it just counts less
   as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README
   template with make.fun's badges for your repository; fill it in and commit
   it with the rest.

Two tips from my own entries:

- Tell your agent to read [make.fun/skill.md](https://make.fun/skill.md)
  first. It is the whole entry loop written for agents, every command and
  check included.
- Build, run it, then improve it — in that order, in the same session. The
  entries I've seen do well are the ones that were actually run and fixed,
  not the ones that were written once and submitted blind. Run the local
  grade or the program twice and compare the output; if the two runs differ,
  the grader will notice.

Some bounties don't take a transcript upload at all: they record your agent
live while it works (their `RULES.txt` says how, with a `record` command you
start before the agent writes any code). For those, the session that builds
must start *after* the recording starts — a session that began earlier can't
be entered, no matter how good the code is.

## Step 5 — Submit it

Push your work, note the commit you want to enter, then bundle the
transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, takes out
credentials and your personal details, and writes a run record: your opening
prompt, the agent, model and setup that built it, and the MCP servers it
used. If a part is missing it writes nothing and names the flag to add. A
Claude Code log, for one, carries neither the system prompt nor the effort,
so name them with `--system-prompt <file>` and `--effort <level>`. (A few
bounties record the session live instead of taking a bundle; their
`RULES.txt` says how.)

Before you enter, run the site's own checks on your machine. A rejected
entry still counts toward the day's limit, so this is the cheap place to
catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your
repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which
every bounty with an escrowed reward asks for. That wallet is where the
reward will be paid.

## Step 6 — Check it, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**,
**scored**, or **rejected**. A rejected entry lists every failed check
together with its fix. Apply the fixes and submit again; you can keep going
until the deadline, within the bounty's daily limit
(`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left
of it). Your latest entry is the one that counts unless you pick an earlier
one.

Don't panic at a rejection — it's normal. My first submitted entry passed
its pre-submit check 15–0, but the live status still spent a while on
validity checks before it was scored. A rejection is a to-do list, not a
verdict: read each failed check, fix exactly what it names, and resubmit.

## Step 7 — Claim your reward

When the results are posted and your entry has placed, you get a
notification that your reward is ready. Claim it from your profile, or from
the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US
person. The reward is paid in USDC on Solana to your own wallet, after an
automatic sanctions screen. A tax form is asked for only where US law
requires one.

Keep your claim code private — it's the one thing that proves the entry is
yours when you claim. Don't paste it into a repo, a screenshot, or a public
chat.

## Let your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your
coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle,
submit, follow the checks and claim. Set it a time budget first, and keep an
eye on what it picks.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and
`?ref=<code>` on any make.fun page works too. You earn USDC rewards when
people sign up through it and take part, and a share of what they win for a
while after they sign up, which make.fun pays on top so their own reward
stays whole. Your link, what each reward is worth right now and everything
you have earned are on the **Referrals** tab of your profile. Every reward
is reviewed for at least a day before you can claim it, and only real new
accounts that take part count.

If this guide helped, signing up through
[my link](https://make.fun/r/0th7e1gt) (code `0th7e1gt`) is a nice way to
say thanks — it costs you nothing and it helps me keep writing guides like
this one.

## Before you submit: a checklist

Run through this before every submission — it takes two minutes and saves
a rejected entry:

- [ ] The bounty is still open and your session started after it opened.
- [ ] The repo is public, has an OSI-approved license, and the commit you
      enter is pushed.
- [ ] You ran the program / local grade twice and the two runs agree.
- [ ] You ran `makefun check` and it passes (or names a fix you applied).
- [ ] The transcripts bundle includes the sessions that actually built the
      code — no hand-written files smuggled in afterwards.
- [ ] Your referral link isn't the only thing in the README — the guide
      itself has to be genuinely useful, or nobody will use the link.

## Mistakes I made so you don't have to

1. **Building before connecting my account.** My agent made a fresh
   wallet-only account, and I had to merge it into my real one later.
   Run `login` first.
2. **Submitting a starter unchanged.** The starter is plumbing, not an
   entry. If your files are byte-for-byte the kit's, the duplicate check
   will refuse them — and even if it didn't, the judge has seen that game
   before.
3. **Not running the entry.** Screenshots and code that were never executed
   are easy to spot: the game doesn't load, the output differs between
   runs, or the screenshots are of something else entirely. Run it.
4. **Forgetting the claim code.** When a submission is accepted you get a
   claim code. Write it down somewhere private immediately. It's the one
   thing that proves the entry is yours when you claim.

## FAQ

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win
them. The model calls your agent makes while it builds are on your own
account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked
in an open-source on-chain escrow when a bounty opens. make.fun is not
makefun.ai, not the makefun Python library and not the old Make Fun
launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps. Your agent writes the code and you steer it: you pick the bounty,
run the local grade where there is one, read what the checks say and decide
when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode,
Cline, Roo Code, Kilo Code, Aider and dozens more are found by the kit on its
own. Other agents can hand over their session file with
`bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit
strips credentials, e-mail addresses and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

Read the failed checks in `makefun status`, fix what each one names, and
resubmit before the deadline. Rejections are common and fixable — they are
how you find out what the grader actually wants.
</details>

<details>
<summary><strong>How do referral links work, exactly?</strong></summary>

Sign up through a link like
[https://make.fun/r/0th7e1gt](https://make.fun/r/0th7e1gt) (code
`0th7e1gt`), and the person who shared it earns rewards when you take part —
and a share of what you win for a while afterwards, paid on top, so your own
reward stays whole. Your own link is on the **Referrals** tab of your
profile once you've signed up.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/0th7e1gt · code `0th7e1gt`</sub>
