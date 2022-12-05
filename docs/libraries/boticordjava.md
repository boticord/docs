# Java
BotiCordJava - это библиотека для взаимодействия с сервисом BotiCord.top на языке Java.

____

### Полезные ссылки:

- [Github-Репозиторий](https://github.com/boticord/boticordjava) 
- [Jitpack.io](https://jitpack.io/#megoRU/boticordjava)


## Установка

### Maven

Просто добавьте это в свой `pom.xml`.

```xml
<repositories>
 <repository>
    <id>jitpack.io</id>
    <url>https://jitpack.io</url>
 </repository>
</repositories>

<dependency>
    <groupId>com.github.megoRU</groupId>
    <artifactId>boticordjava</artifactId>
    <version>v4.0</version>
</dependency>
```

Другие методы установки можно найти [тут](https://jitpack.io/#megoRU/boticordjava).

## Примеры работы:
**Простая публикация статистики**

```java
public class Main {
    public static void main(String[] args) {
        BotiCordAPI api = new BotiCordAPI.Builder()
                .tokenEnum(TokenEnum.BOT)
                .token("319bbc0e-0743-4d9c-872b-e547d5e8fd0d")
                .build();

        try {
            Result result = api.setStats(500, 1, 2000);
            System.out.println(result);
        } catch (UnsuccessfulHttpException e) {
            System.out.println(e.getMessage());
        }
    }
}
```

**Получать все комментарии по ID бота**

```java
public class Main {
    public static void main(String[] args) {
        BotiCordAPI api = new BotiCordAPI.Builder()
                .tokenEnum(TokenEnum.BOT)
                .token("319bbc0e-0743-4d9c-872b-e547d5e8fd0d")
                .build();

        try {
            Comments[] comments = api.getBotComments("808277484524011531");

            for (int i = 0; i < comments.length; i++) {
                System.out.println(comments[i].getText());
            }
        } catch (UnsuccessfulHttpException e) {
            System.out.println(e.getMessage());
        }
    }
}
```


## WebHooks
```java
public class Main {
    static class Comment extends ListenerAdapter {
        @Override
        public void onCommentEvent(@NotNull CommentAction event) {
            System.out.println(event.getType()); //delete_bot_comment
        }
    }

    static class ServerBumpEvent extends ListenerAdapter {
        @Override
        public void onServerBumpEvent(@NotNull ServerBump event) {
            System.out.println(event.getType()); //new_server_bump
        }
    }

    public static void main(String[] args) {
        WebSocket webSocket = new WebSocket("3fbf63cefsfs2321a", null, 8080);
        webSocket.addListener(new Comment(), new ServerBumpEvent());
    }
}
```

Остальные примеры использования располагаются [здесь](https://github.com/boticord/boticordjava).

## Нужна помощь?

Если Вам нужна какая-либо помощь, то мы рекомендуем подробнее поискать ответы
на ваши вопросы в [репозитории проекта](https://github.com/boticord/boticordjava).

Разработчик библиотеки: [`@mego#5338`](https://boticord.top/profile/250699265389625347)

