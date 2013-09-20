HOST: https://oauth.edemos.org

# edemos OAuth API
OAuth API

## Contents
1. [Content](#1-content)
	1. [Retrieve news](#Content-GetNews)
	2. [Retrieve news count](#Content-GetNewsCount)
1. [Votings](#2-votings)
2. [Votes](#3-votes)
3. [Apps](#4-apps)

## 1. Retrieving client token

### GET /token

**Parameters:**
* ```grant_type = client_credentials```
* ```client_id```
* ```client_secret```

**Request:**
```http
GET /token HTTP/1.1
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=123&client_secret=123
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"access_token": "1q2w3e4r5t6y7u8i9o0p",
	"token_type": "Client",
	"expires_in": 43000
}
```

## 2. Retrieving auth code
## 3. Retrieving owner token

### Get token POST /token