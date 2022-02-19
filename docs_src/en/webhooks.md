# Webhooks

Get real-time information from the Boticord API.
_____

## How to work with it?

The first thing you must do is set up a link to the webhook. You can do it on the bot/server edit page. After setting up the link, on the same page, under the webhook link field, you can copy private key that will be sent in Headers as **X-Hook-Key** (to check the authorization).

![Picture](https://media.discordapp.net/attachments/928734933814497343/944487720699441192/assets2F-MTA7c_niON-8K1DJnTo2F-MjiBik8Bs-fMOJgByRd2F-MjiCGt9_B_2DfWSioHg2Fimage.png)

## And what to do next?

Next, just accept messages from the Boticord. It requires you to setup your own HTTP server.

### What should I use from it? 

Our list of recommendation libs:

* Python - [aiohttp](https://docs.aiohttp.org/en/stable/), [Flask](https://flask.palletsprojects.com/en/2.0.x/) **or [BoticordPY Webhooks](https://py.boticord.top/)**.
* Node.js - [Fastify](https://www.fastify.io) or `http`/`https`
* Rust - [warp](https://github.com/seanmonstar/warp)

## List of events:

|    Boticord Events     |             Description           |
|--------------------|-------------------------------------------|
|    new_bot_comment     |      On new bot comment        |
|    edit_bot_comment    | On bot comment edit      |
|   delete_bot_comment   |     On bot comment delete    |
|      new_bot_bump      |    On new bot bump      |
|   new_server_comment   |   On new server comment     |
|   edit_server_comment  |   On server comment edit   |
|  delete_server_comment |   On server comment delete  |

## Response Data examples:

### Bot Bump

```json
{
    "type": "new_bot_bump",
    "data": {
        "user": "178404926869733376",
        "at": 1631789378024
    }
}
```

### Action with comment

```
{
    "type": "*_*_comment", // Types provided in list
    "data": {
        "user": "178404926869733376",
        "comment": {
            "vote": {
                "old": -1 | null,
                "new": 1 | null
            },
            "old": "Плохой бот!" | null,
            "new": "Лучший бот среди всех ботов и времён!" | null
        },
        "reason": "self" | "moderation", // If comment has been deleted
        "at": 1631789378024
    }
}
```

