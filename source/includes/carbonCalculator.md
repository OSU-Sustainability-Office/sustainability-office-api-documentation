# Carbon Calculator

The base URL for the Carbon Calculator's API is [https://api.sustainability.oregonstate.edu/v2/carbon](https://api.sustainability.oregonstate.edu/v2/carbon). The following routes can be accessed by appending the endpoint to the base URL (ie: [https://https://api.sustainability.oregonstate.edu/v2/carbon/category...](https://https://api.sustainability.oregonstate.edu/v2/carbon/category...)

## /category

This endpoint is used for performing CRUD operations on one or more categories.

### GET
> GET

```shell
# Request all categories
curl "https://api.sustainability.oregonstate.edu/v2/carbon/category"
```

```shell
# Request a specific category
curl "https://api.sustainability.oregonstate.edu/v2/carbon/category?ID=1"
```

```javascript
// Response
{
  "categories": [
    {
      "id": 0,
      "color": "ffffff",
      "title": "Introduction",
      "IgnoreResults": true
    }
  ]
}
```

This method is used to retrieve one or more categories.

URL Parameters | Description
---------- | -------
ID (Optional) | The ID of the requested category. When this is specified, only one category is returned.

### POST
> POST

```shell
# Create a new category
curl -X POST "https://api.sustainability.oregonstate.edu/v2/carbon/category" \
-H "Content-Type: application/json" \
-H "Cookie: token=(put authentication token here)" -d \
'{
  "color": "ffffff",
  "title": "New Category",
  "ignoreResults": false
}'
```

```javascript
// Response
{
  "categories": [
    {
      "id": 9,
      "color": "ffffff",
      "title": "New Category",
      "ignoreResults": false
    }
  ]
}
```

This method is used to create a new category and is reserved for administrators. Administrators must include an authentication token with each request.

JSON Parameters | Description
---------- | -------
color | The six-character hexidecimal string corresponding to the new category's color.
title | The category's title.
ignoreResults | A boolean value that is `true` if this category should not be included in the results calculations. `false` otherwise.

### DELETE
> DELETE

```shell
# Delete a category by ID
curl -X DELETE "https://api.sustainability.oregonstate.edu/v2/carbon/category?ID=1" \
```

```javascript
// Response
{
  "status": 200,
  "message": "Category deleted."
}
```

This method is used to create a new category and is reserved for administrators. Administrators must include an authentication token with each request.

URL Parameters | Description
---------- | -------
ID | The ID of the category to be deleted.

## /question

This endpoint is used for performing CRUD operations on one or more questions.

### GET
> GET

```shell
# Request all categories
curl "https://api.sustainability.oregonstate.edu/v2/carbon/question"
```

```shell
# Request a specific question
curl "https://api.sustainability.oregonstate.edu/v2/carbon/question?ID=1"
```

```javascript
// Response
{
  "questions": [
    {
      "id": 0,
      "questionText": "How many miles do you drive each day?",
      "metaData": "This question is not real.",
      "input": {
        "type": "Numerical",
        "hint": "Try answering the question.",
        "value": 0,
        "unit": {
          "prefix": false,
          "chars": "mi"
        }
      },
      "trigger": {
        "triggerValue": "someValue",
        "parentQuestion": 3,
        "visible": false
      },
      "categoryID": 0
    }
  ]
}
```

This method is used to retrieve one or more questions.

URL Parameters | Description
---------- | -------
ID | The ID of the requested question. When this is specified, only one question is returned.
categoryID | When this is specified, all of the questions belonging to a particular category are returned.

<aside class="notice">
You must use either ID or categoryID. They are mutually exclusive, and one is always required.
</aside>

### POST
> POST

```shell
# Create a new question
curl -X POST "https://api.sustainability.oregonstate.edu/v2/carbon/question" \
-H "Content-Type: application/json" \
-H "Cookie: token=(put authentication token here)" -d \
'{
  "questionText": "How many miles do you drive each day?",
  "metaData": "This question is not real.",
  "input": {
    "type": "Numerical",
    "hint": "Try answering the question.",
    "value": 0,
    "unit": {
      "prefix": false,
      "chars": "mi"
    }
  },
  "trigger": {
    "triggerValue": "someValue",
    "parentQuestion": 3,
    "visible": false
  },
  "categoryID": 0
}'
```

```javascript
// Response
{
  "questions": [
    {
      "id": 999,
      "questionText": "How many miles do you drive each day?",
      "metaData": "This question is not real.",
      "input": {
        "type": "Numerical",
        "hint": "Try answering the question.",
        "value": 0,
        "unit": {
          "prefix": false,
          "chars": "mi"
        }
      },
      "trigger": {
        "triggerValue": "someValue",
        "parentQuestion": 3,
        "visible": false
      },
      "categoryID": 0
    }
  ]
}
```

This method is used to create a new question and is reserved for administrators. Administrators must include an authentication token with each request.

JSON Parameters | Description
---------- | -------
color | The six-character hexidecimal string corresponding to the new question's color.
title | The question's title.
ignoreResults | A boolean value that is `true` if this question should not be included in the results calculations. `false` otherwise.

### DELETE
> DELETE

```shell
# Delete a question by ID
curl -X DELETE "https://api.sustainability.oregonstate.edu/v2/carbon/question?ID=1" \
```

```javascript
// Response
{
  "status": 200,
  "message": "Question deleted."
}
```

This method is used to create a new question and is reserved for administrators. Administrators must include an authentication token with each request.

URL Parameters | Description
---------- | -------
ID | The ID of the question to be deleted.

## /data
This endpoint is used for retrieving and deleting a user's historical data.

### GET

### POST

### DELETE

## Error Codes

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The kitten requested is hidden for administrators only.
404 | Not Found -- The specified kitten could not be found.
405 | Method Not Allowed -- You tried to access a kitten with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
410 | Gone -- The kitten requested has been removed from our servers.
418 | I'm a teapot.
429 | Too Many Requests -- You're requesting too many kittens! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
