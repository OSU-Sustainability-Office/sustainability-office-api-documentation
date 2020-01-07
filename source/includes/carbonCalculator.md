# Carbon Calculator

The base URL for the Carbon Calculator's API is [https://api.sustainability.oregonstate.edu/v2/carbon](https://api.sustainability.oregonstate.edu/v2/carbon). The following routes can be accessed by appending the endpoint to the base URL (ie: [https://https://api.sustainability.oregonstate.edu/v2/carbon/category...](https://https://api.sustainability.oregonstate.edu/v2/carbon/category...)

## Get Categories

```shell
# Request all categories
curl "https://api.sustainability.oregonstate.edu/v2/carbon/category"
```

```shell
# Request a specific category
curl "https://api.sustainability.oregonstate.edu/v2/carbon/category?ID=1"
```

```json
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

## Create Categories

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

```json
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

## Delete Categories

```shell
# Delete a category by ID
curl -X DELETE "https://api.sustainability.oregonstate.edu/v2/carbon/category?ID=1" \
-H "Cookie: token=(put authentication token here)"
```

```json
{
  "status": 200,
  "message": "Category deleted."
}
```

This method is used to delete a category and is reserved for administrators. Administrators must include an authentication token with each request.

URL Parameters | Description
---------- | -------
ID | The ID of the category to be deleted.

## Get Questions

This endpoint is used for performing CRUD operations on one or more questions.

```shell
# Request all questions for a particular category
curl "https://api.sustainability.oregonstate.edu/v2/carbon/question?categoryID=1"
```

```shell
# Request a specific question
curl "https://api.sustainability.oregonstate.edu/v2/carbon/question?ID=1"
```

```json
{
  "questions": [
    {
      "ID": 999,
      "questionText": "How many miles do you drive each day?",
      "orderIndex": 3,
      "metaData": "This question is not real.",
      "input": {
        "type": "numerical",
        "value": 0, // this is the initial value that appears before the user modifies the input box on the calculator.
        "coef": 0.533,
        "unit": "mi",
        "isPrefix": false
      },
      "trigger": {
        "triggerValue": "Gasoline",
        "parentQuestion": 2,
        "visible": false
      },
      "categoryID": 0
    },
    ...
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

## Create Questions

```shell
# Create a new question
curl -X POST "https://api.sustainability.oregonstate.edu/v2/carbon/question" \
-H "Content-Type: application/json" \
-H "Cookie: token=(put authentication token here)" -d \
'{
  "questionText": "How many miles do you drive each day?",
  "orderIndex": 3,
  "metaData": "This question is not real.",
  "input": {
    "type": "numerical",
    "value": 0, // this is the initial value that appears before the user modifies the input box on the calculator.
    "coef": 0.533,
    "unit": "mi",
    "isPrefix": false
  },
  "trigger": {
    "triggerValue": "Gasoline",
    "parentQuestion": 2,
    "visible": false
  },
  "categoryID": 0
}'
```

```json
{
  "questions": [
    {
      "ID": 999,
      "questionText": "How many miles do you drive each day?",
      "orderIndex": 3,
      "metaData": "This question is not real.",
      "input": {
        "type": "numerical",
        "value": 0, // this is the initial value that appears before the user modifies the input box on the calculator.
        "coef": 0.533,
        "unit": "mi",
        "isPrefix": false
      },
      "trigger": {
        "triggerValue": "Gasoline",
        "parentQuestion": 2,
        "visible": false
      },
      "categoryID": 0
    }
  ]
}
```

This method is used to delete a question and is reserved for administrators. Administrators must include an authentication token with each request.

JSON Parameters | Description
---------- | -------
questionText | This is the string containing text for the question, such as "How old are you?".
orderIndex | Each question is displayed in a particular order, beginning with 0. If -1 is supplied, this will be appended to the end of the current list of questions for the specified category. Otherwise, this question will be placed at the specified index. If a question already exists at the specified index, the new question will be inserted into the list at the index.
metaData | This is displayed when the user hovers the mouse over a tooltip. This contains information regarding any sources used for computing the CO2e coefficient for this question, or any other pertinent information.
input (optional) | An object describing the type of input that should be rendered for this question.
trigger (optional) | An object describing whether or not this question's visibility is triggered by the answer to another question. For example, the question: "How many miles do you drive?" may be triggered by the response "Yes" to the question: "Do you drive a car?"
categoryID | The ID of the category this question will reside within. To look up category IDs, refer to the /category endpoint.

### Input Objects
A question can employ one of four kinds of inputs:

1. No input. This is used when a "question" is really just a paragraph. In this case, assign the input key a null value.
<pre class="center-column">
  {
    "questionText": "Welcome to the calculator.",
    "orderIndex": -1,
    "metaData": "This question is actually a paragraph.",
    "input": null,
    "trigger": null,
    "categoryID": 0
  }
</pre>
2. Numerical. This is used when a question computes a carbon footprint using an integer input by the user.
<pre class="center-column">
  {
    "questionText": "How many miles do you drive each day?",
    "orderIndex": 3,
    "metaData": "This question is not real.",
    "input": {
      "type": "numerical",
      "value": 0, // this is the initial value that appears before the user modifies the input box on the calculator.
      "coef": 0.533,
      "unit": "mi",
      "isPrefix": false
    },
    "trigger": {
      "triggerValue": "Gasoline",
      "parentQuestion": 2,
      "visible": false
    },
    "categoryID": 0
  }
</pre>
3. List. This is used when a user must select from one or more predetermined values in a list (or a toggle switch).
<pre class="center-column">
  {
    "questionText": "What kind of car do you drive?",
    "orderIndex": 2,
    "metaData": "This question is not real.",
    "input": {
      "type": "list",
      "values": ["Gasoline", "Diesel", "Hybrid", "Electric", "Other"],
      "coefs": [0.533, 0.421, 0.213, 0.048, 0],
      "unit": null,
      "isPrefix": null
    },
    "trigger": null,
    "categoryID": 0
  }
</pre>
4. Table. This is used when a user must input data in a table format.
<pre class="center-column">
  {
    "questionText": "From the following list of appliances, electronics, lighting, etc, input how many of each item are in your room and how many hours a day each item is in use or plugged in. If you own an item not listed below please be sure to fill in extra fields: What is the item and wattage? You can find the wattage on the bottom of most appliances. Be sure to multiply by 1000 if the wattage is given in kilowatts.",
    "orderIndex": 4,
    "metaData": "This question is not real.",
    "input": {
      "type": "table",
      "formula": "C1 * C2 * C3 * 0.214",
      "values": [
        ["Item", "Quantity", "Watts", "Active Use (Hours/Day)", "Standby Use"],
        ["Refrigerator", 1, 160, 24, 0],
        ["Microwave", 1, 1000, 0, 0],
        ...
      ]
    },
    "trigger": null,
    "categoryID": 0
  }
</pre>

### Trigger Objects
A question's visibility on the frontend can be triggered by another question. The user may respond to Question A favorably, "triggering" Question B's visibility. If this functionality is not desired, the trigger object can be null.

The object is constructed like this:

<pre class="center-column">
"trigger": {
  "triggerValue": "Gasoline",
  "parentQuestion": 2,
  "visible": false
}
</pre>

JSON Parameters | Description
---------- | -------
triggerValue | If the user's response to the parentQuestion is equivalent to the triggerValue, this question's visibility will be toggled.
parentQuestion | This is the orderIndex of the parent question within the current category.
visible | If true, the question will initially be visible. If false, the question will not initially be visible.

## Delete Questions

```shell
# Delete a question by ID
curl -X DELETE "https://api.sustainability.oregonstate.edu/v2/carbon/question?ID=1" \
-H "Cookie: token=(put authentication token here)"
```

```json
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
This endpoint is used for retrieving and deleting a user's historical data. The user must be logged in and an authentication token must be included with every request.

### GET
> GET

```shell
# Request all historica data for the current user
curl "https://api.sustainability.oregonstate.edu/v2/carbon/data"
```

```json
{
  "data": [
    {
      "ID": 1,
      "created": "YYYY-MM-DD hh:mm:ss", // SQL Datetime format, UTC timezone
      "totals":[
        {
          "categoryID": 1,
          "total": 1234.56
        },
        ...
      ]
    },
    ...
  ]
}
```
This method retrieves all of the historical datapoints for the current user.

### POST
> POST

```shell
# Request all historica data for the current user
curl -X POST "https://api.sustainability.oregonstate.edu/v2/carbon/data" \
-H "Content-Type: application/json" \
-H "Cookie: token=(put authentication token here)" -d \
'{
  "totals":[
    {
      "categoryID": 1,
      "total": 1234.56
    },
    ...
  ]
}'
```

```json
{
  "data": [
    {
      "ID": 999,
      "created": "YYYY-MM-DD hh:mm:ss", // SQL Datetime format, UTC timezone
      "totals":[
        {
          "categoryID": 1,
          "total": 1234.56
        },
        ...
      ]
    },
    ...
  ]
}
```
This method stores a results object as a historical data point.

### DELETE
> DELETE

```shell
# Delete the specified historical data point
curl -X DELETE "https://api.sustainability.oregonstate.edu/v2/carbon/data?ID=1" \
-H "Cookie: token=(put authentication token here)"
```

```json
{
  "status": 200,
  "message": "Data point deleted."
}
```

This method deletes the specified historical data point.

URL Parameters | Description
---------- | -------
ID | The ID of the historical data point to be deleted. Each data point unique consists of a set of totals for each category and a timestamp.

## Error Codes

(Incomplete)

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
