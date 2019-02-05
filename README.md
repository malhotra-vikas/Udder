# Alexa Skills - Pirates of cruising
A simple Alexa skill that interacts with the user and captures details for creating an offline cruise catelog
Checkout the GIT project and run "mvn assembly:assembly -DdescriptorId=jar-with-dependencies package" in  order to 
build the project as well as to create the cruisewizard-1.0-jar-with-dependencies.jar that needs to be running on
AWS Lambda in order for the skill to work
 
## Interaction Examples

### One-shot model:
    Alexa open pirates of cruising
 
### Skill Artifacts
The skill is currently hosted on my AWS. There are three broad artifacts for the skill
1. The skill deployed at developer.amazon.com with the skill ID amzn1.ask.skill.15b2e00b-d31e-4e76-b58c-07455c73f072. 
The skill currently support en_US however we can support de_DE easily by selecting the German language in the 
Language Settings of the skill. Once the de_DE is setup, copy Skill's JSON file from en_US to de_DE context. You will 
need to translate the skill's spoken text. Do not translate the Intent Name and Slot Names. Do translate the 
Utterances for the intent and slots

2. The Skill's Lambda is a Java jar that is currently running in my AWS. The Lambda is setup to work for the 
"main.java.com.mconsultants.alexa.UtterDevSpeechletRequestStreamHandler" as the handler

3. The skill uses SES in order to send emails, the SES credentials are setup in the AWSeMailService.java file

### How to deploy and test the skill
1. Create a new custom, skill https://developer.amazon.com/alexa 
2. Copy the skill's JSON file (speechAssets/skillBuilder.json) from project's git directory and paste it to the skill's under its
JSON Editor
3. Save the model
4. Go to Permissions and check, Customer name (Full Name ) and Customer Email Address
5. Go to EndPoint and copy the skill's ID
6. Paste the skill's ID at the project's src/main/skill.property
7. Update the skill property with the from and to email that you plan on using
8. Create a new Lambda in your account by visiting https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions
9. Add Alexa skill kit as the trigger for lambda. Configure your skill's ID with the Lambda
10. Setup the Lambda Execution role (lambda_Basic_Execution) to have access to SES
11. Update Lambda's timeout to 30 sec
12. Copy Lambda's ARN and paste it to the skill's service end point
13. Build the code and upload the jar from project's target folder to the Lambda
14. Save and Publish (under Actions) the Lambda
15. Save and Build the skill's model 
16. Test the skill by invoking the skill "Alexa open pirates of cruising"
