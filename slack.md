# Slack
Documentation for how to put the bot on Slack.

--- Slack Side ---
1. Go to api.slack.com/apps
2. Create new app and pick from scratch, naming it and picking the workspace you want it in(can be changed). 
3. Go to socket mode on left sidebar, and turn enable socket mode on. Have the app-level token with connections:write and copy the xapp- into SLACK_APP_TOKEN(or your equivalent) in .env.
4. Go to OAUTH & Permissions in the left sidebar, scroll down to Scopes --> Bot Token Scopes and add OAuth scope for:
  -app_mentions:read
  -chat:write
  -im:history
  -im:read
  -im:write
  -commands
5. Click Install to ___(Workspace Name) and allow the permissions. Then at the same place as the button for installing, copy over the token starting with xoxb- and copy that olver to SLACK_BOT_TOKEN(or your equivalent) in .env.
6. On left sidebar click event subscriptions and turn enable events on, subscribe to bot events:
  -app_mention
  -message.im
then save.
7. On left sidebar click Slach Commands. Create a command called /tutor with whatever description/usage hint you want.
8. On left sidebar click  App home under show tabs enable "Allow users to send Slash commands and messages from the messages tab."
9. To add it in channels write /invite @Data 8 Tutor(or whatever username you gave)