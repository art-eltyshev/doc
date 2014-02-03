# public API
1. [Information](#1-information)
2. [User authorization](#2-user-authorization)
  * [Check phone](#check-phone-post-check-phone) `POST /check-phone`
  * [Confirm](#confirm-post-confirm) `POST /confirm`
3. [Votings](#3-votings)
  * [Get votings](#get-votings-get-votings) `GET /votings`
  * [Get votings count](#get-votings-count-get-votingscount) `GET /votings/count`
  * [Create voting](#create-voting-post-votings) `POST /votings`
  * [Get voting](#get-voting-get-votingsid) `GET /votings/{id}`
  * [Edit voting](#edit-voting-put-votingsid) `PUT /votings/{id}`
  * [Delete voting](#delete-voting-delete-votingsid) `DELETE /votings/{id}`
  * [Get voting options](#get-voting-options-get-votingsidoptions) `GET /votings/{id}/options`
  * [Get voting options](#get-voting-option-get-votingsvoting_idoptionsoption_id) `GET /votings/{voting_id}/options/{option_id}`
  * [Add voting option](#add-voting-option-post-votingsidoptions) `POST /votings/{id}/options`
  * [Edit voting option](#edit-voting-option-put-votingsvoting_idoptionsoptionsoption_id) `PUT /votings/{voting_id}/options/{option_id}`
  * [Delete voting option](#delete-voting-option-delete-votingsvoting_idoptionsoption_id) `DELETE /votings/{voting_id}/options/{option_id}`
  * [Get user's vote in voting](#get-users-vote-in-voting-get-votingsidvote) `GET /votings/{id}/vote`
  * [Add user's vote to voting](#add-users-vote-to-voting-post-votingsidvote) `POST /votings/{id}/vote`
  * [Get voting result](#get-voting-result-get-votingsidresult) `GET /votings/{id}/result`
4. [Apps](#4-apps)
  * [Get current app info](#get-current-app-info-get-appsself) `GET /apps/self`
  * [Edit current app info](#edit-current-app-info-put-appsself) `PUT /apps/self`
  * [Get apps](#get-apps-get-apps) `GET /apps`
  * [Get apps count](#get-apps-count-get-appscount) `GET /apps/count`
  * [Create app](#create-app-post-apps) `POST /apps`
  * [Get app](#get-app-get-appsid) `GET /apps/{id}`
  * [Edit app] (#edit-app-put-appsid) `PUT /apps/{id}`
  * [Delete app] (#delete-app-delete-appsid) `DELETE /apps/{id}`
5. [Users](#5-users)
  * [Get user's info](#get-users-info-get-user) `GET /user`
  * [Edit user's info](#edit-users-info-put-user) `PUT /user`
  * [Get user's votes](#get-users-votes-get-uservotes) `GET /user/votes`

## 1. Information

*work in progress...*

## 2. User authorization

### Check phone `POST /check-phone`

**Headers:**
* `Api-Key: {api_key}`

**Parameters:**
* `phone` ( *required*, *string* )

**Request:**
```http
POST /check-phone HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
Content-Type: application/json

{
	"phone": "79999999999"
}
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"requests_left": 19,
	"attempts_left": 5,
	"password_lifetime": 900
}
```
### Confirm `POST /confirm`

**Headers:**
* `Api-Key: {api_key}`

**Parameters:**
* `phone` ( *required*, *string* )
* `password` ( *required*, *string* )

**Request:**
```http
POST /confirm HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
Content-Type: application/json

{
	"phone": "79999999999",
	"password": "12345"
}
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"requests_left": 19,
	"attempts_left": 5,
	"password_lifetime": 900
}
```

## 3. Votings

### Get votings `GET /votings`

**Headers:**
* `Api-Key: {api_key}`

**Parameters:**
* `limit` ( *optional*, *number*, *default=5* )
* `offset` ( *optional*, *number*, *default=0* )

**Request:**
```http
GET /votings HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"count": 2,
	"votings":[
		{
			"id": "1aa9f854-d69a-42a3-bcbe-4be0dbacde72",
			"title": "Voting for president",
			"start_date": "2013-01-01T0:00:00",
            		"end_date": "2014-01-01T0:00:00"
		},
		{
			"id": "25b217f5-1c03-49c7-9901-f89c04fc7e8b",
			"title": "Test voting",
			"start_date": "2013-01-01T0:00:00",
            		"end_date": "2014-01-01T0:00:00"
		}
	]
}
```

### Get votings count `GET /votings/count`

**Headers:**
* `Api-Key: {api_key}`

**Request:**
```http
GET /votings/count HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
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
* `Api-Key: {api_key}`
* `Content-Type: application/json`

**Parameters:**
* `title` ( *required*, *string* ) - Voting title.
* `url` ( *required*, *string* ) - Url of the voting page.
* `start_date` ( *required*, *string* )
* `end_date` ( *required*, *string* ) - in format %Y-%m-%dT%H:%M:%S
* `max_selection` ( *required*, *int* )
* `refrain` ( *required*, *bool* )
* `realtime_result` ( *required*, *bool* )

**Request:**
```http
POST /votings HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
Content-Type: application/json

{
	"title": "New voting",
	"url": "http://democratia2.ru/votings/848eb030-8a74-11e3-baa8-0800200c9a66",
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
	"id": "848eb030-8a74-11e3-baa8-0800200c9a66"
}
```

### Get voting `GET /votings/{id}`

**Headers:**
* `Api-Key: {api_key}`

**Parameters:**
* `id` ( *required* ) - Voting id

**Request:**
```http
GET /votings/848eb030-8a74-11e3-baa8-0800200c9a66 HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"title": "New voting",
	"url": "http://democratia2.ru/votings/848eb030-8a74-11e3-baa8-0800200c9a66",
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
* `Api-Key: {api-key}`
* `Content-Type: application/json`

**Parameters:**
* `title` ( *required*, *string* ) - Voting title.
* `url` ( *required*, *string* ) - Url of the voting page.
* `start_date` ( *required*, *string* )
* `end_date` ( *required*, *string* ) - in format %Y-%m-%dT%H:%M:%S
* `max_selection` ( *required*, *int* )
* `refrain` ( *required*, *bool* )
* `realtime_result` ( *required*, *bool* )

**Request:**
```http
PUT /votings/848eb030-8a74-11e3-baa8-0800200c9a66 HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
Content-Type: application/json

{
	"title": "New voting",
	"url": "http://democratia2.ru/votings/848eb030-8a74-11e3-baa8-0800200c9a66",
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
DELETE /votings/848eb030-8a74-11e3-baa8-0800200c9a66 HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
```

**Response**
```http
HTTP/1.1 200 OK
```

### Get voting options `GET /votings/{id}/options`

**Headers:**
* `Api-Key: {api_key}`

**Parameters:**
* `id` ( *required* ) - Voting id

**Request:**
```http
GET /votings/848eb030-8a74-11e3-baa8-0800200c9a66/options HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"options": [
		{
			"id": "1aa9f854-d69a-42a3-bcbe-4be0dbacde72",
			"data": {
				"title": "Option #1",
				"description": "First option in voting",
				"photo": "1.jpg"
			}
		},
		{
			"id": "25b217f5-1c03-49c7-9901-f89c04fc7e8b",
			"data": {
				"title": "Option #2",
				"description": "Second option in voting",
				"photo": "2.jpg"
			}
		},
		{
			"id": "a0f8c836-f543-433d-93fa-97331944a761",
			"data": {
				"title": "Against all!"
				"description": "Against all option",
				"photo": "against.jpg"
			},
			"against_all": true
		},
	],
	"count": 3
}
```


### Get voting option `GET /votings/{voting_id}/options/{option_id}`

**Headers:**
* `Api-Key: {api_key}`

**Parameters:**
* `voting_id` ( *required* ) - Voting id
* `option_id` ( *required* ) - Option id

**Request:**
```http
GET /votings/848eb030-8a74-11e3-baa8-0800200c9a66/options/1aa9f854-d69a-42a3-bcbe-4be0dbacde72 HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"id": "a0f8c836-f543-433d-93fa-97331944a761",
	"data": {
		"title": "Against all!"
		"description": "Against all option",
		"photo": "against.jpg"
	},
	"against_all": true
}
```

### Add voting option `POST /votings/{id}/options`

**Headers:**
* `Api-Key: {api_key}`
* `Content-Type: application/json`

**Parameters:**
* `data` ( *required*, *JSON object* )
* `against_all` ( *optional*, *boolean* )

**Request:**
```http
POST /votings/848eb030-8a74-11e3-baa8-0800200c9a66/options HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
Content-Type: application/json

{
	"data": {
		"title": "Against all!"
		"description": "Against all option",
		"photo": "against.jpg"
	},
	"against_all": true
}
```

**Response**
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
	"id": "a0f8c836-f543-433d-93fa-97331944a761"
}
```

### Edit voting option `PUT /votings/{voting_id}/options/{option_id}`

**Headers:**
* `Api-Key: {api_key}`
* `Content-Type: application/json`

**Parameters:**
* `voting_id` ( *required* )
* `option_id` ( *required* )
* `data` ( *required*, *JSON object* )
* `against_all` ( *optional*, *boolean* )

**Request:**
```http
PUT /votings/848eb030-8a74-11e3-baa8-0800200c9a66/options/1aa9f854-d69a-42a3-bcbe-4be0dbacde72 HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
Content-Type: application/json

{
	"data": {
		"title": "Option #3"
		"description": "Third option in voing",
		"photo": "3.jpg"
	},
	"against_all": false
}
```

**Response**
```http
HTTP/1.1 200 OK
```

### Delete voting option `DELETE /votings/{voting_id}/options/{option_id}`

**Headers:**
* `Api-Key: {api-key}`

**Parameters:**
* `voting_id` ( *required* )
* `option_id` ( *required* )

**Request:**
```http
DELETE /votings/848eb030-8a74-11e3-baa8-0800200c9a66/options/1aa9f854-d69a-42a3-bcbe-4be0dbacde72 HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
```

**Response**
```http
HTTP/1.1 200 OK
```

### Get voting result `GET /votings/{id}/result`

**Headers:**
* `Api-Key: {api_key}`

**Parameters:**
* `id` ( *required* )

**Request:**
```http
GET /votings/848eb030-8a74-11e3-baa8-0800200c9a66/result HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"total_voters": 10000,
	"verified_voters": 6700,
	"options": [
		{
			"id": "1aa9f854-d69a-42a3-bcbe-4be0dbacde72",
			"total_voters": 5000,
			"verified_voters": 3000
		},
		{
			"id": "25b217f5-1c03-49c7-9901-f89c04fc7e8b",
			"total_voters": 5000,
			"verified_voters": 3700
		}
	]
}
```

### Get user's vote in voting `GET /votings/{id}/vote`

**Headers:**
* `Api-Key: {api_key}`
* `User-Token: {user_token}`

**Parameters:**
* `id` ( *required* )

**Request:**
```http
GET /votings/848eb030-8a74-11e3-baa8-0800200c9a66/vote HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
User-Token: bf3ffc46b57d4d08bfe2d0be307b21ae
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"date": "2013-01-01T0:00:00",
	"options": [
		{
			"id": "1aa9f854-d69a-42a3-bcbe-4be0dbacde72"
		}
	]
}
```

### Add user's vote to voting `POST /votings/{id}/vote`

**Headers:**
* `Api-Key: {api_key}`
* `User-Token: {user_token}`
* `Content-Type: application/json`

**Parameters:**
* `id` ( *required* )
* `options_ids` ( *required* )

**Request:**
```http
POST /votings/848eb030-8a74-11e3-baa8-0800200c9a66/vote HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
User-Token: bf3ffc46b57d4d08bfe2d0be307b21ae
Content-Type: application/json

[
	{
		"id": "1aa9f854-d69a-42a3-bcbe-4be0dbacde72"
	},
	{
		"id": "25b217f5-1c03-49c7-9901-f89c04fc7e8b"
	}
]
```

**Response**
```http
HTTP/1.1 201 Created
```


## 4. Apps

### Get current app info `GET /apps/self`

**Headers:**
* `Api-Key: {api_key}`

**Request:**
```http
GET /apps/self HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"title": "Democratia 2",
	"url": "http://democratia2.ru"
}
```

### Edit current app info `PUT /apps/self`

**Headers:**
* `Api-Key: {api_key}`
* `Content-Type: application/json`

**Parameters:**
* `title` ( *required*, *string* )
* `url` ( *required*, *string* )

**Request:**
```http
PUT /apps/self HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
Content-Type: application/json

{
	"title": "Democratia 2",
	"url": "http://democratia2.ru",
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
* `Api-Key: {api_key}`
* `Content-Type: application/json`

**Parameters:**
* `title` ( *required*, *string* )
* `url` ( *required*, *string* )

**Request:**
```http
POST /apps HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
Content-Type: application/json

{
	"title": "Democratia 2",
	"url": "http://democratia2.ru",
}
```

**Response**
```http
HTTP/1.1 201 Created
Content-Type: application/json

{
	"id": "2",
	"api_key": "d4fa4d4f3c2c42878114bb9112352e59"
}
```

### Get app `GET /apps/{id}`

### Edit app `PUT /apps/{id}`

### Delete app `DELETE /apps/{id}`

**Headers:**
* `Api-Key: {api_key}`

**Parameters:**
* `id` ( *required*, *string* )

**Request:**
```http
DELETE /apps/2 HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
```

**Response**
```http
HTTP/1.1 200 OK
```

## 5. Users

### Get user's info `GET /user`

**Headers:**
* `Api-Key: {api_key}`
* `User-Token: {user_token}`

**Request:**
```http
GET /user HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
User-Token: bf3ffc46b57d4d08bfe2d0be307b21ae
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"firstname": "Firstname",
        "middlename": "Middlename",
        "lastname": "Lastname",
        "birth_date": "1991-01-01T0:00:00",
        "email": "admin@edemos.org",
        "email_subscribed": true,
        "phone": "79999999999",
        "phone_subscribed": false,
        "register_date": "2013-01-01T0:00:00"
}
```

### Edit user's info `PUT /user`

**Headers:**
* `Api-Key: {api_key}`
* `User-Token: {user_token}`
* `Content-Type: application/json`

**Parameters:**
* `firstname` ( *required*, *string* )
* `middlename` ( *required*, *string* )
* `lastname` ( *required*, *string* )
* `birth_date` ( *required*, *datetime* )
* `email` ( *required*, *string* )
* `email_subscribed` ( *required*, *bool* )
* `phone_subscribed` ( *required*, *bool* )

**Request:**
```http
PUT /user HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
User-Token: bf3ffc46b57d4d08bfe2d0be307b21ae
Content-Type: application/json

{
	"firstname": "Firstname",
        "middlename": "Middlename",
        "lastname": "Lastname",
        "birth_date": "1991-01-01T0:00:00",
        "email": "admin@edemos.org",
        "email_subscribed": true,
        "phone_subscribed": false,
}
```

**Response**
```http
HTTP/1.1 200 OK
```

### Get user's votes `GET /user/votes`

**Headers:**
* `Api-Key: {api_key}`
* `User-Token: {user_token}`

**Parameters:**
* `limit` ( *optional*, *number*, *default=5* )
* `offset` ( *optional*, *number*, *default=0* )

**Request:**
```http
GET /user/votes HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
User-Token: bf3ffc46b57d4d08bfe2d0be307b21ae
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

[
	{
		"date": "2013-01-01T0:00:00",
		"voting":
		{
			"title": "New voting",
			"start_date": "2013-01-01T0:00:00",
			"end_date": "2013-01-02T0:00:00",
			"total_voters": 10000,
			"realtime_result": true
		},
		"options":
		[
			{
				"id": "1aa9f854-d69a-42a3-bcbe-4be0dbacde72",
				"data": {
					"title": "Option #1",
					"description": "First option in voting",
					"photo": "1.jpg"
				}
			},
			{
				"id": "25b217f5-1c03-49c7-9901-f89c04fc7e8b",
				"data": {
					"title": "Option #2",
					"description": "Second option in voting",
					"photo": "2.jpg"
				}
			}
		]
	}
]
```


### Get user's votes count `GET /user/votes/count`

**Headers:**
* `Api-Key: {api_key}`
* `User-Token: {user_token}`

**Request:**
```http
GET /user/votes/count HTTP/1.1
Api-Key: 550e8400e29b41d4a716446655440000
User-Token: bf3ffc46b57d4d08bfe2d0be307b21ae
```

**Response**
```http
HTTP/1.1 200 OK
Content-Type: application/json

{
	"count": 1
}
```
