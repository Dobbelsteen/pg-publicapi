# Place.Guru public API documentation

**ALL public api calls require the affix** `?key=YOUR_API_KEY`

**POST** and **PUT** requests can either be made with **form data** or **JSON-objects**

# Places

## Get All Places

```
GET /publicapi/places
```

No other parameters


## Get Place

```
GET /publicapi/places/{url}
```

#### URL parameters
- `url` The identifying url of a place

Example request
```
https://place.guru/publicapi/places/azerty4-ab713bc-qwerty2?key=YOUR_API_KEY
```

## Create place

```
POST /publicapi/places
```

#### Arguments

- `name` (required)
  - **Valid values:** Text string of maximum 45 characters
- `geolat` (required)
  - **Valid values:** Latitude between -90 and 90
- `geolng` (required)
  - **Valid values:** Longitude between -180 and 180
- `description` (optional)
  - **Valid values:** Text string of maximum 65554 characters, supports **markdown** format
- `published` (optional)
  - **Valid values:** `true` or `false`
  - **Default:** `false`
  - **Description:** Whether the place shows up in explore or not
- `comments_enabled` (optional)
  - **Valid values:** `true` or `false`
  - **Default:** `true`
  - **Description:** Enable comments or not
- `mails_enabled` (optional)
  - **Valid values:** `true` or `false`
  - **Default:** `true`
  - **Description:** Enable e-mail updates when there is activity in the place (new comments)
- `address` (optional)
  - **Valid values:** Text string of maximum 255 characters
- `phone_number` (optional)
  - ** values:** Text string of maximum 255 characters
- `email` (optional)
  - **Valid values:** E-mail address of maximum 255 characters
- `videos` (optional)
  - **Valid values:** Array of urls for embedded videos
    - **Example:** `[ "link_1" , "link_2" ]`
    **TODO:** What kind of URLs will we allow, parse them in backend or not, ..., exampple links?
- `links` (optional)
  - **Valid values:** Array of link objects
    - **Example:**
    ```
    [
      {
        "type" : "website",
        "url" : "http://my.site.com"
      },
      {
        "type" : "twitter",
        "url" : "https://twitter.com/myCompany"
      }
    ]
    ```
    - `url` (required)
      - **Valid values:** Valid url
    - `type` (optional)
      - **Valid values:** `website`, `twitter`, `facebook`, `linkedin` (types will be expanded upon)
- `personas` (optional)
  - **Valid values:** Array of persona objects
    - **Example:**
    ```
    [
      {
        "name": "Your name",
        "title": "Your company title",
        "url": "azerty12"
      },
      {
        "name": "Your CTO's name",
        "title": "Company CTO"
      }
    ]
    ```
    - `name` (required)
      - **Valid values:** Text string of maximum 120 characters  
    - `title` (optional)
      - **Valid values:** Text string of maximum 255 characters
    - `url` (optional)
      - **Valid values:** THINK ABOUT WORKING HERE, maybe rename field
- `availability` (optional)
  - **Valid values:** Array of availiability objects
    - **Example:**
    ```
    [
      {
        "start" : "1-1-2017",
        "end": "25-02-2017",
        "note" : "Only available via phone"
      },
      {
        "start" : "28-02-2017",
        "end": "14-03-2017",
        "note" : "We're on skibreak"
      }
    ]
    ```
    - `start` (required)
      - **Valid values:** Date with format d-m-Y
    - `end` (optional)
      - **Valid values:** Date with format d-m-Y
    - `note` (optional)
      - *Valid values:** Text string of maximum 1023 characters
- `opening_hours` (optional)
  - **Valid values:** Array of opening_hour objects  
    - **Example:**
    ```
    [
      {
        "note": "Business opening hours"
        "hours": [
          {
            "day":"1",
        	  "open":"08:30",
        	  "close":"17:00"
        	},
          {
            "day":"2",
            "open":"08:30",
            "close":"12:00"
          },
          {
            "day":"2",
            "open":"13:30",
            "close":"17:00"
          },
          {
            "day":"5",
            "open":"08:30",
            "close":"17:00"
          }
        ]
      },
      {
        "note": "Callcenter opening hours"
        "hours": [
          {
            "day":"1",
            "open":"08:30",
            "close":"23:00"
          },
          {
            "day":"2",
            "open":"08:30",
            "close":"23:00"
          },
          {
            "day":"5",
            "open":"08:30",
            "close":"23:00"
          }
        ]
      }
    ]
    ```
    - `note` (optional)
      - **Valid values:** Text string of maximum 1023 characters
    - `hours` (required)
      - **Valid values:** Hours object, you can have multiple Hours objects for the same day
        - `day` (required)
        - **Valid values:** 1-7, 1 being Monday, 7 being Sunday
        - `open` (required)
        - **Valid values:** Hour with format H:i
        - `close` (required)
        - **Valid values:** Hour with format H:i, after `open`
- `tags` (optional)
  - **Valid values:** Array of maximum 5 tags, each being maximum 25 characters long
    - **Example:** `[ "tag" , "your" , "place" ]`
- `custom_url` (optional)
  - **Valid values:** String of 2-45 characters long, no spaces, only letters, numbers, _ and -
- `custom_marker` (optional)
  - **Valid values:** Id of the custom marker you want to add

#### Full Example
```
{
  "name": "My first API Place",
  "geolat": "60.543232",
  "geolng": "30.321432",
  "description": "My place description goes here.",
  "published": true,
  "comments_enabled": true,
  "mails_enabled": false,
  "address": "SomeRoad 13, SomeCity",
  "phone_number": "123-45678-90",
  "email": "you@company.come",
  "videos": [
    "link_1",
    "link_2"
  ],
  "links": [
    {
      "type" : "website",
      "url" : "http://my.site.com"
    },
    {
      "type" : "twitter",
      "url" : "https://twitter.com/myCompany"
    }
  ],
  "personas": [
    {
      "name": "Your name",
      "title": "Your company title",
      "url": "azerty12"
    },
    {
      "name": "Your CTO's name",
      "title": "Company CTO"
    }
  ],
  "availability": [
    {
      "start" : "1-1-2017",
      "end": "25-02-2017",
      "note" : "Only available via phone"
    },
    {
      "start" : "28-02-2017",
      "end": "14-03-2017",
      "note" : "We're on ski break"
    }
  ],
  "opening_hours": [
    {
      "note": "Business opening hours"
      "hours": [
        {
          "day":"1",
          "open":"08:30",
          "close":"17:00"
        },
        {
          "day":"2",
          "open":"08:30",
          "close":"12:00"
        },
        {
          "day":"2",
          "open":"13:30",
          "close":"17:00"
        },
        {
          "day":"5",
          "open":"08:30",
          "close":"17:00"
        }
      ]
    }
  ],
  "tags": [ "tag", "your", "place" ],
  "custom_url": "my_custom_url",
  "custom_marker": 32
}
```

## Update place

```
PUT /publicapi/places/{url}
```

Updating a place uses the same template as the one used for creating a place.  
If you want to empty a field, just add the key of the field, and an empty string/array after.

Regarding arrays, such as `personas`, `tags`, `videos`, `links`, `opening_hours` and `availability`:  
If you add them to your request, the whole previous array will be overwritten.  
So, if you already had 1 persona for example, if you want to add a 2nd, you have to send both personas in the request.

**TODO:** Example

#### URL parameters
- `url` The identifying url of a place

#### Arguments
```
...
```

## Delete Place

```
DELETE /publicapi/places/{url}
```

#### URL parameters
- `url` The identifying url of a place



# Lists

## Get All Lists

```
GET /publicapi/lists
```

No other parameters


## Get List

```
GET /publicapi/lists/{url}
```

#### URL parameters
- `url` The identifying url of a list

Example request
```
https://place.guru/publicapi/lists/azerty4-ab713bc-qwerty2?key=YOUR_API_KEY
```

## Create list

```
POST /publicapi/lists
```

#### Arguments

- `name` (required)
  - **Valid values:** Text string of maximum 45 characters
- `description` (optional)
  - **Valid values:** Text string of maximum 65554 characters, supports **markdown** format
- `published` (optional)
  - **Valid values:** `true` or `false`
  - **Default:** `false`
  - **Description:** Whether the list shows up in explore or not
- `comments_enabled` (optional)
  - **Valid values:** `true` or `false`
  - **Default:** `true`
  - **Description:** Enable comments or not
- `mails_enabled` (optional)
  - **Valid values:** `true` or `false`
  - **Default:** `true`
  - **Description:** Enable e-mail updates when there is activity in the list (new comments)
- `address` (optional)
  - **Valid values:** Text string of maximum 255 characters
- `phone_number` (optional)
  - ** values:** Text string of maximum 255 characters
- `email` (optional)
  - **Valid values:** E-mail address of maximum 255 characters
- `videos` (optional)
  - **Valid values:** Array of urls for embedded videos
    - **Example:** `[ "link_1" , "link_2" ]`
    **TODO:** What kind of URLs will we allow, parse them in backend or not, ..., exampple links?
- `links` (optional)
  - **Valid values:** Array of link objects
    - **Example:**
    ```
    [
      {
        "type" : "website",
        "url" : "http://my.site.com"
      },
      {
        "type" : "twitter",
        "url" : "https://twitter.com/myCompany"
      }
    ]
    ```
    - `url` (required)
      - **Valid values:** Valid url
    - `type` (optional)
      - **Valid values:** `website`, `twitter`, `facebook`, `linkedin` (types will be expanded upon)
- `personas` (optional)
  - **Valid values:** Array of persona objects
    - **Example:**
    ```
    [
      {
        "name": "Your name",
        "title": "Your company title",
        "url": "azerty12"
      },
      {
        "name": "Your CTO's name",
        "title": "Company CTO"
      }
    ]
    ```
    - `name` (required)
      - **Valid values:** Text string of maximum 120 characters  
    - `title` (optional)
      - **Valid values:** Text string of maximum 255 characters
    - `url` (optional)
      - **Valid values:** THINK ABOUT WORKING HERE, maybe rename field
- `availability` (optional)
  - **Valid values:** Array of availiability objects
    - **Example:**
    ```
    [
      {
        "start" : "1-1-2017",
        "end": "25-02-2017",
        "note" : "Only available via phone"
      },
      {
        "start" : "28-02-2017",
        "end": "14-03-2017",
        "note" : "We're on skibreak"
      }
    ]
    ```
    - `start` (required)
      - **Valid values:** Date with format d-m-Y
    - `end` (optional)
      - **Valid values:** Date with format d-m-Y
    - `note` (optional)
      - *Valid values:** Text string of maximum 1023 characters
- `opening_hours` (optional)
  - **Valid values:** Array of opening_hour objects  
    - **Example:**
    ```
    [
      {
        "note": "Business opening hours"
        "hours": [
          {
            "day":"1",
        	  "open":"08:30",
        	  "close":"17:00"
        	},
          {
            "day":"2",
            "open":"08:30",
            "close":"12:00"
          },
          {
            "day":"2",
            "open":"13:30",
            "close":"17:00"
          },
          {
            "day":"5",
            "open":"08:30",
            "close":"17:00"
          }
        ]
      },
      {
        "note": "Callcenter opening hours"
        "hours": [
          {
            "day":"1",
            "open":"08:30",
            "close":"23:00"
          },
          {
            "day":"2",
            "open":"08:30",
            "close":"23:00"
          },
          {
            "day":"5",
            "open":"08:30",
            "close":"23:00"
          }
        ]
      }
    ]
    ```
    - `note` (optional)
      - **Valid values:** Text string of maximum 1023 characters
    - `hours` (required)
      - **Valid values:** Hours object, you can have multiple Hours objects for the same day
        - `day` (required)
        - **Valid values:** 1-7, 1 being Monday, 7 being Sunday
        - `open` (required)
        - **Valid values:** Hour with format H:i
        - `close` (required)
        - **Valid values:** Hour with format H:i, after `open`
- `tags` (optional)
  - **Valid values:** Array of maximum 5 tags, each being maximum 25 characters long
    - **Example:** `[ "tag" , "your" , "list" ]`
- `custom_url` (optional)
  - **Valid values:** String of 2-45 characters long, no spaces, only letters, numbers, _ and -
- `custom_marker` (optional)
  - **Valid values:** Id of the custom marker you want to add

#### Full Example
```
{
  "name": "My first API List",
  "description": "My list description goes here.",
  "published": true,
  "comments_enabled": true,
  "mails_enabled": false,
  "address": "SomeRoad 13, SomeCity",
  "phone_number": "123-45678-90",
  "email": "you@company.come",
  "videos": [
    "link_1",
    "link_2"
  ],
  "links": [
    {
      "type" : "website",
      "url" : "http://my.site.com"
    },
    {
      "type" : "twitter",
      "url" : "https://twitter.com/myCompany"
    }
  ],
  "personas": [
    {
      "name": "Your name",
      "title": "Your company title",
      "url": "azerty12"
    },
    {
      "name": "Your CTO's name",
      "title": "Company CTO"
    }
  ],
  "availability": [
    {
      "start" : "1-1-2017",
      "end": "25-02-2017",
      "note" : "Only available via phone"
    },
    {
      "start" : "28-02-2017",
      "end": "14-03-2017",
      "note" : "We're on ski break"
    }
  ],
  "opening_hours": [
    {
      "note": "Business opening hours"
      "hours": [
        {
          "day":"1",
          "open":"08:30",
          "close":"17:00"
        },
        {
          "day":"2",
          "open":"08:30",
          "close":"12:00"
        },
        {
          "day":"2",
          "open":"13:30",
          "close":"17:00"
        },
        {
          "day":"5",
          "open":"08:30",
          "close":"17:00"
        }
      ]
    }
  ],
  "tags": [ "tag", "your", "list" ],
  "custom_url": "my_custom_url",
  "custom_marker": 32
}
```

## Update list

```
PUT /publicapi/lists/{url}
```

Updating a list uses the same template as the one used for creating a list.  
If you want to empty a field, just add the key of the field, and an empty string/array after.

Regarding arrays, such as `personas`, `tags`, `videos`, `links`, `opening_hours` and `availability`:  
If you add them to your request, the whole previous array will be overwritten.  
So, if you already had 1 persona for example, if you want to add a 2nd, you have to send both personas in the request.

**TODO:** Example

#### URL parameters
- `url` The identifying url of a list

#### Arguments
```
...
```

## Delete List

```
DELETE /publicapi/lists/{url}
```

#### URL parameters
- `url` The identifying url of a list
