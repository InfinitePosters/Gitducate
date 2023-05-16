# Gitducate
Build a plataform to elevate your knowledge by Github
---
Here are the steps on how to connect Discord API to GitHub API using AWS:

1. Create a Discord application.
2. Create a GitHub OAuth application.
3. Create a Lambda function in AWS.
4. Configure the Lambda function to use the Discord and GitHub APIs.
5. Deploy the Lambda function.
6. Create an API Gateway endpoint for the Lambda function.
7. Configure the Discord application to use the API Gateway endpoint.
8. Test the integration.

Here are the detailed steps for each step:

**1. Create a Discord application.**

Go to the Discord Developer Portal and create a new application. In the "General" tab, enter a name for your application and select a bot to represent your application. In the "OAuth & Permissions" tab, enable the "Bot" scope and the "OAuth2 Application" scope. Click the "Create Application" button.

**2. Create a GitHub OAuth application.**

Go to the GitHub Developer Portal and create a new OAuth application. In the "Application name" field, enter a name for your application. In the "Homepage URL" field, enter the URL of your website or blog. In the "Authorization callback URL" field, enter the URL of the Lambda function that you will create in step 3. Click the "Create application" button.

**3. Create a Lambda function in AWS.**

Go to the AWS Lambda console and create a new Lambda function. In the "Basic information" section, enter a name for your function and select the "Python 3.8" runtime. In the "Role" section, select the "Create a new role" option and select the "Basic Lambda execution role" option. Click the "Create function" button.

In the Lambda function code editor, paste the following code:

```python
import json
import requests

def lambda_handler(event, context):
    # Get the Discord message data.
    message_data = json.loads(event["body"])

    # Get the GitHub OAuth token.
    github_oauth_token = os.environ["GITHUB_OAUTH_TOKEN"]

    # Create a GitHub API request.
    github_api_url = "https://api.github.com/repos/<OWNER>/<REPO>/issues"
    github_api_headers = {
        "Authorization": "Bearer " + github_oauth_token,
        "Content-Type": "application/json",
    }

    # Create the GitHub issue.
    github_issue_data = {
        "title": message_data["content"],
        "body": message_data["content"],
    }
    requests.post(github_api_url, headers=github_api_headers, data=json.dumps(github_issue_data))

    return {
        "statusCode": 200,
        "body": "Success!",
    }
```

In the "Environment variables" section, add the following environment variable:

* GITHUB_OAUTH_TOKEN: The GitHub OAuth token for your application.

Click the "Save" button.

**4. Configure the Lambda function to use the Discord and GitHub APIs.**

In the Lambda function configuration, add the following triggers:

* Discord: Incoming Webhook
* GitHub: Webhook

**5. Deploy the Lambda function.**

Click the "Deploy" button.

**6. Create an API Gateway endpoint for the Lambda function.**

Go to the AWS API Gateway console and create a new API. In the "Create API" wizard, select the "REST API" option and click the "Next" button.

In the "API name" field, enter a name for your API. In the "Endpoint type" section, select the "Regional" option. Click the "Next" button.

In the "Resources" section, click the "Create resource" button. In the "Resource name" field, enter a name for your resource. In the "Resource path" field, enter the path to your Lambda function. Click the "Create resource" button.

In the "Method settings" section, select the "GET" method. In the "Integration type" section, select the "Lambda" option. In the "Lambda function" field, select the Lambda function that you created in step 3. Click the "Save" button.

**7. Configure the Discord application to use the API Gateway endpoint.**

In the Discord Developer Portal, go to the "OAuth & Permissions" tab. In the "Bot Endpoints" section, enter the URL of the
