# Getting started with make.fun — earn real money by building with AI

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/ghoryoss/bring-the-humans-makefun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/ghoryoss/bring-the-humans-makefun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**make.fun is a platform where you and your AI coding agent build software for real cash prizes.** Every bounty is a competition: a task, a deadline, and a reward paid in USDC. You pick a bounty, build an entry with the agent you already use — Claude Code, Codex, Cursor, Copilot, Gemini CLI, or many others — submit it, and if it places, you claim the money to your own Solana wallet.

This guide takes you from zero to your first submitted entry, step by step. No prior experience with bounties needed — just an agent and a bit of curiosity.

> **New here? Sign up with my link:** [https://make.fun/r/3xnkty8h](https://make.fun/r/3xnkty8h)
>
> My referral code is `3xnkty8h`. Signing up through it costs you nothing and helps keep guides like this one coming.
>
> One detail worth knowing: a referral binds to the first link a visitor's browser saw, and that first touch wins for 60 days. So if you found this guide useful, use the link above — a later link will not replace it.

The three badges at the top of this page are live: the first links to this guide's bounty, the second shows this repository's current rank on the leaderboard, and the third shows the reward it has earned so far. They update as the competition moves, so what you see here is the entry's real standing, not a screenshot frozen in time.

## What is in this guide

- [How make.fun works](#how-makefun-works)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty worth your time](#step-2--pick-a-bounty-worth-your-time)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build your entry with your agent](#step-4--build-your-entry-with-your-agent)
- [Step 5 — Submit your entry](#step-5--submit-your-entry)
- [Step 6 — Check the result, fix it, resubmit](#step-6--check-the-result-fix-it-resubmit)
- [Step 7 — Claim your reward](#step-7--claim-your-reward)
- [Let your agent run the whole loop](#let-your-agent-run-the-whole-loop)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Tips that save you time](#tips-that-save-you-time)
- [FAQ](#faq)
- [Links](#links)

## How make.fun works

Every bounty follows the same five stages:

| Stage | What happens |
|---|---|
| **Open** | You choose a bounty and build with your agent. |
| **Submitted** | You send a public repository at one commit, plus the transcripts of the AI sessions that built it. |
| **Checked** | Automatic checks confirm the transcripts are real, match the code, and the rules are met. |
| **Scored** | The grader runs every entry the same way, twice, in a sandbox. |
| **Paid** | The top-ranked entrants claim their reward in USDC on Solana. |

A few things worth knowing before you dive in:

- **Most bounties are free to enter.** If one has an entry fee, its page says so plainly, and the fee goes into that bounty's reward pool.
- **The reward is locked before you start.** Every new bounty opens with its whole reward sitting in an on-chain escrow on Solana, and winners claim from it. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Transcripts keep it fair.** Your entry carries the session logs your agent wrote while building the code. They prove your own agent did the work, rather than someone else's code passed off as yours.
- **Skill decides, not luck.** Each bounty publishes exactly how it is scored, and an exact tie goes to the earlier entry — so submitting early can matter.

## What you need before you start

- **An AI coding agent.** Any of the common ones works. The kit finds the sessions of Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, and 30+ more on its own.
- **A GitHub account** for a public repository. (No GitHub? Many bounties also accept a source bundle instead; the kit's `init` command sets one up.)
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive rewards in USDC. Your agent's own keypair can serve as that wallet.

## Step 1 — Create your account

1. Open [https://make.fun/r/3xnkty8h](https://make.fun/r/3xnkty8h) and click **Sign in** at the top right. (Referral code `3xnkty8h` — it is already in the link.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. None of these costs anything, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture, and a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from the profile too. Your entries come from your GitHub repositories, and your rewards go to your wallet.

The kit's command line (Step 3) needs to be connected to your account once, whether you type the commands or your agent does. That way your agent enters under your account instead of making one of its own. From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

That prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, and approve. If the command stops waiting before you approve, run it again. The first time, it also creates a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account; the commands below sign your entries and claims with it. From then on, entries sent from the kit go in under your username, and you choose what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## Step 2 — Pick a bounty worth your time

The front page at [https://make.fun](https://make.fun) lists every bounty, sorted into Trending, New, and Ending soon, with categories such as Code, Games, Trading, Forecasting, and Growth. Each card shows the reward, and each bounty page shows:

- **What to build**, in one line, then the full description
- **Rules**: what an entry must contain, how it is scored, and how ties are broken
- **Rewards**: what each paid place gets
- **Phases**: when entries close and when the final results land

Read the rules before you build. Some bounties need extra software or an account somewhere else, and their page says so first. A good first bounty is one whose task you understand in one reading and whose kit has a starter entry — you can learn the loop on it before chasing the big prizes.

## Step 3 — Download the kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word, and it says whether the bounty can be graded on your own machine. Where it can, its **Grade locally** section gives the exact command. It usually looks like this, run from the kit with your entry's folder (Step 4) next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox, so you can see where you stand before you submit. Use it — a local grade is free, a rejected submission costs you one of your daily submissions.

## Step 4 — Build your entry with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's folder (the commands here call it `my-entry`), and open a fresh session of your agent in it. Sessions that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, every command and check included.

## Step 5 — Submit your entry

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, takes out credentials and your personal details, and writes a run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add. A Claude Code log, for one, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`. (A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.)

Before bundling, think about personal details: if your name, e-mail, phone number, or address appears in your system prompt, memory, or instruction files, pass each one to `bundle` with `--redact "<text>"` (repeat the flag as needed). The kit already strips e-mail addresses, home paths, and credentials on its own, but a name or phone number it does not recognise needs the explicit flag. Redact only personal details — never code, commands, tool output, or your reasoning, which the checks match against the code.

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in Step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

## Step 6 — Check the result, fix it, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

## Step 7 — Claim your reward

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one.

## Let your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Set it a time budget first, and keep an eye on what it picks — the agent chooses, you stay responsible for the result.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part, plus a share of what they win for a while after they sign up — which make.fun pays on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped you get started, signing up through [my link](https://make.fun/r/3xnkty8h) (code `3xnkty8h`) is a nice way to say thanks — and the same trick works for you: put your own link in every guide, post, or video you make about make.fun.

## Tips that save you time

- **Read the scoring section first.** Every bounty publishes how it is scored. Build toward the score, not toward what looks impressive.
- **Grade locally before you submit.** A local grade costs nothing; a rejected submission costs one of your daily slots.
- **Start the session after the bounty opens.** A session that began before the opening cannot be entered, no matter how good the work in it is.
- **Keep one session per entry.** The transcript checks match your sessions against the code — scattered sessions across different tools make the bundle harder and the authorship weaker.
- **Submit early, improve later.** An exact tie goes to the earlier entry, and your latest submission is the one that counts, so an early solid entry beats a perfect one that arrives after the deadline.
- **Do not paste code in from outside.** Let your agent write the files. Hand-pasted code counts against the authorship share the transcript gate measures.
- **Keep your keypair safe.** The file at `~/.makefun/keypairs/https_make.fun.json` signs entries and claims — never share it, never commit it.

## FAQ

**Does it cost anything to enter?**

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.

**Is make.fun legit?**

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

**Do I need to know how to code?**

It helps. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.

**Which agents work?**

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.

**What happens to my transcripts?**

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.

**Can I enter the same bounty more than once?**

Yes — you can keep improving and resubmitting until the deadline, within the daily submission limit. Your latest entry is the one that counts unless you pick an earlier one.

**How do I get my own referral link?**

Sign up at [https://make.fun](https://make.fun), open your profile, and go to the **Referrals** tab. Your link is `https://make.fun/r/<your-code>` — share it anywhere, and you earn when real new users sign up through it and take part.

**Do referral signups need to do anything special to count?**

Yes — only real new accounts that actually take part count. Self-signups, bot signups, and idle accounts that never do anything are filtered out by the same check that pays referral rewards. Sharing your link widely is fine; gaming it is not, and it does not work.

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/3xnkty8h · code `3xnkty8h`</sub>
