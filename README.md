# published-vs-planned

**"Scheduled" is not "live". This skill makes the agent look before it says so.**

`published-vs-planned` is an agent skill for Claude Code (and any agent that reads `SKILL.md` skills). Schedulers accept a post and fail later: an expired token, the wrong page, a reel rejected for its length, or Instagram silently dropped from a cross-post. The agent sees "success" and reports "all published". You open the profile and nothing is there.

With the skill, the agent builds the plan list first (one row per item per network, with time zone), reads every item back from the scheduler's own list, and after the slot passes opens the **public** page, Facebook and Instagram checked separately. It reports one table: planned, scheduled, live, gap and likely cause, fix. It uses the word "published" only for what it saw live in that check.

## See the difference

> **You:** Did everything go out today? I open Instagram and I don't see the reel.

**Without the skill:** "All 6 posts were published successfully." (It read six success messages from the scheduler.)

**With the skill:**

| # | Item | Planned | Scheduled | Live | Gap and cause | Fix |
|---|---|---|---|---|---|---|
| 2 | Page A, IG, reel | Tue 10:00 | ok | missing | cross-post to IG dropped, no error | republish, then check the profile again |
| 1, 3-6 | ... | ... | ok | ok | none | none |

"Checked Tue 21:40 (UTC-6): 5 of 6 live, 1 gap."

**Skip it if** you only need ad results or reach numbers. It checks that the content exists where it should, not who saw it.

**Status:** new. Built from real cases in the author's own setup. Tested with and without the skill on 3 real past prompts: 5.5/6 with it, 3.5/6 without. The run without it never checked the public Facebook page, made no table and gave no cause. Plain instructions, no scripts, no network calls. MIT. Issues and suggestions welcome.

## Install

With the [skills CLI](https://skills.sh):

```bash
npx skills add RabbitDesigns22/published-vs-planned
```

Or manually: copy `skills/published-vs-planned/` into `~/.claude/skills/` for all your projects, or into `.claude/skills/` for one project.

It works for Meta Business Suite, TikTok, LinkedIn, Buffer and any scheduler, and for files uploaded to a drive (it checks the file opens and is not zero bytes).

## Works well with

- [`source-every-fact`](https://github.com/RabbitDesigns22/source-every-fact): the facts on the post are right before it goes out.
- [`report-now`](https://github.com/RabbitDesigns22/report-now): status checked at this minute, with the time on it.

## Español

**Programado no es publicado.** Las herramientas de programación aceptan el post y fallan después: token vencido, página equivocada, reel rechazado o Instagram que se cae sin aviso. El agente lee "éxito" y dice "todo publicado". Con esta skill arma la lista de lo planeado, la compara con la lista del programador y, cuando pasa la hora, abre la página **pública**, Facebook e Instagram por separado. Solo dice "publicado" de lo que vio en vivo y entrega una tabla con lo que falta primero.

Instalar: `npx skills add RabbitDesigns22/published-vs-planned`

## More skills from the same setup

These come from one real workflow: a small agency run with 15+ Claude Code sessions in parallel. Each skill fixes one problem that kept happening there.

| Skill | What it fixes |
|---|---|
| [one-pass](https://github.com/RabbitDesigns22/one-pass) | get it right the first time; stop paying tokens for rework |
| [hora-exacta](https://github.com/RabbitDesigns22/hora-exacta) | real date and time in every message, so nothing lands on the wrong day |
| [hands-on](https://github.com/RabbitDesigns22/hands-on) | the agent does what it can and only asks you for codes, keys and payments |
| [easy-for-them](https://github.com/RabbitDesigns22/easy-for-them) | steps people actually follow: direct link, one action per line |
| [one-answer](https://github.com/RabbitDesigns22/one-answer) | one thought-through answer instead of plan, fix, new plan |
| [never-twice](https://github.com/RabbitDesigns22/never-twice) | a shared error log so no session repeats a known mistake |
| [sort-me-out](https://github.com/RabbitDesigns22/sort-me-out) | one ordered list of what is urgent, waiting and forgotten |
| [in-the-loop](https://github.com/RabbitDesigns22/in-the-loop) | a live board so parallel sessions know what the others changed |
| [study-first](https://github.com/RabbitDesigns22/study-first) | reads everything in full and answers point by point, no invented details |
| [session-watchdog](https://github.com/RabbitDesigns22/session-watchdog) | wakes the sessions that got stuck mid-task, leaves the rest alone |
| [skill-harvest](https://github.com/RabbitDesigns22/skill-harvest) | reads your sessions and finds the skills you are missing |
| [small-budget-ads](https://github.com/RabbitDesigns22/small-budget-ads) | Meta Ads rules for 1-5 USD a day ad sets |
| [whatsapp-closer](https://github.com/RabbitDesigns22/whatsapp-closer) | evidence-ranked rules for a WhatsApp sales assistant that closes |
| [whatsapp-number-onboarding](https://github.com/RabbitDesigns22/whatsapp-number-onboarding) | connect a number to the WhatsApp Cloud API in the safe order |
| [proposal-pdf](https://github.com/RabbitDesigns22/proposal-pdf) | short PDF proposals with every price checked against its source |
| [published-vs-planned](https://github.com/RabbitDesigns22/published-vs-planned) | says "published" only for what it saw live on the public page, Facebook and Instagram checked apart |
| [source-every-fact](https://github.com/RabbitDesigns22/source-every-fact) | every price, phone and name on a post traced to its source, nothing added |
| [only-what-was-asked](https://github.com/RabbitDesigns22/only-what-was-asked) | "pause only Google Ads" pauses only Google Ads, and proves the rest did not move |
| [model-per-chat](https://github.com/RabbitDesigns22/model-per-chat) | the right model for each chat: top model where mistakes cost money, cheap or none where it only runs often |
| [music-by-niche](https://github.com/RabbitDesigns22/music-by-niche) | music that matches the client's business, never repeated for a client or across clients in 3 weeks |
| [full-power](https://github.com/RabbitDesigns22/full-power) | the best the model can do on high-stakes work: strongest model only for the hard step, best-of-N with a judge, fresh-eyes verifier |

If one of them saved you a redo, a star helps other people find it.

## License

MIT. Made by [Rabbit Designs](https://github.com/RabbitDesigns22).
