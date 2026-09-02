# Discord setup

Follow these steps to create and install the bot on Discord.

1. Open the [Discord Developer Portal](https://discord.com/developers/applications).
2. Select **New Application**, enter a name, and create the application.
3. Open **Bot** in the left sidebar.
4. Copy the bot token. If no token is available, select **Reset Token** to generate one.
5. Store the token in your `.env` file:

    ```dotenv
    DISCORD_BOT_TOKEN=your-token
    ```

6. On the **Bot** page, enable **Message Content Intent**, then save your changes.
7. Open **OAuth2** in the left sidebar.
8. Under **OAuth2 URL Generator**, enable these scopes:
    - `bot`
    - `applications.commands`
9. Enable these bot permissions:
    - View Channels
    - Send Messages
    - Send Messages in Threads
    - Read Message History
    - Embed Links
    - Use Slash Commands
    - Any additional permissions required by your bot
10. Copy the generated URL and open it in a browser.
11. Select the server, authorize the application, and complete any verification prompt.

The bot will be available in the selected server whenever its application is running.
