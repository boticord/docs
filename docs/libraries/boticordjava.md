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
    <version>v2.8</version>
</dependency>
```

Другие методы установки можно найти [тут](https://jitpack.io/#megoRU/boticordjava).

## Примеры работы:
**Простая публикация статистики**

```java
public static void main(String[] args) {

    BotiCordAPI api = new BotiCordAPIImpl("YOUR_TOKEN", "BOT_ID");

    int servers = ...; // the server count
    int shards = ...; // shards count
    int users = ...; // the amount of users

    api.setStats(servers, shards, users);
}    
```

Остальные примеры использования располагаются [здесь](https://github.com/boticord/boticordjava).

## Нужна помощь?

Если Вам нужна какая-либо помощь, то мы рекомендуем подробнее поискать ответы
на ваши вопросы в [репозитории проекта](https://github.com/boticord/boticordjava).

Разработчик библиотеки: [`@mego#5338`](https://boticord.top/profile/250699265389625347)

