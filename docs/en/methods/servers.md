# Servers

This page lists all API-methods related to servers.
_____


???+ info "GET ```https://api.boticord.top/v1/server/:shortCode|serverID```"

    === "Information"

        **Information about the server**
    
        ЭThis API method will return you information about the server from the database.
    
    === "Parameters"
    
        | Parameter | Data Type | Description |
        |--------|--------------|----------|
        | `Path` |  String  |   |
        | `shortCode | serverID` |  String  |  Short Code or Id of server  |

    === "Response"
        ??? success "Status-Code: 200 (API successfully returned information about the server)"
            
            ```json
            {
                id: String,
                shortCode: String || null,
                status: String,
                links: [],
                information: {
                    name: String,
                    avatar: String,
                    members: [Number, Number], // [all, online]
                    owner: String,
                    bumps: Number,
                    tags: [],
                    links: {
                        invite: String || null,
                        site: String || null,
                        youtube: String || null,
                        twitch: String || null,
                        steam: String || null,
                        vk: String || null
                    },
                    shortDescription: String || null,
                    longDescription: String || null,
                    badge: String || null
                }
            }
            ```
        ??? fail "Status-Code: 404 (No results were found for this query)" 
            
            ```json
            {
                error: {
                    code: 404,
                    message: "Server not found"
                }
            }
            ```


???+ info "GET ```https://api.boticord.top/v1/server/:serverID/comments```"

    === "Information"

        **Server's comments**
    
        This API method will return list of comments of specified server.

        !!! warning ""
            **You must specify an API-token to use this method!**
    
    === "Parameters"
    
        | Parameter | Data Type | Description |
        |--------|--------------|----------|
        | `Path` |  String  |  |
        | ` serverID` |  String  |  Id of the server  |

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

???+ danger "POST ```https://api.boticord.top/v1/server```"

    === "Information"

        **Send server's stats**
    
        This API method takes information about the server and updates it on Boticord.

        !!! warning ""
            **You must specify an API-token to use this method! (YOU MUST BE A BOTICORD-SERVICE BOT)**
    
    === "Parameters"
    
        | Parameter | Data Type | Description |
        |--------|--------------|----------|
        | `Path` |  String   |  |

    === "Request Body"
    
        | Required? | Key | Data Type | Description |
        |------|--------|--------------|----------|
        | Yes | `serverID` |  String  | Id of server |
        | Yes | `up` |  Number  | Type of request: |
        | | | |                        - 0: Update information about the server |
        | | | |                        - 1: Update information about the server and up it |
        | Yes | `status` |  Number  | Status of server: |
        | | | |                        - 0: there is a bot on the server |
        | | | |                        - 1: there isn't bot on the server |
        | No | `serverName` |  String  | Name of the server (if specified - will be changed) |
        | No | `serverAvatar` |  String  | Avatar of the server (if specified - will be changed) |
        | No | `serverMembersAllCount` |  Number  | Total number of users (if specified - will be changed) |
        | No | `serverMembersOnlineCount` |  Number  | Number of currently online users (if specified - will be changed) |
        | No | `serverOwnerID` |  String  | Id of the server owner (if specified - will be changed) |

    === "Response"
        ??? success "Status-Code: 200"

            `updated = true` means that information updated successefully, `updated = false` means something went wrong. Additional information is returned to `message` as a future bot message.
            
            ```json
            {
                "serverID": "722424773233213460",
                "up": 1,
                "updated": true,
                "bumps": 2,
                "boost": true,
                "upSuccessfully": true,
                "timeToNextUpInMs": 1641589230690,
                "message": ":white_check_mark: Серверу было успешно добавлено **2 UP**!\n\nℹ️Вы также можете оставить отзыв о сервере!\n> https://myservers.me/s/boticord"
            }
            ```

        ??? fail "Status-Code: 401 (Most likely, you specified the API-token incorrectly.)" 
            
            ```json
            {
                "error": {
                    "code": 401,
                    "message": "Unauthorized"
                }
            }
            ```

        ??? fail "Status-Code: 403 (This error is caused only for private bots: the server that wants to update the information is unavailable to the owner of the API-token.)" 
            
            ```json
            {
                "error": {
                    "code": 403,
                    "message": "Forbidden"
                }
            }
            ```
