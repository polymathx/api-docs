# Errors

> An example error code from the API result.

```json
{
    "error": 404,
    "message": "No content found with that query."
}
```

If a transaction with the API fails, you will be returned with a set of JSON representing the error. The Polymath API uses the following error codes:


Error Code | Meaning
---------- | -------
404 | Content or endpoint data not found
500 | Internal Server Error -- We had a problem with our server, or your query failed. Try again later, or contact an account representative if this persists.

<aside class="notice">
If the errors you experience are not due to lack of content, or you believe the error to be the result of a bug please contact your account representative. 
</aside>