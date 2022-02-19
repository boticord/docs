# Rust
BoticordRS - is a Rust crate to interact with the Boticord API.
____

### Links:

- [Github-Repository](https://github.com/boticord/boticordrs) 
- [crates.io](https://crates.io/crates/boticordrs) 
- [Documentation](https://docs.rs/boticordrs) 


## Installation

Just add this into your `Cargo.toml`.

```toml
[dependencies]
boticordrs = "0.1.0"
```

## Examples:
**Simple stats posting**

```rs
use boticordrs::{BoticordClient};
use boticordrs::types::{BotStats};

#[tokio::main]
async fn main() {
    let client = BoticordClient::new("your token".to_string()).expect("failed client");

    let stats = BotStats {servers: 2514, shards: 3, users: 338250};

    match client.post_bot_stats(stats).await {
        Ok(_) => {
            println!("Well Done!")
        },
        Err(e) => eprintln!("{}", e),
    }
}
```

You can find other examples [here](https://github.com/boticord/boticordrs/tree/master/examples) (like autoposting).

## Need help?

If you need any help we recommend you to [read documentation](https://docs.rs/boticordrs).

You can find us [here](https://boticord.top/discord). Main Library developer is `@Marakarka#0575`
