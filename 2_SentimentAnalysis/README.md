# Module 2: Sentiment Analysis using Comprehend

In this module you'll use [Amazon API Gateway](https://aws.amazon.com/api-gateway/), [AWS Lambda](https://aws.amazon.com/lambda/) and [Amazon Comprehend](https://aws.amazon.com/comprehend/) to analyze the feedback that users enter through the web page. The browser application that you deployed in the first module allows users to enter their name and feedback. The JavaScript running in the browser invokes an API Gateway method, which executes a Lambda function to persist the information entered in a DynamoDB table.
 
In order to activate “Predict Sentiment” functionality, you will add another method in your API Gateway and a corresponding Lambda function. The Lambda function will invoke Amazon Comprehend Service API to predict the sentiment expressed in user's feedback.

## Architecture Overview

The architecture for this module is composed of AWS Lambda function that leverage the sentiment analysis capabilities of Amazon Comprehend. Feedback entered by the user through the web page is persisted in a DynamoDB table. Upon the request from the web page, API Gateway invokes the Lambda function, which sends an API call to Comprehend to do the sentiment analysis. The result is saved to the DynamoDB table and the web page gets refreshed to show the result of the analysis, both through the Lambda function and API Gateway.  

![Sentiment Analysis Architecture](images/sentiment-analysis-architecture.jpg)

## Implementation Instructions

Each of the following sections provide an implementation overview and detailed, step-by-step instructions. The overview should provide enough context for you to complete the implementation if you're already familiar with the AWS Management Console or you want to explore the services yourself without following a walkthrough.

If you're using the latest version of the Chrome, Firefox, or Safari web browsers the step-by-step instructions won't be visible until you expand the section.

### 1. Create a Lambda Function 

#### Background

AWS Lambda will run your code in response to events in this case from API Gateway (which we will cover in the next section). In this step you'll build the core function that will process API requests (via API Gateway) from the web application to detect a sentiment of a feedback text. In the next section you'll use Amazon API Gateway to create a RESTful API that will expose an HTTP endpoint that can be invoked from your users' browsers. You'll then connect the Lambda function you create in this step to that API in order to create a fully functional backend for your web application.

#### High-Level Instructions

Use the AWS Lambda console to create a new Lambda function called `PredictFeedbackSentiment-username` that will process the requests. Replace "username" for your emails address without the "@company.com" part.

Make sure to configure your function to use the `VOCLambdaRole-username` IAM role you created in the previous section.

<details>
<summary><strong>Step-by-step instructions (expand for details)</strong></summary><p>

1. Choose on **Services** then select **Lambda** in the Compute section.

1. Click **Create function**.

1. Keep the default **Author from scratch** card selected.

1. Enter `PredictFeedbackSentiment-username` in the **Name** field.

1. Select **Python 3.6** for the **Runtime**.

1. Ensure `Choose an existing role` is selected from the **Role** dropdown.

1. Select `VOCLambdaRole-username` from the **Existing Role** dropdown.
    ![Create Lambda function screenshot](images/create-lambda-function.png)

1. Click on **Create function**.

1. Scroll down to the **Function code** section and replace the exiting code in the **lambda_function.py** code editor with the contents of [predictfeedbacksentiment.py](functions/predictfeedbacksentiment.py).

    ![Create Lambda function screenshot](images/create-lambda-function-code.png)

1. Scroll down to the **"Environment sariables"** section and add an environment variable with Key `table_name` and Value - `UnicornCustomerFeedback-username`.
    ![Create Lambda function screenshot](images/create-lambda-env-var.png)
    
1. Click **"Save"** in the upper right corner of the page.

</p></details>

### 2. Add Policy to Lambda Execution Role 

#### Background

In Module 1,  you have created Lambda execution role `VOCLambdaRole-username`. In order for your Lambda function you created in the step 1 to call the Comprehend API, you will need to add policy to grands your Lambda function permission to detect sentiment. 

#### High-Level Instructions

Use the IAM Management Console to add a policy to the exisitng role. Go to the Lambda execution role you created in Module 1. You'll need to create a custom inline policy for the role that allows the `comprehend:DetectSentiment` action. 

<details>
<summary><strong>Step-by-step instructions (expand for details)</strong></summary><p>

1.	Go to the IAM Management Console, and look for the `VOCLambdaRole-username` role you created in the Module 1.

1.	Select the `VOCLambdaRole-username` role that you created in the Module 1.

1.	On the Permissions tab, choose the **Add inline policy** link in the lower right corner to create a new inline policy. 
	![Inline policies screenshot](images/inline-policies.png)

1. Select **Choose a service**.

1. Begin typing `Comprehend` into the search box labeled **Find a service** and select **Comprehend** when it appears. 
	![Select policy service](images/select-policy-service.png)
	
1. Choose **Select actions**.

1.	Begin typing `DetectSentiment` into the search box labeled **Filter actions** and check the box next to **DetectSentiment** when it appears.

1. Choose **Review Policy**.

1. Enter `ComprehendDetectSentiment` for the policy name and choose **Create policy**.
    ![Review Policy](images/review-policy.png)
	
</p></details>

## Implementation Validation

For this section you will test the function that you built using the AWS Lambda console. In the next section you will add a REST API with API Gateway so you can invoke your function from the browser-based application that you deployed in the first module.

1. From the main edit screen for your function, select **Configure test event** from the the **Select a test event...** dropdown.
    ![Configure test event](images/configure-test-event.png)
	
1. Keep **Create new test event** selected.

1. Enter `TestAnalyzeSentiment` in the **Event name** field

1. Insert JSON request body similar to the following into the test event editor:

	```JSON
    {
        "ID": "271605fb-f9f0-4d63-b3fd-578a4a5d8c04,f92921dc-bed1-4af0-98ec-eb128add7cf3"
    }
    ```
    Replace the IDs specified with the IDs of the item you have in the DynamoDB table - `UnicornCustomerFeedback`. You can find the items inserted into DynamoDB table flom DynamoDB console, by looking inside the table `UnicornCustomerFeedback`. 
    ![DynamoDB Entries](images/dynamodb-entries.png)
    
    Items will get inserted there as you keep using the web application created in Module-1.
    You can insert as many items and use as many of those IDs as you like. In case of multiple IDs, you have to separate the entries with comma(,).
    ![Configure test event](images/configure-test-event-2.png)
	
1. Click **Create**.

1. On the main function edit screen click **Test** with `TestAnalyzeSentiment` selected in the dropdown.   

1. Scroll to the top of the page and expand the **Details** section of the **Execution result** section.

1. Verify that the execution succeeded and that the function result looks similar to the following (actual results will vary depedning on the feedbacks records you used):

    ```JSON
    [
    "271605fb-f9f0-4d63-b3fd-578a4a5d8c04 - POSITIVE",
    "f92921dc-bed1-4af0-98ec-eb128add7cf3 - NEGATIVE"
    ]
    ```
    Status of `Execution result` should display as **"succeeded"**, and expanding the section should show the summary and log output as shown below. 
    ![Test event execution result](images/test-event-result.png)
    
After you have successfully tested your new function using the Lambda console, you can move on to the next section.

### 3. Add a Resource and Method to the existing REST API

API Gateway calls the Lambda function we created at the previous step. Create a GET method that invokes the Lambda function and passes the IDs of each user feedback as an event. 

Create a new resource called `/predictsentiment` within your API. Then create a GET method for that resource and configure it to use a Lambda proxy integration backed by the `PredictFeedbackSentiment` function you created in the previous section.

<details>
<summary><strong>Step-by-step instructions (expand for details)</strong></summary><p>

1. In the left nav, click on **Resources** under your NLPWorkshopAPI.

1. From the **Actions** dropdown select **Create Resource**.

1. Enter `predictsentiment` as the **Resource Name**.

1. Ensure the **Resource Path** is set to `predictsentiment`.

1. Select **Enable API Gateway CORS** for the resource. 

1. Click **Create Resource**.

    ![Create resource screenshot](images/create-resource.png)

1. With the newly created `/predictsentiment` resource selected, from the **Action** dropdown select **Create Method**.

1. Select `GET` from the new dropdown that appears, then **click the checkmark**.

    ![Create method screenshot](images/create-method.png)

1. Select **Lambda Function** for the integration type.

1. Select the Region you are using for **Lambda Region**.

1. Enter the name of the function you created in the previous module, `PredictFeedbackSentiment-username`, for **Lambda Function**.

1. Choose **Save**. Please note, if you get an error that you function does not exist, check that the region you selected matches the one you used in the previous module.

    ![API method integration screenshot](images/api-integration-setup.png)

1. When prompted to give Amazon API Gateway permission to invoke your function, choose **OK**.

1. Click to open the **Method Request** card.

1. Open the **URL Query String Parameters**, and click on **Add query string** link. Enter Name as `Id` and then **click the checkmark**.

	![API method request 1 screenshot](images/api-query_string-setup.png)

1.	Go back to the previous screen and choose **Integration Request** card.

1.	Scroll down to see Body Mapping Templates and open the section by clicking on the arrow on the left side. 

1.	Click on **Add mapping template** link and type `application/json` in the textbox.

	![API method request 2 screenshot](images/api-body_mapping--template-setup.png)

1.	When you save it by clicking on the checkmark, it will bring up a text area. Type `{ "ID": "$input.params('Id')" }` into it and press the save button. 

	![API method request 3 screenshot](images/api-body_mapping-template.png)

</p></details>

### 4. Deploy Your API

From the Amazon API Gateway console, choose Actions, Deploy API. You'll be prompted to create a new stage. You can use prod for the stage name.

<details>
<summary><strong>Step-by-step instructions (expand for details)</strong></summary><p>

1. In the **Actions** drop-down list select **Deploy API**.

1. Select the deployment stage named `vocweb` created in the previous modules in the **Deployment stage** drop-down list. This will add the additional method to the same deployment, so that the endpoint base URL stays the same.

    ![API Re-deploy](images/deploy-api.png)

1. Choose **Deploy**.

1. Note the **Invoke URL**, it should stay the same as the one created during the previous module. The Javascript file under `js/config.js` in your website config bucket should already have the same URL specified for `invokeUrl`. 

</p></details>

## Implementation Validation

**Note:** It's possible that you will see a delay between updating the config.js file in your S3 bucket and when the updated content is visible in your browser. You should also ensure that you clear your browser cache before executing the following steps. 

1.	Visit `/enterfeedback.html` under your website domain.

1.	Enter a test **First Name**, **Last Name** and **Feedback**.

1.	Click **Submit** button. It will redirect to a list of customer names and feedback.

1.	Choose checkbox of the feedback you want to detect sentiment.

1.	Click on **Predict Sentiment** button. It will refresh the page and load the result of the sentiment detection.

![VOC Webapp screenshot](images/voc-webapp-homepage-with-sentiments.png)

Congratulations, you have completed the module 2 of the NLP Workshop!
