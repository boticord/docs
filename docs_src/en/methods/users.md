# Users

This page lists all API-methods related to users profiles.
_____

???+ info "GET ```https://api.boticord.top/v1/profile/:userID```"

    === "Information"

        **Information about the user profile**
    
        This method returns information about the user with the specified Discord-Id.
    
    === "Parameters"
    
        | Parameter | Data Type | Description |
        |--------|--------------|----------|
        | `Path` |  String  |   |
        | `userID` |  String  | Id of the Discord user  |

    === "Response"
        ??? success "Status-Code: 200 (API successfully returned information about the user)"
            
            ```json
            {
                "id": '178404926869733376',
                "status": '"Если вы не разделяете мою точку зрения, поздравляю — вам больше достанется." © Артемий Лебедев',
                "badge": 'STAFF',
                "shortCode": 'cipherka',
                "site": 'https://sqdsh.top/',
                "vk": null,
                "steam": 'sadlycipherka',
                "youtube": null,
                "twitch": null,
                "git": 'https://git.sqdsh.top/me'
            }
            ```
        ??? fail "Status-Code: 404 (No results were found for this query)" 
            
            ```json
            {
                "error": {
                    "code": 404,
                    "message": "Profile not found"
                }
            }
            ```

???+ info "GET ```https://api.boticord.top/v1/profile/:userID/comments```"

    === "Information"

        **User's comments**
    
        This API method will return list of comments by specified user..

        !!! warning ""
            **You must specify an API-token to use this method!**
    
    === "Parameters"
    
        | Parameter | Data Type | Description |
        |--------|--------------|----------|
        | `Path` |  String  |   |
        | `userID` |  String  | Id of the user  |

    === "Response"
        ??? success "Status-Code: 200 (The API returned to arrays of comments)"
            
            ```json
            {
                "bots": ['data from /v1/bot/:botID/comments'],
                "servers": ['data from /v1/server/:serverID/comments']
            }
            ```

???+ info "GET ```https://api.boticord.top/v1/bots/:userID```"

    === "Information"

        **List of user's bots**

        !!! warning ""
            **You must specify an API-token to use this method!**
    
    === "Parameters"
    
        | Parameter | Data Type | Description |
        |--------|--------------|----------|
        | `Path` |  String  |   |
        | `userID` |  String  | Id of the user  |

    === "Response"
        ??? success "Status-Code: 200 (API will return an array with bot's Ids and short codes)"
            
            ```json
            [
                {
                    "id":"672406367344132116",
                    "shortCode":"sonata"
                }
            ]
            ```
