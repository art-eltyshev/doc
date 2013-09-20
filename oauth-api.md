HOST: https://oauth.edemos.org

# edemos OAuth API
OAuth API

## Contents
1. [Information](#1-information)
2. [App authorization](#2-app-authorization)
3. [User authorization](#)
  1. [Common access grant](#)
  2. [Simplified access grant](#)

## 1. Information

## 2. App authorization
Retrieving client access token:

**URL:** ```GET /token```

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
## 3. User authorization
### 3.1. Common access grant
### 3.2. Simplified access grant