# Grok Bot

[Data 8 Tutor by Benjamin](https://x.ai/bot/3JTODK3i9jilU1aOo0gCo)
is a hosted Data 8 tutor for UC Berkeley students. On first use it sets up
the Spring 2026 course materials on its own cloud computer. After that it
gives hints, cites lectures and the textbook, and is instructed not to hand
over solution code or answer keys.

Unlike the self-hosted CLI, Discord, and Slack options, you do not install
the tutor locally or import a course archive yourself.

<div class="guide-actions" markdown>
[Add Data 8 Tutor to Grok Bot](https://x.ai/bot/3JTODK3i9jilU1aOo0gCo){ .md-button .md-button--primary }
</div>

<div class="outline-grid" markdown>

<div class="outline-card" markdown>
:material-open-in-new:{ .outline-card__icon }

### Add the template

Open the shared tutor and add a copy to your Grok Bot account.
</div>

<div class="outline-card" markdown>
:material-cloud-download-outline:{ .outline-card__icon }

### Let first-use setup finish

The tutor downloads and stores Spring 2026 course materials on its own
computer. You do not paste a setup prompt or provide local files.
</div>

<div class="outline-card" markdown>
:material-chat-question-outline:{ .outline-card__icon }

### Ask a Data 8 question

Once setup completes, ask for hints and citations the same way you would
ask a course tutor.
</div>

</div>

## What you need

- A Grok Bot account with an eligible paid plan
- Enough included or on-demand Grok Bot usage for first-use setup and later
  questions

## Cost

Grok Bot does not have a separate tutor fee. According to the
[Grok Bot FAQ](https://docs.x.ai/grok-bot/faq), it is included with paid
individual Cursor plans, Cursor Teams, and linked SuperGrok subscriptions.
Eligible subscriptions include weekly usage; additional work may be billed
on demand according to model and token cost.

[SuperGrok currently starts at $30 per month](https://x.ai/pricing) and lists
Grok Bot access as an included feature. Prices, included usage, and account
eligibility can change, so check the live pricing and usage pages before
starting.

!!! note "First-use setup uses resources"
    The tutor's automatic Spring 2026 setup can consume a meaningful part of
    the account's included Grok Bot usage. Later questions also consume
    usage.

## Tradeoffs

**Advantages**

- No local Python install, API key, or Discord/Slack bot configuration
- One-click template add; first-use setup collects the corpus itself
- The cloud computer can keep working after you close the laptop
- The tutor is already instructed to hint and cite, not hand over answers

**Limits**

- Requires an eligible paid plan; there is no separate free Grok Bot tutor
  SKU
- First-use setup and later questions consume weekly or on-demand usage
- Every bot on the account shares one cloud computer, including files and
  browser sessions
- Solution files live on that computer; prompt rules are not a technical
  access control
- This path does not use the project's local retrieval engine, so results
  are not directly comparable to the CLI, Discord, or Slack tutors

## 1. Add the tutor

1. Open [Data 8 Tutor by Benjamin](https://x.ai/bot/3JTODK3i9jilU1aOo0gCo).
2. Select **Add to Grok Bot**.
3. Review the template's instructions and integrations before accepting it.
4. Open the new tutor's chat.

The [official Grok Bot FAQ](https://docs.x.ai/grok-bot/faq) states that adding
a shared bot gives you a copy of its configuration and does not give the
template author your computer, logins, or conversation history.

## 2. Let it set up the course materials

On first use, the tutor sets up the Spring 2026 course materials on its own
persistent cloud computer. Wait for that step to finish before asking course
questions.

Do not upload files from your personal computer, and do not ask the tutor to
browse, mount, or access your local drives. The template is designed to
collect and store the corpus itself.

## 3. Ask a question

After setup completes, ask:

```text
How do I use tbl.where? Give me a hint and cite the lecture or textbook
source you used.
```

A useful response should explain the concept, cite course material, and avoid
providing assignment solution code.

## Data and privacy boundaries

The tutor stores course materials on a persistent cloud computer. The
[official FAQ](https://docs.x.ai/grok-bot/faq) notes that every bot on one
account shares that computer, including its files and browser sessions.
Separate bots are therefore not a security boundary.

!!! warning "Course materials include restricted solution files"
    The Spring 2026 corpus includes solution and answer-key files. The tutor
    is instructed not to disclose them, but prompt instructions are not a
    technical access control. Do not share the cloud-computer account with
    students, and do not rely on a separate bot to isolate those files.

Grok Bot requires cloud data storage and does not support Legacy Privacy
Mode. Review the account's privacy settings before adding the tutor.

## Course material licensing

The Spring 2026 materials retain their source licenses. Included content uses
a mixture of BSD 3-Clause, CC BY-NC 4.0, and CC BY-NC-ND 4.0 terms. Use the
corpus noncommercially, preserve attribution, and consult each included
license before redistributing or modifying its materials.
