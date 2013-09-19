FORMAT: X-1A
HOST: https://api.edemos.org

# edemos public API
Public API

# Group Votings

## /votings

+ Headers

        Authorization: Client {client_token}

### Retrieve votings [GET]

+ Parameters

    + offset = '0' (optional, number) ... The offset from beginning (the newest votings).
    + limit = '5' (optional, number) ... The maximum number of results to return.

+ Request
    
    + Headers

            Authorization: Client 1q2w3e4r5t6y7u8i9o0p

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

### Create new voting [POST]

+ Parameters

    + title (required, string) ... Voting title.
    + link (required, string) ... Link to voting page.
    + start_date
    + end_date
    + max_selection
    + has_log
    + anonymous
    + refrain
    + realtime_result
    + custom_options
    + against_all_option

+ Request (application/json)
    
    + Headers

            Authorization: Client 1q2w3e4r5t6y7u8i9o0p

+ Response 201 (application/json)

        {
            "id": 123123
        }
            

## /votings/{id}

+ Headers

        Authorization: Client {token}

+ Parameters

    + id (required) ... Voting id.

### Get voting information [GET]

+ Request (application/json)
    
    + Headers

            Authorization: Client 1q2w3e4r5t6y7u8i9o0p

+ Response 200 (application/json)

        {
            "title": voting["title"],
            "creation_date": voting["creation_date"],
            "start_date": voting["start_date"],
            "end_date": voting["end_date"],
            "state": voting_state(voting["state"]),
            "against_all_option_id": voting["against_all_option_id"],
            "max_selection": voting["max_selection"],
            "has_log": voting["has_log"],
            "anonymous": voting["anonymous"],
            "refrain": voting["refrain"],
            "realtime_result": voting["realtime_result"],
            "custom_options": voting["custom_options"],
            "options": [
                {
                    "id": x["id"],
                    "title": x["title"]
                } for x in voting["options"]
            ]
        }

### Edit voting [POST]

+ Parameters

    + title (required, string) ... Voting title.
    + link (required, string) ... Link to voting page.
    + start_date
    + end_date
    + max_selection
    + has_log
    + anonymous
    + refrain
    + realtime_result
    + custom_options
    + against_all_option

+ Request (application/json)
    
    + Headers

            Authorization: Client 1q2w3e4r5t6y7u8i9o0p

+ Response 200