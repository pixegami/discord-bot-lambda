# Discord Bot on AWS Lambda

This repo is an example of how to run a Discord bot on AWS Lambda. It uses [Discord Interactions Endpoint](https://discord.com/developers/docs/interactions/application-commands).

The app is built with [Flask](https://flask.palletsprojects.com/) to create a HTTP server.
The server is hosted on AWS Lambda Docker Container using [AWS CDK](https://aws.amazon.com/cdk/).

Once you've replaced updated all the tokens and keys, you can deploy the bot to AWS Lambda with the CDK. You'll then get an API endpoint like `https://xxxxx.execute-api.us-east-1.amazonaws.com/prod/`.

You can then update the Discord application's interactions endpoint to point to that URL on your [Discord Developer Portal](https://discord.com/developers/applications), and interact with the bot in your Discord server (after you've added it to the server).

### Registering the Commands

Before you can use the bot, you'll need to register the commands with Discord.

Modify/update the `discord_commands.yaml` file to add your own commands. Also install the dependencies in `requirements.txt` if you haven't already.

```sh
pip install -r commands/requirements.txt
```

Then update the API key and application ID in `register_commands.py` to match your own. Then run the `register_commands.py` script in the `commands` directory.

```sh
cd commands
python register_commands.py
```

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

But this won't work with the `@verify_key_decorator`, because the request won't have a token that works with the public key.

So you'll need to comment out the decorator to test locally or update the example request with a valid token from your Lambda logs.

### Deploying to AWS Lambda

Bootstrap the CDK if you haven't already.

```sh
cdk bootstrap
```

Then you can run this to deploy it (make sure your AWS CLI is set up first).

```sh
cdk deploy
```
