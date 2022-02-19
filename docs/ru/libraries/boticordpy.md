# Python
BoticordPY - это библиотека для взаимодействия с сервисом Boticord.top на языке Python.

____

### Полезные ссылки:

- [Github-Репозиторий](https://github.com/boticord/boticordpy) 
- [PyPi](https://pypi.org/project/boticordpy) 
- [Документация](https://py.boticord.top/) 


## Установка

Используйте одну из этих команд для установки библиотеки:

```
pip install boticordpy
```

```
python3 -m pip install boticordpy
```

```
pip install git+https://github.com/boticord/boticordpy
```

Учтите, что последний вариант установки не гарантирует работоспособность всего функционала библиотеки.

## Примеры работы:
**Автоматическая публикация статистики (discord.py)**

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

**Вебхуки сервиса Boticord (discord.py)**

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

## Нужна помощь?

Если Вам нужна какая-либо помощь, то мы рекомендуем еще раз прочитать [документацию библиотеки](https://py.boticord.top/).

Вы можете найти нас на [сервере поддержки сервиса](https://boticord.top/discord). Разработчик библиотеки `@Marakarka#0575`
