FORMAT: X-1A
HOST: https://api.edemos.org

# edemos public API
Public API

# Group Votings

## /votings

### Retrieve votings [GET]

+ Parameters

    + offset = '0' (optional, number) ... The offset from beginning (the newest votings).
    + limit = '5' (optional, number) ... The maximum number of results to return.

+ Request
    
    + Headers

            Authorization: Client {token}

+ Response 200 (application/json)

        {
        "count": 2,
        "votings":[
            {
                "id": 12321,
                "title": "Выборы Перзидента РФ"
            },
            {
                "id": 12322,
                "title": "Выборы в КС"
            }
            ]
        }


### Delete voting [DELETE]
+ Response 204
