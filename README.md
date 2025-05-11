# SpanishDict WOTD Discord Bot

A Python-based Discord bot that posts the [SpanishDict Word of the Day](https://www.spanishdict.com/wordoftheday) to a specified Discord channel or thread.

## Features

- ✅ Scrapes the latest Word of the Day from SpanishDict
- 📆 Posts automatically once per day at a configurable UTC time (daemon)
- 🧪 One-shot mode for running from cron instead
- 💬 Sends to a channel or thread
- 🔁 Prevents reposting the same word 


## Usage

### Options

| Option                | Description                                                              |
|-----------------------|--------------------------------------------------------------------------|
| `--channel-id`        | Discord channel ID to post into                                          |
| `--thread-id`         | Discord thread ID to post into (mutually exclusive with `--channel-id`)  |
| `--utc-time HH:MM`    | Time to post in UTC (default is `09:00`, equivalent to 1AM PT)           |
| `--once`, `-o`        | Send the WOTD once and exit (no daemon)                                              |

#### Example

```
DISCORD_TOKEN=your_token_here ./spanishdictwotd --thread-id 987654321098765432 --utc-time 16:30
```

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

## License

MIT

