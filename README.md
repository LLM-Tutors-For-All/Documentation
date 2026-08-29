# discord
Documentation for how to put the bot on discord.

--- Discord Side ---
1. Go to discord.com/developers/applications
2. Create a new applicatoin and give it it's name.
3. In the left sidebar go to bot and copy the token. If you don't have a token, just click reset token and then it would generate a new one.
4. Add this to your .env as DISCORD_BOT_TOKEN or the variable you chose to name it.
5. Still on the bot page enable message content intent and save.
6. Now in the left sidebar go to OAuth2. For scopes check:
  -bot
  -applications.commands
7. For bot permissions check:
  -View Channels
  -Send Messages
  -Send Messages in Threads
  -Read Message History
  -Embed Links
  -Use slash Commands
  --anything else you want specifically.
8. Copy over the Generated URL, this is the invite link that you can share out. For you specifically just open up a new tab and paste it. Sign in to discord and then add it to the server you want. After you authorize it, it should now be functional on your server when on.