# Tutor Options

The project offers one Data 8 tutor through three self-hosted interfaces and a
Grok Bot template. The self-hosted options share the same course corpus,
retrieval system, and tutoring engine; Grok Bot keeps its own corpus on a
persistent cloud computer.

## Choose an interface

<div class="option-gallery">

<a class="option-card option-card--compact" href="interfaces/local-cli/">
  <div class="option-card__body">
    <div class="option-card__heading">
      <img class="option-card__logo" src="../assets/gallery/cli.png" alt="">
      <h3>Local CLI</h3>
    </div>
    <p>Run one-shot questions, interactive chat, retrieval checks, and staff mode.</p>
  </div>
</a>

<a class="option-card option-card--compact" href="interfaces/discord/">
  <div class="option-card__body">
    <div class="option-card__heading">
      <img class="option-card__logo" src="../assets/gallery/discord.png" alt="">
      <h3>Discord</h3>
    </div>
    <p>Let students ask through mentions, direct messages, or the tutor command.</p>
  </div>
</a>

<a class="option-card option-card--compact" href="interfaces/slack/">
  <div class="option-card__body">
    <div class="option-card__heading">
      <img class="option-card__logo" src="../assets/gallery/slack.png" alt="">
      <h3>Slack</h3>
    </div>
    <p>Use mentions, direct messages, or the tutor command through Socket Mode.</p>
  </div>
</a>

<a class="option-card option-card--compact" href="interfaces/grok-bot/">
  <div class="option-card__body">
    <div class="option-card__heading">
      <img class="option-card__logo" src="../assets/gallery/grok.jpg" alt="">
      <h3>Grok Bot</h3>
    </div>
    <p>Add the hosted template. On first use it sets up the Spring 2026 materials on its own.</p>
  </div>
</a>

</div>

The local CLI, Discord, and Slack options currently use the same Data 8 course
corpus and OpenRouter brain. The configured OpenRouter model can be changed
without changing those interfaces or their retrieval pipeline. Grok Bot is a
separate hosted option with its own plan, usage, storage, and privacy terms.
