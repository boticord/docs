# Rust
boticordrs - это библиотека для взаимодействия с сервисом BotiCord.top на языке Rust.

____

### Полезные ссылки:

- [Github-Репозиторий](https://github.com/boticord/boticordrs) 
- [crates.io](https://crates.io/crates/boticordrs) 
- [Документация](https://docs.rs/boticordrs) 


## Установка

Просто добавьте это в свой `Cargo.toml`.

```toml
[dependencies]
boticordrs = "0.1.3"
```

## Примеры работы:
**Простая публикация статистики**

```rs
use boticordrs::{BoticordClient};
use boticordrs::types::{BotStats};

#[tokio::main]
async fn main() {
    let client = BoticordClient::new("Bot YOUR_TOKEN".to_string(), 2).expect("failed client");

    let stats = BotStats {servers: 2514, shards: 3, users: 338250};

    match client.post_bot_stats(stats).await {
        Ok(_) => {
            println!("Well Done!")
        },
        Err(e) => eprintln!("{}", e),
    }
}
```

Остальные примеры использования располагаются [здесь](https://github.com/boticord/boticordrs/tree/master/examples) (например авто-постинг).

## Нужна помощь?

Если Вам нужна какая-либо помощь, то мы рекомендуем еще раз прочитать [документацию библиотеки](https://docs.rs/boticordrs).

Вы можете найти нас на [сервере поддержки сервиса](https://boticord.top/discord).
Разработчик библиотеки: [`@Marakarka#0575`](https://boticord.top/profile/585766846268047370)
