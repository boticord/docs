# Сервера

На этой странице перечислены все API-методы, связанные с серверами.
_____


???+ info "GET ```/server/:shortCode|serverID```"

    === "Информация"

        **Информация о сервере**
    
        Этот API-метод выдаст информацию о сервере из базы данных.
    
    === "Параметры"
    
        | Параметр | Тип Данных | Описание |
        |--------|--------------|----------|
        | `Путь` |  Строка  |   |
        | `shortCode | serverID` |  Строка  |  Короткий домен или ID сервера  |

    === "Ответ"
        ??? success "Status-Code: 200 (API успешно вернуло информацию о сервере)"
            
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
        ??? fail "Status-Code: 404 (API не нашло в базе данных информацию по указанным данным)" 
            
            ```json
            {
                error: {
                    code: 404,
                    message: "Server not found"
                }
            }
            ```


???+ info "GET ```/server/:serverID/comments```"

    === "Информация"

        **Комментарии к серверу**
    
        Этот API-метод выдаст информацию о комментариях к серверу из базы данных.

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
        | ` serverID` |  Строка  |  ID сервера  |

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

???+ danger "POST ```/server```"

    === "Информация"

        **Отправка статистики о сервере**
    
        Запрос на обновление статистики о сервере (есть-ли бот на сервере, название сервера, его аватарка, количество всех/в сети участников, ID владельца сервера)

        !!! warning ""
            **Этот метод требует авторизации!**

            | Версия API | Тип токена |
            |------------|------------|
            | `v1`| `API-токен БОТА` (**ТРЕБУЕТСЯ БЫТЬ СЕРВИСНЫМ БОТОМ**) | 
            | `v2`| `Bot` (**ТРЕБУЕТСЯ БЫТЬ СЕРВИСНЫМ БОТОМ**), `PrivateBot` (только на разрешённых пяти серверах) |
    
    === "Параметры"
    
        | Параметр | Тип Данных | Описание |
        |--------|--------------|----------|
        | `Путь` |  Строка  |  |

    === "Тело запроса"
    
        | Обязательно? | Ключ | Тип Данных | Описание |
        |------|--------|--------------|----------|
        | Да | `serverID` |  Строка  | ID сервера |
        | Да | `up` |  Число  | Тип запроса: |
        | | | |                        - 0: просто обновление статистики (в данном случае вывод ответа не требуется) |
        | | | |                        - 1: вместе с обновлением статистики добавляется 1 АП (если это возможно) |
        | Да | `status` |  Число  | Статус сервера: |
        | | | |                        - 0: бота нет на сервере |
        | | | |                        - 1: бот есть на сервере |
        | Нет | `serverName` |  Строка  | Название сервера (если указано - после каждого запроса будет изменяться) |
        | Нет | `serverAvatar` |  Строка  | Аватарка сервера (если указано - после каждого запроса будет изменяться) |
        | Нет | `serverMembersAllCount` |  Число  | Общее количество участников на сервере (если указано - после каждого запроса будет обновляться) |
        | Нет | `serverMembersOnlineCount` |  Число  | Количество участников в сети на сервере (если указано - после каждого запроса будет обновляться) |
        | Нет | `serverOwnerID` |  Строка  | ID владельца сервера (если указано - после каждого запроса будет обновляться) |
        | Нет | `serverOwnerTag` |  Строка  | Тег владельца сервера (если указано - после каждого запроса будет обновляться) |
        | Да | `upUserID`      |  Строка  | ID пользователя, который поднял сервер |
        | Да | `upChannelID`   |  Строка  | ID канала, в котором пользователь активировал триггер поднятия сервера |
        | Да | `upChannelName` |  Строка  | Название канала, в котором пользователь активировал триггер поднятия сервера |

    === "Ответ"
        ??? success "Status-Code: 200 (Смотреть подробнее*)"

            `updated = true` говорит о статусе обновления информации, `updated = false` означает что что-то пошло не так. Дополнительная информация возвращается в `message` как будущее сообщение бота.
            
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

        ??? fail "Status-Code: 401 (Скорее всего, вы неверно указали API-токен.)" 
            
            ```json
            {
                "error": {
                    "code": 401,
                    "message": "Unauthorized"
                }
            }
            ```

        ??? fail "Status-Code: 403 (Эта ошибка вызывается только для приватных ботов: сервер, которому хотят обновить информацию, недоступен для владельца токена.)" 
            
            ```json
            {
                "error": {
                    "code": 403,
                    "message": "Forbidden"
                }
            }
            ```
