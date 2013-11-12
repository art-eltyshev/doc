# public API
1. [Information](#1-information)
2. [Votings](#2-votings)
  * [Get votings](#get-votings-get-votings) `GET /votings`
  * [Get votings count](#get-votings-get-votingscount) `GET /votings/count`
  * [Create voting](#create-voting-post-votings) `POST /votings`
  * [Get voting](#get-voting-get-votingsid) `GET /votings/{id}`
  * [Edit voting](#edit-voting-put-votingsid) `PUT /votings/{id}`
  * [Delete voting](#delete-voting-delete-votingsid) `DELETE /votings/{id}`
  * [Get voting options](#get-voting-options-get-votingsidoptions) `GET /votings/{id}/options`
  * [Add voting option](#add-voting-option-post-votingsidoptions) `POST /votings/{id}/options`
  * [Edit voting option](#edit-voting-option-put-votingsidoptionsid) `PUT /votings/{id}/options/{id}`
  * [Delete voting option](#delete-voting-option-delete-votingsidoptionsid) `DELETE /votings/{id}/options/{id}`
  * [Get user's vote in voting](#get-users-vote-in-voting-get-votingsidvote) `GET /votings/{id}/vote`
  * [Add user's vote to voting](#add-users-vote-to-voting-post-votingsidvote) `POST /votings/{id}/vote`
  * [Get voting result](#get-voting-result-get-votingsidresult) `GET /votings/{id}/result`
3. [Apps](#3-apps)
  * [Get current app info](#get-current-app-info-get-appsself) `GET /apps/self`
  * [Edit current app info](#edit-current-app-info-put-appsself) `PUT /apps/self`
  * [Get apps](#get-apps-get-apps) `GET /apps`
  * [Get apps count](#get-apps-count-get-appscount) `GET /apps/count`
  * [Create app](#create-app-post-apps) `POST /apps`
  * [Get app](#get-app-get-appsid) `GET /apps/{id}`
  * [Edit app] (#edit-app-put-appsid) `PUT /apps/{id}`
4. [Users](#4-users)
  * [Get user's info](#get-users-info-get-user) `GET /user`
  * [Edit user's info](#edit-users-info-put-user) `PUT /user`
  * [Get user's votes](#get-users-votes-get-uservotes) `GET /user/votes`

## 1. Information

To use this API your app need **client access token** and for some resources **owner access token**. Authorize using [OAuth API](https://github.com/art-eltyshev/doc/blob/master/oauth-api.md) to get tokens.

App access levels:
* Common
* Extended

*work in progress...*

## 2. Votings

### Get votings `GET /votings`

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

### Get votings count `GET /votings/count`

**Headers:**
* `Authorization: Client {client_token}`

**Request:**
```http
GET /votings/count HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"count": 2
}
```

### Create voting `POST /votings`

**Headers:**
* `Authorization: Client {client_token}`
* `Content-Type: application/json`

**Parameters:**
* `title` ( *required*, *string* ) - Voting title.
* `url` ( *required*, *string* ) - Url of the voting page.
* `start_date` ( *required*, *string* )
* `end_date` ( *required*, *string* in format %Y-%m-%dT%H:%M:%S )
* `max_selection` ( *required*, *int* )
* `refrain` ( *required*, *bool* )
* `realtime_result` ( *required*, *bool* )

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
	"refrain": false,
	"realtime_result": false
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

### Get voting `GET /votings/{id}`

**Headers:**
* `Authorization: Client {client_token}`

**Parameters:**
* `id` ( *required* ) - Voting id

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
	"max_selection": 1,
	"refrain": false,
	"realtime_result": false
}
```

### Edit voting `PUT /votings/{id}`

**Headers:**
* `Authorization: Client {client_token}`
* `Content-Type: application/json`

**Parameters:**
* `title` ( *required*, *string* ) - Voting title.
* `url` ( *required*, *string* ) - Url of the voting page.
* `start_date` ( *required*, *string* )
* `end_date` ( *required*, *string* in format %Y-%m-%dT%H:%M:%S )
* `max_selection` ( *required*, *int* )
* `refrain` ( *required*, *bool* )
* `realtime_result` ( *required*, *bool* )

**Request:**
```http
PUT /votings/123456 HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
Content-Type: application/json

{
	"title": "New voting",
	"url": "http://democratia2.ru/votings/123",
	"start_date": "2013-01-01T0:00:00",
	"end_date": "2013-01-02T0:00:00",
	"max_selection": 1,
	"refrain": false,
	"realtime_result": false
}
```

**Response**
```http
HTTP/1.1 200 OK
```

### Delete voting `DELETE /votings/{id}`

**Headers:**
* `Authorization: Client {client_token}`

**Parameters:**
* `id` ( *required* ) - Voting id

**Request:**
```http
DELETE /votings/123456 HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
```

**Response**
```http
HTTP/1.1 200 OK
```

### Get voting options `GET /votings/{id}/options`

**Headers:**
* `Authorization: Client {client_token}`

**Parameters:**
* `id` ( *required* ) - Voting id

**Request:**
```http
GET /votings/123456/options HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"options": [
		{
			"id": 123,
			"data": {
				"title": "Option #1"
			}
		},
		{
			"id": 456,
			"data": {
				"title": "Option #2"
			}
		},
		{
			"id": 789,
			"data": {
				"title": "Against all!"
			},
			"against_all": true
		},
	],
	"count": 3
}
```

### Add voting option `POST /votings/{id}/options`

**Headers:**
* `Authorization: Client {client_token}`
* `Content-Type: application/json`

**Parameters:**
* `data` ( *required*, *JSON object* )
* `against_all` ( *optional*, *boolean* )

**Request:**
```http
POST /votings/123456/options HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
Content-Type: application/json

{
	"data": {
		"title": "Against all!"
	},
	"against_all": true
}
```

**Response**
```http
HTTP/1.1 201 OK
Content-Type: application/json

{
	"id": 789
}
```

### Edit voting option `PUT /votings/{voting_id}/options/{option_id}`

**Headers:**
* `Authorization: Client {client_token}`
* `Content-Type: application/json`

**Parameters:**
* `voting_id` ( *required* )
* `option_id` ( *required* )
* `data` ( *required*, *JSON object* )
* `against_all` ( *optional*, *boolean* )

**Request:**
```http
PUT /votings/123456/options/789 HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
Content-Type: application/json

{
	"data": {
		"title": "Option #3"
	},
	"against_all": false
}
```

**Response**
```http
HTTP/1.1 200 OK
```

### Delete voting option `DELETE /votings/{id}/options/{id}`

**Headers:**
* `Authorization: Client {client_token}`

**Parameters:**
* `voting_id` ( *required* )
* `option_id` ( *required* )
* `data` ( *required*, *JSON object* )
* `against_all` ( *optional*, *boolean* )

**Request:**
```http
DELETE /votings/123456/options/789 HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
```

**Response**
```http
HTTP/1.1 200 OK
```

### Get user's vote in voting `GET /votings/{id}/vote`

**Headers:**
* `Authorization: Owner {owner_token}`

**Parameters:**
* `id` ( *required* )

**Request:**
```http
GET /votings/123456/vote HTTP/1.1
Authorization: Owner 1q2w3e4r5t6y7u8i9o0p
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
}
```

### Add user's vote in voting `POST /votings/{id}/vote`

**Headers:**
* `Authorization: Owner {owner_token}`
* `Content-Type: application/json`

**Parameters:**
* `id` ( *required* )
* `options_ids` ( *required* )

**Request:**
```http
POST /votings/123456/vote HTTP/1.1
Authorization: Owner 1q2w3e4r5t6y7u8i9o0p
Content-Type: application/json

[
	123, 456
]
```

**Response**
```http
HTTP/1.1 201 OK
```

### Get voting result `GET /votings/{id}/result`

**Headers:**
* `Authorization: Client {client_token}`

**Parameters:**
* `id` ( *required* )

**Request:**
```http
GET /votings/123456/result HTTP/1.1
Authorization: Owner 1q2w3e4r5t6y7u8i9o0p
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
}
```

## 3. Apps

### Get current app info `GET /apps/self`

**Headers:**
* `Authorization: Client {client_token}`

**Request:**
```http
GET /apps/self HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"title": "Democratia 2",
	"url": "http://democratia2.ru",
	"redirect_uri": "http://democratia2.ru/auth"
}
```

### Edit current app info `PUT /apps/self`

**Headers:**
* `Authorization: Client {client_token}`
* `Content-Type: application/json`

**Parameters:**
* `title` ( *required*, *string* )
* `url` ( *required*, *string* )
* `redirect_uri` ( *required*, *string* ) - Redirect uri for OAuth access grant

**Request:**
```http
PUT /apps/self HTTP/1.1
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
HTTP/1.1 200 OK
```

### Get apps `GET /apps`

### Get apps count `GET /apps/count`

### Create app `POST /apps`

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

### Get app `GET /apps/{id}`

### Edit app `PUT /apps/{id}`

## 4. Users

### Get user's info `GET /user`
### Edit user's info `PUT /user`
### Get user's votes `GET /user/votes`