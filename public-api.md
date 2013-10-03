# public API
1. [Information](#1-information)
2. [Content](#2-content)
  1. [Get news](#21-get-news-get-news) `GET /news`
  2. [Get news count](#22-get-news-count-get-newscount) `GET /news/count`
  3. [Get banner](#23-get-banner-get-banner) `GET /banner`
3. [Votings](#3-votings)
  1. [Get votings](#31-get-votings-get-votings) `GET /votings`
  2. [Create voting](#32-create-voting-post-votings) `POST /votings`
  3. [Get voting](#33-get-voting-get-votingsid) `GET /votings/{id}`
  4. [Edit voting](#34-edit-voting-put-votingsid) `PUT /votings/{id}`
  5. [Delete voting](#35-delete-voting-delete-votingsid) `DELETE /votings/{id}`
4. [Votes](#4-votes)
  1. [Get user votes](#41-get-user-votes-get-votes) `GET /votes`
  2. [Get user votes count](#42-get-user-votes-count-get-votescount) `GET /votes/count`
  3. [Create user vote](#43-create-user-vote-post-votes) `POST /votes`
  4. [Get user vote](#44-get-user-vote-get-votesid) `GET /votes/{id}`
5. [Apps](#5-apps)
  1. [Get apps](#51-get-apps) `GET /apps`
  2. [Get apps count](#52-get-apps-count) `GET /apps/count`
  3. [Create app](#53-create-app-post-apps) `POST /apps`
6. [Profile](#6-profile)
  1. [Get profile](#61-get-profile-get-profile) `GET /profile`
  2. [Create profile](#62-create-profile-post-profile) `POST /profile`

## 1. Information

To use this API your app need **client access token** and for some resources **owner access token**. Authorize using [OAuth API](https://github.com/art-eltyshev/doc/blob/master/oauth-api.md) to get tokens.

App access levels:
* Common
* Extended

*work in progress...*

## 2. Content
Resources for retrieving edemos content

### 2.1. Get news `GET /news`

**Headers:**
* `Authorization: Client {client_token}`

**Parameters:**
* `limit` ( *optional*, *number*, *default=2* )
* `offset` ( *optional*, *number*, *default=0* )

**Request:**
```http
GET /news?limit=1 HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
```

**Response:**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"news": [
		{
			"date": 2013-01-02T8:00:00,
			"title": "Breaking news!",
			"text": "Something happends",
			"image": "1.jpeg"
		}
	],
	"count": 1
}
```

### 2.2. Get news count `GET /news/count`

**Headers:**
* `Authorization: Client {client_token}`

**Request:**
```http
GET /news/count HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"count": 1
}
```

### 2.3. Get banner `GET /banner`

**Headers:**
* `Authorization: Client {client_token}`

**Request:**
```http
GET /news/count HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"text": "Test banner",
	"image": "1.jpeg"
}
```

## 3. Votings

### 3.1. Get votings `GET /votings`

**Headers:**
* `Authorization: Client {client_token}`

**Parameters:**
* `limit` ( *optional*, *number*, *default=5* )
* `offset` ( *optional*, *number*, *default=0* )

**Request:**
```http
GET /votings HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"count": 2,
	"votings":[
		{
			"id": 12321,
			"title": "Voting for president"
		},
		{
			"id": 12322,
			"title": "Test voting"
		}
	]
}
```

### 3.2. Create voting `POST /votings`

**Headers:**
* `Authorization: Client {client_token}`
* `Content-Type: application/json`

**Parameters:**
* `title` ( *required*, *string* ) - Voting title.
* `url` ( *required*, *string* ) - Url of the voting page.
* `start_date`
* `end_date`
* `max_selection`
* `has_log`
* `anonymous`
* `refrain`
* `realtime_result`
* `custom_options`
* `options`
* `against_all_option`

**Request:**
```http
POST /votings HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
Content-Type: application/json

{
	"title": "New voting",
	"url": "http://democratia2.ru/votings/123",
	"start_date": "2013-01-01T0:00:00",
	"end_date": "2013-01-02T0:00:00",
	"max_selection": 1,
	"has_log": false,
	"anonymous": false,
	"refrain": false,
	"realtime_result": false,
	"custom_options": false,
	"options": ["Option #1", "Option #2"],
	"against_all_option": "Against all!"
}
```

**Response**
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
	"id": 123123
}
```

### 3.3. Get voting `GET /votings/{id}`

**Headers:**
* `Authorization: Client {client_token}`

**Parameters:**
* `id` ( *required*, *string* ) - Voting id

**Request:**
```http
GET /votings/123456 HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"title": "New voting",
	"url": "http://democratia2.ru/votings/123",
	"creation_date": "2012-12-31T8:00:00",
	"start_date": "2013-01-01T0:00:00",
	"end_date": "2013-01-02T0:00:00",
	"state": "finished",
	"max_selection": 1,
	"has_log": false,
	"anonymous": false,
	"refrain": false,
	"realtime_result": false,
	"custom_options": false,
	"options": [
		{
			"id": 1,
			"title": "Option #1"
		},
		{
			"id": 2,
			"title": "Option #2"
		},
		{
			"id": 3,
			"title": "Against all!"
		}
	],
	"against_all_option_id": 3
}
```

### 3.4. Edit voting `PUT /votings/{id}`

**Headers:**
* `Authorization: Client {client_token}`
* `Content-Type: application/json`

**Parameters:**
* `title` ( *required*, *string* ) - Voting title.
* `url` ( *required*, *string* ) - Link to the voting page.
* `start_date`
* `end_date`
* `max_selection`
* `has_log`
* `anonymous`
* `refrain`
* `realtime_result`
* `custom_options`
* `options`
* `against_all_option`

**Request:**
```http
PUT /votings/123456 HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
Content-Type: application/json

{
	"title": "New voting",
	"url": "http://democratia2.ru/votings/456",
	"start_date": 2013-01-01T0:00:00,
	"end_date": 2013-01-02T0:00:00,
	"max_selection": 1,
	"has_log": false,
	"anonymous": false,
	"refrain": false,
	"realtime_result": false,
	"custom_options": false,
	"options": ["Option #1", "Option #2"],
	"against_all_option": "Against all!"
}
```

**Response**
```http
HTTP/1.1 200 OK
```

### 3.5. Delete voting `DELETE /votings/{id}`

**Headers:**
* `Authorization: Client {client_token}`

**Parameters:**
* `id` ( *required*, *string* ) - Voting id

**Request:**
```http
DELETE /votings/123456 HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
```

**Response**
```http
HTTP/1.1 200 OK
```

## 4. Votes

### 4.1. Get user votes `GET /votes`
### 4.2. Get user votes count `GET /votes/count`
### 4.3. Create user vote `POST /votes`

**Headers:**
* `Authorization: Owner {owner_token}`
* `Content-Type: application/json`

**Parameters:**
* `voting_id` ( *required*, *string* ) - Voting id
* `options` ( *required*, *array* of *string* ) - Array of voted options ids
* `custom_option` ( *not used* )

**Request:**
```http
POST /votes HTTP/1.1
Authorization: Owner 1q2w3e4r5t6y7u8i9o0p
Content-Type: application/json

{
	"voting_id": "123456",
	"options": ["123", "321"]
}
```

**Response**
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
	"id": 123123
}
```

### 4.4. Get user vote `GET /votes/{id}`

## 5. Apps

### 5.1. Get apps `GET /apps`
### 5.2. Get apps count `GET /apps/count`
### 5.3. Create app `POST /apps`

**Headers:**
* `Authorization: Client {client_token}`
* `Content-Type: application/json`

**Parameters:**
* `title` ( *required*, *string* )
* `url` ( *required*, *string* )
* `redirect_uri` ( *required*, *string* ) - Redirect uri for OAuth access grant

**Request:**
```http
POST /apps HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
Content-Type: application/json

{
	"title": "Democratia 2",
	"url": "http://democratia2.ru",
	"redirect_uri": "http://democratia2.ru/auth"
}
```

**Response**
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
	"client_id": "123123",
	"client_secret": "1q2w3e4r"
}
```

## 6. Profile

### 6.1. Get profile `GET /profile`
### 6.2. Create profile `POST /profile`