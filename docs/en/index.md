# Home
Welcome to the BotiCord API (`[v1]`) documentation!
____

## Domains Table

|      Description      |       Domain      |
| ------------------ | -----------------|
|     Website   |   boticord.top   |
|   Internal API   | boticord.top/api |
| Main API `[v1]` | api.boticord.top/v1 |

## Authorization
A lot of methods requires to provide an authorization API-token.
In http requests you can set it in `headers` like this:

|      headers      |       value     |
| ------------------ | -----------------|
|   Authorization   |   API-токен   |

## How to get an API-token?
To get an API-token you need to [add your bot to the website](https://boticord.top/add). After its verification you can use all the features of the BotiCord Service. Then go to the edit page (of your bot).

![go down to the button `Управление`, there will be your token.](https://media.discordapp.net/attachments/928734933814497343/944137133566873610/assets2F-MTA7c_niON-8K1DJnTo2F-MTABScExbNNnpikgHHy2F-MTAC6usAOw1DVq4gq1z2Fimage.png)

## Ratelimits

!!! danger "What will exceeding the limits lead to?"

    Exceeding the Limits will result in temporary blocking of access to the resource! If abused frequently, **access may be permanently restricted.**

### Limits

| Route  | Limit |  Retry after |
| ------|-------|----------------|
| `*` | `5/5 s` | `5 s` |
| `/v1/server` | `1/2 s` | `2 s` |
| `/v1/stats` | `1/2 s` | `2 s` |

!!! warning "Recommendations"

    * Don't set posting stats interval lower than 900 seconds!
    * Try not to reach the limits.


