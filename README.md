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

---
To create a GitHub OAuth application, follow these steps:

1. Go to the GitHub Developer Settings page: Visit the GitHub website and log in to your account. From your account dropdown, select "Settings", then navigate to the "Developer settings" section.

2. Create a new OAuth application: In the Developer settings page, click on "OAuth Apps" in the left sidebar. Then, click on the "New OAuth App" button.

3. Provide application details: Fill out the required fields in the new OAuth application form. Here are some important fields:

   - **Application name**: Enter a name for your OAuth application.
   - **Homepage URL**: Provide the URL of your application's homepage.
   - **Authorization callback URL**: Enter the URL where GitHub should redirect users after authorization. This is typically the URL of a callback endpoint in your application.

4. Configure application permissions: Choose the scopes or permissions that your OAuth application requires. These permissions determine the level of access your application will have when users authenticate with it.

5. Register the application: After filling out all the required information, click on the "Register application" button to create your OAuth application.

6. Retrieve your OAuth application credentials: Once your application is registered, you will be redirected to the application details page. On this page, you can find your **Client ID** and **Client Secret**. These credentials will be needed to authenticate your application with GitHub's OAuth API.

Keep in mind that you should securely store your client secret and avoid exposing it publicly or committing it to version control. It's recommended to use environment variables or a secure configuration mechanism to manage these credentials.

That's it! You have now created a GitHub OAuth application, which will allow your application to authenticate users and interact with the GitHub API on their behalf.
