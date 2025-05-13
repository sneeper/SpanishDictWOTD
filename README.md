# SpanishDict WOTD Discord Bot

A Python-based Discord bot that posts the [SpanishDict Word of the Day](https://www.spanishdict.com/wordoftheday) to a specified Discord channel or thread.

![](./SpanishDictWOTD_example.png)

## Features

- ✅ Scrapes the latest Word of the Day from SpanishDict
- 📆 Posts automatically once per day at a configurable UTC time (daemon)
- 🧪 One-shot mode for running from cron instead
- 💬 Sends to a channel or thread
- 💬 Sends to a channel or thread via Bot token
- 🔗 Sends via Discord Incoming Webhook (env or CLI)
- 🔁 Prevents reposting the same word 


## Usage

#### Example (webook mode + one time)

```
DISCORD_WEBHOOK_URL=https://discord.com/api/webhooks/123456/fooobar
./spanishdictwotd --once
```


#### Example (bot mode)

```
DISCORD_TOKEN=your_token_here 
./spanishdictwotd --thread-id 987654321098765432 --utc-time 16:30
```

### Options


| Option                | Short  | Description                                                     | Default                | Notes                                                           |
|-----------------------|--------|-----------------------------------------------------------------|------------------------|-----------------------------------------------------------------|
| `--once`              | `-o`   | Send the WOTD once and exit (no daemon)                         | `false`                | Omit for daemon mode                                            |
| `--channel-id <ID>`   | `-c`   | Discord channel ID to post into                                 | _none_                 | Mutually exclusive with `--thread-id` & `--webhook-url`         |
| `--thread-id <ID>`    | `-t`   | Discord thread ID to post into                                  | _none_                 | Mutually exclusive with `--channel-id` & `--webhook-url`        |
| `--webhook-url <URL>` | `-w`   | Discord incoming webhook URL to post into                       | `$DISCORD_WEBHOOK_URL` | Mutually exclusive with `--channel-id` & `--thread-id`          |
| `--utc-time <HH:MM>`  | `-u`   | Daily send time in UTC (e.g. `16:30`)                           | `09:00`                | Only applies in daemon mode                                    | 
| `--history-file <PATH>` | `-f`   | Path to the history file                                 | `sent_wotd.txt`         | Override default; allows separate histories per target |

- Daemon (default): runs continuously and posts once per day at --utc-time.
- One-shot (--once): posts immediately and exits.

**NOTE**: The script writes to `sent_wotd.txt` in the same directoryto avoid sending duplicate words. The user running the script must have write access to the file (and the directory if the file does not exist to create it). 


## Authentication (bot mode)

The bot looks for a Discord token in:

1.	The `DISCORD_TOKEN` environment variable
1.	A `.token` file in the same directory

## Requirements

- Python 3.9+
- A Discord bot token
- Discord.py and supporting libraries

Install dependencies with:

```bash
pip install -r requirements.txt
```

## Webhook Method 

Use a Discord incoming webhook instead of a Bot token. 

**1. Create your webhook**  
   - In Discord, open Server Settings → Integrations → Webhooks → **New Webhook**.  
   - Choose channel/thread, give it a name, then 

**Copy Webhook URL**.

**2. Enable in the bot**  
   - **Env var**:  
     ```bash
     export DISCORD_WEBHOOK_URL="https://discord.com/api/webhooks/…"
     ```  
   - **Or CLI flag**:  
     ```bash
     ./spanishdictwotd --webhook-url https://discord.com/api/webhooks/… [other flags]
     ```

**3. Choose one-shot vs. daemon**  
   - `--once` (or cron): post immediately, then exit.  
   - (default) no `--once`: run 24/7 and post at `--utc-time` (defaults to 09:00 UTC).

**4. (Optional) Schedule time**  
   ```bash
   ./spanishdictwotd.py --webhook-url … --utc-time 16:30
   ```
   Posts daily at 16:30 UTC; omit `--once` for daemon.


## Bot Method 

Set 

### Bot Setup 

1.	Go to the [Discord Developer Portal](https://discord.com/developers/applications) and click New Application.

2.	Under Bot, click Add Bot, then copy its TOKEN.

3.	Under OAuth2 → URL Generator, grant it the `bot` scope and the `Send Messages` permission, then visit the generated URL to invite it into your server.  

### Run bot on your server or on a Cloud platform
* Locally with a cron job (e.g. run the script once a day), or
* Hosted on Heroku / Railway / AWS Lambda / a VPS, where the bot runs 24/7 and sleeps between tasks.

How to do that is well beyond the scope of this document.


## License

MIT

