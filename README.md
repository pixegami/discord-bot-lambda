# Discord Bot on AWS Lambda

### Testing Locally

Send a request to the Flask app this way. Put a sample request (which you can get by logging the JSON in Lambda). PUt it in `test_request.json`.

Start up the bot as a Flask app.

```sh
python src/app/main.py
```

Then send the request to the Flask app.

```sh
curl -X POST -H "Content-Type: application/json" -d @test_request.json http://127.0.0.1:5000/
```

### Deploying to AWS Lambda

Bootstrap the CDK if you haven't already.

```sh
cdk bootstrap
```

Then you can run this to deploy it (make sure your AWS CLI is set up first).

```sh
cdk deploy
```
