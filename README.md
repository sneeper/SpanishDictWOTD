# SpanishDict WOTD Discord Bot

A Python-based Discord bot that posts the [SpanishDict Word of the Day](https://www.spanishdict.com/wordoftheday) to a specified Discord channel or thread.

![](./SpanishDictWOTD_example.png)

## Features

- ✅ Scrapes the latest Word of the Day from SpanishDict
- 📆 Posts automatically once per day at a configurable UTC time (daemon)
- 🧪 One-shot mode for running from cron instead
- 💬 Sends to a channel or thread
- 🔁 Prevents reposting the same word 


## Usage

#### Example

```
DISCORD_TOKEN=your_token_here 
./spanishdictwotd --thread-id 987654321098765432 --utc-time 16:30
```

### Options

| Option                | Description                                                              |
|-----------------------|--------------------------------------------------------------------------|
| `--channel-id`        | Discord channel ID to post into                                          |
| `--thread-id`         | Discord thread ID to post into (mutually exclusive with `--channel-id`)  |
| `--utc-time HH:MM`    | Time to post in UTC (default is `09:00`, equivalent to 1AM PT)           |
| `--once`, `-o`        | Send the WOTD once and exit (no daemon)                                              |

**NOTE**: The script writes to `sent_wotd.txt` in the same directoryto avoid sending duplicate words. The user running the script must have write access to the file (and the directory if the file does not exist to create it). 


## Authentication

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

## Bot Setup

1.	Go to the [Discord Developer Portal](https://discord.com/developers/applications) and click New Application.

2.	Under Bot, click Add Bot, then copy its TOKEN.

3.	Under OAuth2 → URL Generator, grant it the `bot` scope and the `Send Messages` permission, then visit the generated URL to invite it into your server.  

### Run bot on a server on in a Cloud
* Locally with a cron job (e.g. run the script once a day), or
* Hosted on Heroku / Railway / AWS Lambda / a VPS, where the bot runs 24/7 and sleeps between tasks.

How to do that is well beyond the scope of this document.


## License

MIT

