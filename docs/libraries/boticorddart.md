# Dart
boticorddart - это библиотека для взаимодействия с сервисом BotiCord.top на языке Dart.

____

### Полезные ссылки:

- [Github-Репозиторий](https://github.com/boticord/boticorddart) 
- [pub.dev](https://pub.dev/packages/boticord) 
- [Документация](https://pub.dev/documentation/boticord/latest/) 


## Установка

Для установки можно использовать следующую команду:

```
dart pub add boticord
```

## Примеры работы:
**Простая публикация статистики**

```dart
import 'package:boticord/boticord.dart';
import 'package:boticord/src/models/botstats.dart';

void main() async {
  final client = BotiCord(
    token: '',
  );

  final BotStats stats = BotStats(
    servers: 150,
    users: null,
    shards: 1
  );

  await client.postBotStats(stats);
}
```

Остальные примеры использования располагаются [здесь](https://github.com/boticord/boticorddart/tree/master/example).

## Нужна помощь?

Если Вам нужна какая-либо помощь, то мы рекомендуем еще раз прочитать [документацию библиотеки](https://pub.dev/documentation/boticord/latest/).

Вы можете найти нас на [сервере поддержки сервиса](https://boticord.top/discord).
Разработчик библиотеки: [`@Marakarka#0575`](https://boticord.top/profile/585766846268047370)
