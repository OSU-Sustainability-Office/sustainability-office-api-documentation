# Carbon Calculator

The base URL for the Carbon Calculator's API is [https://api.sustainability.oregonstate.edu/v2/carbon](https://api.sustainability.oregonstate.edu/v2/carbon). The following routes can be accessed by appending the endpoint to the base URL (ie: [https://https://api.sustainability.oregonstate.edu/v2/carbon/category...](https://https://api.sustainability.oregonstate.edu/v2/carbon/category...)

## /category
This endpoint is used for performing CRUD operations on one or more categories.

### GET
This endpoint is used to retrieve one or more categories.

URL Parameters | Description
---------- | -------
ID (Optional) | The ID of the requested category. When this is specified, only one category is returned.

```shell
# Request all categories
curl "https://api.sustainability.oregonstate.edu/v2/carbon/category"
```

```shell
# Request a specific category
curl "https://api.sustainability.oregonstate.edu/v2/carbon/category"
```

### POST

### DELETE

## /question
This endpoint is used for performing CRUD operations on one or more questions.

### GET

### POST

### DELETE

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
