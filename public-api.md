HOST: https://api.edemos.org

# edemos public API
Public API

## Contents
1. [Content](#1-content)
	1. [Retrieve news](#Content-GetNews)
	2. [Retrieve news count](#Content-GetNewsCount)
1. [Votings](#2-votings)
2. [Votes](#3-votes)
3. [Apps](#4-apps)

# 1. Content
Resources for retrieving edemos content

### 1.1. GET /news
Returns project news

**Headers:**
* ```Authorization: Client {client_token}```

**Parameters:**
* ```limit``` = 2
* ```offset``` = 0

**Request:**
```http
GET /news HTTP/1.1
Authorization: Client 1q2w3e4r5t6y7u8i9o0p
```


**Response**
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

### 1.2. GET /news/count
Retrieve news count

**Request**

* Headers

		Authorization: Client 1q2w3e4r5t6y7u8i9o0p

**Response** 200 (application/json)
```javascript
{
	"count": 12
}
```

### 1.3 GET /banner
Returns current banner

**Request**

* Headers

		Authorization: Client 1q2w3e4r5t6y7u8i9o0p

**Response** 200 (application/json)
```javascript
{
	"text": "Test banner",
	"image": "1.jpeg"
}
```

<a name="Votings"></a>
# 2. Votings

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
	+ options
	+ against_all_option

+ Request (application/json)
	
	+ Headers

			Authorization: Client 1q2w3e4r5t6y7u8i9o0p
	
	+ Body

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

### Edit voting [POST]

+ Parameters

	+ title (required, string) ... Voting title.
	+ link (required, string) ... Link to voting page.
	+ start_date (required, datetime)
	+ end_date (required, datetime)
	+ max_selection (required, bool)
	+ has_log (required, bool)
	+ anonymous (required, bool)
	+ refrain (required, bool)
	+ realtime_result (required, bool)
	+ custom_options (required, array)
	+ against_all_option (required, string)

+ Request (application/json)
	
	+ Headers

			Authorization: Client 1q2w3e4r5t6y7u8i9o0p
	
	+ Body
	
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

+ Response 200

<a name="Votes"></a>
# 3. Votes

## /votes

+ Headers

			Authorization: Owner {owner_token}

### Add vote [POST]

+ Parameters

	+ voting_id
	+ option_id