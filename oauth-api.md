HOST: https://oauth.edemos.org

# edemos OAuth API
1. [Information](#1-information)
2. [App authorization](#2-app-authorization)
3. [User authorization](#3-user-authorization)
  1. [Common access grant](#31-common-access-grant)
  2. [Simplified access grant](#32-simplified-access-grant)

## 1. Information
*work in progress...*

## 2. App authorization
To use API your app need to authorize and get **client access token**.
Use this call to get one ;)

**URL:** `/token`

**Method:** `POST`

**Parameters:**
* `grant_type = client_credentials`
* `client_id`
* `client_secret`

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
Resources listed below used to get a grant for your app to work with API from behalf of the user.

### 3.1. Common access grant
This is common OAuth2 access grant.

*work in progress...*

### 3.2. Simplified access grant
This is simplified access grant for apps with extended access.

This grant has two steps:

#### 3.2.1. Check users phone

**URL:** `/check-phone`

**Method:** `POST`

**Parameters:**
* `phone` ( *required*, *number* ) - user's phone number
* `method` ( *optional*, *string* ) - method, used to send user a temporary password

**Request:**
```http
POST /check-phone HTTP/1.1
Content-Type: application/x-www-form-urlencoded

phone=71234567890&method=sms
```

**Response**
```http
HTTP/1.1 200 OK
```

#### 3.2.2. Get access token

**URL:** `/token`

**Method:** `POST`

**Parameters:**
* `grant_type = password` ( *required* )
* `username` ( *required*, *string* ) - user's phone number
* `password` ( *required*, *string* ) - user's password

**Request:**
```http
GET /token HTTP/1.1
Content-Type: application/x-www-form-urlencoded

grant_type=password&username=71234567890&password=1q2w3e4r
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"access_token": "1q2w3e4r5t6y7u8i9o0p",
	"token_type": "Owner",
	"expires_in": 43000
}
```