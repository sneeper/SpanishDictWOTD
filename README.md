# 📚 Word of the Day Poster

A lightweight Python script that fetches the **Word of the Day** from [SpanishDict](https://www.spanishdict.com/wordoftheday) or [FrenchDictionary](https://frenchdictionary.com/wordoftheday) and posts it to a Discord channel via a **webhook**.

## 🔧 Features

- ✅ Supports both Spanish and French word feeds
- ✅ Posts to Discord using webhooks (no bot login needed)
- ✅ Automatically avoids duplicate posts with a history file
- ✅ `--dry-run` mode for testing
- ✅ Cron-compatible for daily automation

---

## 🚀 Usage

### 🖥️ Command Line

```bash
python3 wotd_post.py --webhook-url <URL> --lang spanish
```

Or set the webhook via environment variable:

```
export DISCORD_WEBHOOK="https://discord.com/api/webhooks/..."
python3 wotd_post.py --lang french
```


### ⚙️ Options


| Option                | Short  | Default                                                     | Description                |
|-----------------------|--------|-----------------------------------------------------------------|------------------------|
| `--webhook-url <URL>` | `-w`   | `$DISCORD_WEBHOOK` |Discord incoming webhook URL to post into   |
| `--lang <language>` | `-l`   | spanish | Language source to use (spanish or french) |
| `--history-file <PATH>` | `-f`   | `sent_wotd.txt` | File to track previously posted words |
| `--dry-run` | | *disabled* | Print the embed payload instead of posting |


**NOTE**: The script writes to `sent_wotd.txt` in the same directoryto avoid sending duplicate words. The user running the script must have write access to the file (and the directory if the file does not exist to create it). 


## Requirements

- Python 3.9+

Install dependencies with:

```bash
pip install -r requirements.txt
```

## License

MIT

