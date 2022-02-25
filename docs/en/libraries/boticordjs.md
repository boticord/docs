# JavaScript
boticord.js - is a JavaScript (TypeScript) library to interact with the BotiCord API.

____

### Links:

- [Github-Repository](https://github.com/boticord/boticord.js) 
- [NPM](https://www.npmjs.com/package/boticord.js) 
- [Documentation](https://js.boticord.top/)


!!! note "READ IT PLEASE!"

    - The library supports `discord.js`, `Eris`, `Discordoo`, but you may not use them.
    - If you have typescript in your project, please enable `skipLibCheck` property in your `tsconfig.json`


## Installation
```
npm i boticord.js
```

## Examples:

**Stats autoposting  (discord.js)**

```ts
import { Client as BotiCord, DjsAdapter } from '../../src' // from 'boticord.js'
const client: any = {} // Discord.js client

const adapter = new DjsAdapter(client) // pass djs client to adapter

const boticord = new BotiCord({
  token: 'YOUR_BOTICORD_API_TOKEN',
  apiVersion: 1
}, adapter)

boticord.botStatsAutopost()
  .then(success => {
    if (success) console.log('autopost started successfully!')
    else console.log('autopost already running')
  })
  .catch(error => {
    console.log('whoops, some error occurred!', error)
  })
```

**Simple stats posting**

```ts
import { Client as BotiCord } from '../src' // from 'boticord.js'

const boticord = new BotiCord({
  token: 'YOUR_BOTICORD_API_TOKEN',
  apiVersion: 1
})

boticord.bots.postStats({ servers: 123, users: 12345, shards: 1 })
  .then(success => {
    console.log('posted bot stats! success?', success)
  })
```

You can find other examples [here](https://github.com/boticord/boticord.js/tree/master/examples).

## Need help?

If you need any help we recommend you to [read documentation](https://js.boticord.top/).

You can find us [here](https://boticord.top/discord). Main Library developer is `@san4ouZ#1007`
