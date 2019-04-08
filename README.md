# amazon-guardduty-to-slack
Demonstrates sending Amazon GuardDuty findings to your Slack Channel 

## Prerequisites:

You must have your own slack account
  
## Step 1:
Create an incoming webhook in slack
- Go to your slack application and select your team on the top left corner as shown:
- You will find a popup Menu and you’ll want to click on Manage Apps.
- You will then want to select custom integrations on the left and Incoming Webhooks.
- Select the slack channel that you’d like to post messages to with this new incoming web hook.  An example would be #general.
- Press the button to add the incoming web hook at the bottom of the page.
- Copy the new Webhook URL so we can use it as input in our CloudFormation template.

## Step 2:
Use the CloudFormation service to execute the gd2slack.template in this repository
- You will add your incoming web hook as the first parameter in the template
- Add the slack channel as a parameter - example #general
- Add the minimum severity - example HIGH would only send high severity findings, LOW sends all findings
- Acknowledge that the template will create IAM resources and execute it

## Thats it!  The template will run for about 5 minutes and you are ready to go.

To test the template be sure that you have GuardDuty enabled in the same region.
You can then generate some sample findings.  In a few minutes, you should see 
the findings showing up in your slack channel.  

### Extending the sample and making it your own

This project is intended to be a sample and I embedded the lambda code directly into the 
CloudFormation template to make it simple to do an initial deployment to any region. The
downside of doing this is that the lambda function is limited to 4096 characters and
its node.js embedded in JSON which is difficult to work with.  If you want to extend
the sample, I'd recommend that you package up the lambda code in your own S3 bucket. You
would then just replace the ZipFile parameter in the CloudFormation to the S3Bucket and
S3Key of your lambda function.  

## License

This sample code is made available under the MIT-0 license. See the LICENSE file.
