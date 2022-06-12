# Боты

На этой странице перечислены все API-методы, связанные с ботами.
_____


???+ info "GET ```/bot/:shortCode|botID```"

    === "Информация"

        **Информация о боте**
    
        Этот API-метод выдаст информацию о боте из базы данных.
    
    === "Параметры"
    
        | Параметр | Тип Данных | Описание |
        |--------|--------------|----------|
        | `Путь` |  Строка  |  |
        | `shortCode | botID` |  Строка  |  Короткий домен или ID бота  |

    === "Ответ"
        ??? success "Status-Code: 200 (API успешно вернуло информацию о боте)"
            
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
        ??? fail "Status-Code: 404 (API не нашло в базе данных информацию по указанным данным)" 
            
            ```json
            {
                error: {
                    code: 404,
                    message: "Bot not found"
                }
            }
            ```


???+ info "GET ```/bot/:botID/comments```"

    === "Информация"

        **Комментарии к боту**
    
        Этот API-метод выдаст информацию о комментариях к боту из базы данных.

        !!! warning ""
            **Этот метод требует авторизации!**

            | Версия API | Тип токена |
            |------------|------------|
            | `v1`| `API-токен БОТА`| 
            | `v2`| `Bot`, `PrivateBot`, `Profile` | 
    
    === "Параметры"
    
        | Параметр | Тип Данных | Описание |
        |--------|--------------|----------|
        | `Путь` |  Строка  |  |
        | ` botID` |  Строка  |  ID бота  |

    === "Ответ"
        ??? success "Status-Code: 200 (API вернул в ответ массив с комментариями)"

            **Если комментарий был обновлён (isUpdated == true), вместо createdAt будет отправляться updatedAt.**
            
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

???+ danger "POST ```/stats```"

    === "Информация"

        **Отправка статистики бота**
    
        Этот API-метод принимает количество отправленных вами серверов, шардов и пользователей бота и обновляет его статистику.

        **Отправляйте JSON-объект строкой. Пример (JavaScript):**

        `body: JSON.stringify({ servers: 15573, shards: 7, users: 5283954 });`

        !!! warning ""
            **Этот метод требует авторизации!**

            | Версия API | Тип токена |
            |------------|------------|
            | `v1`| `API-токен БОТА`| 
            | `v2`| `Bot` | 
    
    === "Параметры"
    
        | Параметр | Тип Данных | Описание |
        |--------|--------------|----------|
        | `Путь` |  Строка  |  |

    === "Тело запроса"
    
        | Ключ | Тип Данных | Описание |
        |--------|--------------|----------|
        | `servers` |  Число  | Количество "кешированных" ботом серверов |
        | `shards` |  Число  | Количество шардов |
        | `users` |  Число  | Количество "кешированных" ботом пользователей |

    === "Ответ"
        ??? success "Status-Code: 200 (Статистика бота обновлена)"

            **Статистика бота обновлена (если ok == true).**
            
            ```json
            {
                "ok": true
            }
            ```

