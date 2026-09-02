# Slack setup

Follow these steps to create and install the bot on Slack.

1. Open [Slack API Apps](https://api.slack.com/apps).
2. Select **Create New App**, choose **From scratch**, name the app, and select a workspace.
3. Open **Socket Mode** in the left sidebar and enable it.
4. Create an app-level token with the `connections:write` scope.
5. Copy the token beginning with `xapp-` into your `.env` file:

    ```dotenv
    SLACK_APP_TOKEN=your-app-token
    ```

6. Open **OAuth & Permissions** and add these **Bot Token Scopes**:
    - `app_mentions:read`
    - `chat:write`
    - `im:history`
    - `im:read`
    - `im:write`
    - `commands`
7. Select **Install to Workspace** and authorize the requested permissions.
8. Copy the bot token beginning with `xoxb-` into your `.env` file:

    ```dotenv
    SLACK_BOT_TOKEN=your-bot-token
    ```

9. Open **Event Subscriptions**, enable events, and subscribe to these bot events:
    - `app_mention`
    - `message.im`
10. Save the event subscription settings.
11. Open **Slash Commands** and create a `/tutor` command with the description and usage hint you want.
12. Open **App Home**. Under **Show Tabs**, enable **Allow users to send Slash commands and messages from the messages tab**.
13. To add the bot to a channel, enter:

    ```text
    /invite @Your Bot Name
    ```
