# .NET
Boticord.Net - это библиотека для взаимодействия с сервисом BotiCord.top на языке C#.

____

### Полезные ссылки:

- [Github-Репозиторий](https://github.com/boticord/Boticord.Net) 
- [Документация](https://alxelzot.gitbook.io/boticord.net/quick-start)
- [Nuget](https://www.nuget.org/packages/Boticord.Net/)


## Установка
### Для установки используйте:

```dotnet add package Boticord.Net --version 1.0.3```

Другие методы установки можно найти [тут](https://www.nuget.org/packages/Boticord.Net/).

## Примеры работы:
**Простая публикация статистики**

```cs
using Discord.WebSocket;
using Discord;
using Boticord.Net;


var boticordClient = new BoticordClient(new BoticordConfig
{
    Token = "boticord token here"
});

var botClient = new DiscordSocketClient();
botClient.Ready += BotReady;
botClient.Log += BotLog;

await botClient.LoginAsync(TokenType.Bot, "bot token here");
await botClient.StartAsync();

await Task.Delay(-1);

async Task BotReady()
{
    Console.WriteLine($"Logged into {botClient.CurrentUser}");

    _ = Task.Run(() => AutoUpdateBotStatus());

}

async Task AutoUpdateBotStatus()
{
    var timer = new PeriodicTimer(TimeSpan.FromMinutes(1));

    while (true)
    {
        await boticordClient.SendBotStatsAsync((uint)botClient.Guilds.Count,
            users: (uint)botClient.Guilds.Select(x => x.MemberCount).Sum());
        await timer.WaitForNextTickAsync();
    }
}

async Task BotLog(LogMessage message)
{
    Console.WriteLine(message.Message);
}    
```

Остальные примеры использования располагаются [здесь](https://github.com/boticord/Boticord.Net).

## Нужна помощь?

Если Вам нужна какая-либо помощь, то мы рекомендуем подробнее поискать ответы
на ваши вопросы в [репозитории проекта](https://github.com/boticord/Boticord.Net).

Разработчик библиотеки: [`@Zont1k#5100`](https://boticord.top/profile/564380749873152004), [`@Misha133#9748`](https://boticord.top/profile/394209945513361408)
