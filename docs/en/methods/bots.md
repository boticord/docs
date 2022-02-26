# Bots

This page lists all API-methods related to bots.
_____


???+ info "GET ```https://api.boticord.top/v1/bot/:shortCode|botID```"

    === "Information"

        **Information about Bot**
    
        This API method will return you information about the bot from the database.
    
    === "Parameters"
    
        | Parameter | Data Type | Description |
        |--------|--------------|----------|
        | `Path` |  String  |  |
        | `shortCode | botID` |  String  |  Short Code or Id of bot  |

    === "Response"
        ??? success "Status-Code: 200 (API successfully returned information about the bot)"
            
            ```json
            {
                id: String,
                shortCode: String || null,
                links: [],
                information: {
                    bumps: Number,
                    added: Number,
                    prefix: String,
                    permissions: Number,
                    tags: [],
                    developers: [],
                    links: {
                        discord: String || null,
                        github: String || null,
                        site: String || null
                    },
                    library: String || null,
                    shortDescription: String || null,
                    longDescription: String || null,
                    badge: String || null,
                    stats: {
                        servers: Number,
                        shards: Number,
                        users: Number
                    },
                    status: String
                }
            }
            ```
        ??? fail "Status-Code: 404 (No results were found for this query)" 
            
            ```json
            {
                error: {
                    code: 404,
                    message: "Bot not found"
                }
            }
            ```


???+ info "GET ```https://api.boticord.top/v1/bot/:botID/comments```"

    === "Information"

        **Bot's comments**
    
        This API method will return list of comments of specified bot.

        !!! warning ""
            **You must specify an API-token to use this method!**
    
    === "Parameters"
    
        | Parameter | Data Type | Description |
        |--------|--------------|----------|
        | `Path` |  String  |  |
        | ` botID` |  String  |  Bot's Id  |

    === "Response"
        ??? success "Status-Code: 200 (The API returned an array of comments)"

            **If a comment has been updated (isUpdated == true), updatedAt will be set instead of createdAt.**
            
            ```json
            [
                {
                    userID: String,
                    text: String,
                    vote: Number,
                    isUpdated: false,
                    createdAt: Number
                },
                {
                    userID: String,
                    text: String,
                    vote: Number,
                    isUpdated: true,
                    updatedAt: Number
                }
            ]
            ```

???+ danger "POST ```https://api.boticord.top/v1/stats```"

    === "Information"

        **Send bot's stats**
    
        This API method takes the number of servers, shards, users and updates bot's statistics.

        **Send JSON-object as a string. Example (JavaScript):**

        `body: JSON.stringify({ servers: 15573, shards: 7, users: 5283954 });`

        !!! warning ""
            **You must specify an API-token to use this method!**
    
    === "Parameters"
    
        | Parameter | Data Type | Description |
        |--------|--------------|----------|
        | `Path` |  String  |  |

    === "Request Body"
    
        | Key | Data Type | Description |
        |--------|--------------|----------|
        | `servers` |  Number  | Bot’s servers count |
        | `shards` |  Number  | Bot’s shards count |
        | `users` |  Number  |  Bot’s users count |

    === "Response"
        ??? success "Status-Code: 200 (Stats updated successfully)"

            **Stats updated successfully (if ok == true).**
            
            ```json
            {
                "ok": true
            }
            ```

