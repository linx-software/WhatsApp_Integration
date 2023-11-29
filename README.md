# WhatsAppMessenger Integration - Linx 

  

## Description 

This repo contains a Linx 6 solution that shows how you can integrate with the [WhatsAppAPI](https://business.whatsapp.com/developers/developer-hub). The sample contains functions that will send messages (via a template, text and interactive message), as well as a SimpleRestHost that will allow you to receive messages from the WhatsAppwebhook. You will need to set up the API and WebHook on your WhatsAppBusiness Developer account before you will be able to use this template. You will also require a Linx Server to host the REST API to receive messages.  

You can download this sample and manipulate it to suit your integration using [Linx 6](https://linx.software/). 

  

## Installation 

This is a Linx 6 solution, so you will need an installed version of the [Linx 6 designer](https://linx.software/linx-download/) to work on this solution and to add in your own logic.  

You will also need to have a Linx Server to host the REST host in order to receive the messages from the WhatsAppwebhook. Details below. 

 

### WhatsAppSetup 

You will require a WhatsAppBusiness and Developer account. You can follow the details to set this up on the [documentation](https://business.whatsapp.com/developers/developer-hub) 

You will also need to set up your API. This will give you a temporary token as well as a test number (to test with). You can later set a permanent token and add a business phone number. Pease note that at the time of writing you can only send the template “hello_world” message with a test number. You will also need to add test numbers that the message can be sent to. Later when you have added a business number and set up billing you can send messages to more numbers.  

In order to receive messages you will need to configure the WebHook. Before this can be done, deploy the solution to a Linx Server, set the Base URI and the Webhook_Verification_Token in the Settings. The Webhook_Verification_Token will be used when setting up the Webhook as the token. Once the SimpleRESTHost service is turned on, you can configure the Webhook details on your WhatsAppdeveloper portal. Set the Callback URL to be the Base URL you set in Linx and the Token to the Webhook_Verification_Token. 

Important note: The Callback URL will be your REST_BASE_URL + “\webhooks” - else it will not work.  

 

## Usage 

 The solution has the following settings that needs to be set: 

- PhoneNumber_ID : The Phone Number ID retreived from your WhatsAppDeveloper Portal under the API Setup section 

- Token : The Temporary access token retreived from your WhatsAppDeveloper Portal under the API Setup section. This will be changed to be your permanent token once that is set up 

- REST_BASE_URL: The base URI of your Linx REST HOST API that the Webwook will send messages to. This will be used as the Callback URL (add \webhook to this) 

- Webhook_Verification_Token : The verification token that must match the one on your Webhook configuration on the WhatsAppDeveloper portal 

- Database_Connection : The database connection string you will use to store your messages. Not needed if you are not going to connect to a database 

  

The solution has 3 main functions: 

  

#### SendMessage_Template: 

This function will send a message template to a number. It received the target phone number as an input parameter. It will then construct the API endpoint by using the PhoneNumber_ID setting. It will send the “hello_world” template, this is the pre-approved template that can be sent as a test from your WhatsAppbusiness account. No other template will work while testing, when you have set up a business phone number and billing you can send other templates.  

  

#### SendMessage_Text: 

This function will send a message template to a number. It received the target phone number as an input parameter as well as the text to be sent. It will then construct the API endpoint by using the PhoneNumber_ID setting. It will send the text to the specified phone number. Please note that this will not work on a testing phone number, you will need to set up a business phone number and billing in order to send text messages (at the time of writing). 

 

#### SendMessage_Interactive 

This function will send a message template to a number. It received the target phone number as an input parameter. It will then construct the API endpoint by using the PhoneNumber_ID setting. You will need to construct the Interactive message in the Body_Interactive type, here you can set the message as well as the buttons. Please note that this will not work on a testing phone number, you will need to set up a business phone number and billing in order to send text messages (at the time of writing). 

 

 ### Receive Messages 

The solution also contains a SimpleRESTHost to receive messages from the WhatsAppWebhook. You can follow configuration for the webhook [here](https://developers.facebook.com/docs/whatsapp/cloud-api/get-started#configure-webhooks) - note that you do not need to do step 5. Please note that you need to subscribe to receive messages in the Webhook fields. 

Documentation on how the webhook works can be found [here](https://developers.facebook.com/docs/graph-api/webhooks/getting-started#verification-requests)

#### Webhooks_Validate 

This operation will be used when the webhook validates the connection. It will receive the Token, challenge and mode. It will check that the token matches that set in the settings, and will then send back the challenge as a response.  

#### Webhooks_Notifications 

This operation is used to receive messages. As an example, the operation loops through the elements to extract the message. Typically the webhook will send a message through 4 times, so you may need to filter out by using the message ID.  

## Contributing 

For questions please ask the [Linx community](https://linx/software/community). 

  

## License 

[MIT](https://github.com/linx-software/template-repo/blob/main/LICENSE.txt) 

 
