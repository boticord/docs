# Python
boticordpy is a Python library to interact with the BotiCord API.

____

### Links:

- [Github-Repository](https://github.com/boticord/boticordpy) 
- [PyPi](https://pypi.org/project/boticordpy) 
- [Documentation](https://py.boticord.top/) 


## Installation

Enter one of these commands to install the library:

```
pip install boticordpy
```

```
python3 -m pip install boticordpy
```

```
pip install git+https://github.com/boticord/boticordpy
```

Note that the last installation option (from git) does not guarantee full functionality of the library.

## Examples:
**Stats autoposting (discord.py)**

```py
from discord.ext import commands
from boticordpy import BoticordClient

bot = commands.Bot(command_prefix="!")


async def get_stats():
    return {"servers": len(bot.guilds), "shards": 0, "users": len(bot.users)}


async def on_success_posting():
    print("stats posting successfully")

boticord_client = BoticordClient("your_api_token")
autopost = (
    boticord_client.autopost()
    .init_stats(get_stats)
    .on_success(on_success_posting)
    .start()
)

bot.run("bot token")
```

**Boticord Webhooks (discord.py)**

```py
from discord.ext import commands

from boticordpy import webhook

bot = commands.Bot(command_prefix="!")


async def edit_bot_comment(data):
    print(data.comment.new)

boticord_webhook = webhook.Webhook("x-hook-key", "bot").register_listener("edit_bot_comment", edit_bot_comment)
boticord_webhook.start(5000)

bot.run("bot token")
```

## Need help?

If You need any help we recommend you to check the documentation. You can find us [here](https://boticord.top/discord). Main developer is `Marakarka#0575`
