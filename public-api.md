HOST: https://api.edemos.org

# edemos public API
1. [Information](#)
2. [Content](#)
	1. [Get news](#)
	2. [Get news count](#)
	3. [Get banner](#)
3. [Votings](#)
4. [Votes](#)
5. [Apps](#)
6. [Profile](#)

## 1. Information
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
* `link` ( *required*, *string* ) - Link to the voting page.
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
	"start_date": 2013-01-01T0:00:00,
	"end_date": 2013-01-02T0:00:00,
	"max_selection": 1,
	"has_log": false,
	"anonymous": false,
	"refrain": false,
	"realtime_result": false,
	"custom_options": false,
	"options": ["Option #1", "Option #2"],
	"against_all_option": "Against all!",
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
	"creation_date": 2012-12-31T8:00:00,
	"start_date": 2013-01-01T0:00:00,
	"end_date": 2013-01-02T0:00:00,
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
	"against_all_option_id": 3,
}
```

### 3.4. Edit voting `PUT /votings/{id}`

**Headers:**
* `Authorization: Client {client_token}`
* `Content-Type: application/json`

**Parameters:**
* `title` ( *optional*, *string* ) - Voting title.
* `link` ( *optional*, *string* ) - Link to the voting page.
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
	"start_date": 2013-01-01T0:00:00,
	"end_date": 2013-01-02T0:00:00,
	"max_selection": 1,
	"has_log": false,
	"anonymous": false,
	"refrain": false,
	"realtime_result": false,
	"custom_options": false,
	"options": ["Option #1", "Option #2"],
	"against_all_option": "Against all!",
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

### 4.1. Create user vote `POST /votes`

**Headers:**
* `Authorization: Client {owner_token}`
* `Content-Type: application/json`

**Parameters:**
* `voting_id` ( *required*, *string* ) - Voting id
* `options` ( *required*, *array* of *string* ) - Array of voted options ids
* `custom_option` ( *not used* )

**Request:**
```http
POST /votes HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
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

### 4.2. Get user votes `GET /votes`
### 4.3. Get user votes count `GET /votes/count`
### 4.4. Get user vote `GET /votes/{id}`

## 5. Apps

### 5.1. Create app `POST /apps`

## 6. Profile

### 6.1. Create profile `POST /profile`
### 6.2. Get profile `GET /profile`