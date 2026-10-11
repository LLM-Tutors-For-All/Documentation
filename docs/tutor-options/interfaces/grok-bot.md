# Grok Bot Tutor

The [Tutor by Benjamin](https://x.ai/bot/3JTODK3i9jilU1aOo0gCo)
template creates a Data 8 tutor in Grok Bot. It gives hints, cites course
materials, and is instructed not to provide solution code or answer keys.
Unlike the self-hosted CLI, Discord, and Slack options, Grok Bot runs on a
persistent cloud computer managed by Grok Bot.

<div class="guide-actions" markdown>
[Add Tutor to Grok Bot](https://x.ai/bot/3JTODK3i9jilU1aOo0gCo){ .md-button .md-button--primary }
[Download data8_sp26.zip](https://github.com/LLM-Tutors-For-All/Documentation/releases/download/data8-sp26-v1/data8sp26.zip){ .md-button }
</div>

The course archive is approximately 935 MiB. Its SHA-256 checksum is:

<div class="checksum-block" markdown>

```text
0fe760f8a54227c3263b06f3d10ef80100db3128d30e3fef63792bcac134c6f3
```

</div>

## What you need

- A Grok Bot account with an eligible paid plan
- Enough Grok Bot usage and cloud-computer storage for the course archive
- About 1 GB of network transfer, plus space for extracted and indexed files

## Cost

Grok Bot does not have a separate tutor fee. According to the
[Grok Bot FAQ](https://docs.x.ai/grok-bot/faq), it is included with paid
individual Cursor plans, Cursor Teams, and linked SuperGrok subscriptions.
Eligible subscriptions include weekly usage; additional work may be billed
on demand according to model and token cost.

[SuperGrok currently starts at $30 per month](https://x.ai/pricing) and lists
Grok Bot access as an included feature. Prices, included usage, and account
eligibility can change, so check the live pricing and usage pages before
starting a large import.

!!! note "Importing the corpus uses resources"
    Downloading, extracting, and indexing the 935 MiB archive may consume a
    meaningful part of the account's included Grok Bot usage. Asking questions
    after setup may also consume usage.

## 1. Add the tutor

1. Open [Tutor by Benjamin](https://x.ai/bot/3JTODK3i9jilU1aOo0gCo).
2. Select **Add to Grok Bot**.
3. Review the template's instructions and integrations before accepting it.
4. Open the new tutor's chat.

The [official Grok Bot FAQ](https://docs.x.ai/grok-bot/faq) states that adding
a shared bot gives you a copy of its configuration and does not give the
template author your computer, logins, or conversation history.

## 2. Ask the tutor to store the course data

Paste the following message into the tutor chat. This directs the agent to
download the archive itself and keep the course files on its own cloud
computer—not browse files on your personal computer.

```text
Set up the Data 8 Spring 2026 course corpus on your own persistent cloud
computer.

1. Download this archive directly:
   https://github.com/LLM-Tutors-For-All/Documentation/releases/download/data8-sp26-v1/data8sp26.zip
2. Verify that its SHA-256 is:
   0fe760f8a54227c3263b06f3d10ef80100db3128d30e3fef63792bcac134c6f3
3. Store and extract it in a dedicated folder named data8_sp26 on your cloud
   computer. Preserve the included LICENSE and PROVENANCE files.
4. Build a durable, searchable local index of all course information in the
   archive for future tutoring conversations. Do not try to place the entire
   archive into one model prompt.
5. Do not request, browse, mount, or access files, folders, drives, or accounts
   on my personal computer. Use only the archive downloaded to your cloud
   computer.
6. Treat files whose names indicate solutions or answer keys as restricted
   reference material. Never quote, reproduce, or reveal final answers,
   solution code, or answer keys to a student. Use them only to provide hints,
   diagnose misconceptions, and cite the corresponding non-solution material.
7. When setup is complete, report the storage folder, checksum result, number
   of indexed files, and any files that could not be processed. Do not delete
   the archive or index unless I ask.
```

The tutor should confirm the checksum before indexing. If it reports a
different value, tell it to delete that download and retry from the URL above.

## 3. Verify the setup

After the import completes, ask:

```text
Using only the stored Data 8 corpus, explain what tbl.where does. Give me a
hint-sized explanation and cite the lecture or textbook source you used.
```

A useful response should explain the concept, cite course material, and avoid
providing assignment solution code.

## Data and privacy boundaries

Grok Bot stores this corpus on a persistent cloud computer. The
[official FAQ](https://docs.x.ai/grok-bot/faq) notes that every bot on one
account shares that computer, including its files and browser sessions.
Separate bots are therefore not a security boundary.

!!! warning "The archive contains restricted solution material"
    The archive includes solution and answer-key files. The tutor prompt above
    restricts disclosure, but prompt instructions are not a technical access
    control. Do not share the cloud-computer account with students, and do not
    rely on a separate bot to isolate those files.

Grok Bot requires cloud data storage and does not support Legacy Privacy Mode.
Review the account's privacy settings before importing course content.

## Archive licensing

The archive retains its source license and provenance files. Included
materials use a mixture of BSD 3-Clause, CC BY-NC 4.0, and CC BY-NC-ND 4.0
terms. Use the corpus noncommercially, preserve attribution, and consult each
included license before redistributing or modifying its materials.
