# Discord Bot on AWS Lambda

## Testing Locally

Send a request to the Flask app this way. Put a sample request (which you can get by logging the JSON in Lambda). PUt it in `test_request.json`. Then start up the bot as
a Flask app. Then send the request to the Flask app.

```sh
curl -X POST -H "Content-Type: application/json" -d @test_request.json http://127.0.0.1:5000/
```
