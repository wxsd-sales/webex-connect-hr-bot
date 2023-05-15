# Webex Connect HR Bot


This is a Webex Messaging Bot which runs on the Webex Connect CPaaS platform. It leverages the Webex Connect Q&A Bot builder to respond to users queries and also can process Adaptive Card Actions via the flow and communicate with other integration services..

<img width="1684" alt="image" src="https://user-images.githubusercontent.com/21026209/227618565-db187c29-83f8-4f73-a675-b0d6b2a6f627.png">


- Webex Connect Sandbox - Available to setup here: https://imimobile.com/products/webex-connect/sandbox
- Webex Messaging Bot Token - Guide available here: https://developer.webex.com/docs/bots

## Setup

### Setup Webex Connect Q&A Bot

1. On your Webex Connect Sandbox, navigate to the Bot builder in the App tray:

![image](https://user-images.githubusercontent.com/21026209/217930701-c6ddd4c6-3cf3-4d47-b992-470c6a7ea603.png)

2. At the top right, click ``+ New Q&A Bot``:

![image](https://user-images.githubusercontent.com/21026209/217930978-255a84e6-cf6f-4f4a-8c6d-839958e8fadd.png)

3. Give your Bot a name and click done:

![image](https://user-images.githubusercontent.com/21026209/217931382-4baa2c9e-f631-4026-97de-fced60cb0066.png)

4. This will create a basic Q&A Bot with default articles and responses, you can add more responses to the Bot as needed.

### Setup Webex Connect Flow

1. Download the ``sandbox.workflow`` file from this repo 
2. Create a new Flow on your Webex Connect Sandbox and select the Upload a flow method and use the ``sandbox.workflow`` file
![image](https://user-images.githubusercontent.com/21026209/217921331-0dec5504-b253-46ee-95ee-d59520165782.png)

3. Modify the Webhook and create a new Webex for this Flow and use the following JSON template and parse it:
```js
{
    "id": "This Webhook Notification event Ud in  Base64 id",
    "name": "Name of Webhook associated with the event",
    "targetUrl": "This Webhook URL which this event notification is for",
    "resource": "messages | membership | attachmentActions",
    "event": "created | deleted",
    "orgId": "Base64 Webex Org Id",
    "createdBy": "Base64 person Id",
    "appId": "Base64 Bot Id",
    "ownedBy": "creator",
    "status": "active",
    "created": "2022-10-11T20:19:27.591Z",
    "actorId": "Base64 person Id",
    "data": {
        "id": "Message/Membership/Action Base64 id",
        "roomId": "RoomId Base64",
        "roomType": "direct|group only available for message events",
        "messageId": "MessageId given separate for Actions",
        "personId": "Message creators personId Base64",
        "personEmail": "user@example.com",
        "created": "2022-10-13T17:31:28.884Z",
        "parentId": "MessageId of the parent message, only available for a new message in a thread",
        "type": "submit"
    }
}
```
4. Set the following conditions on the Webhook:

![image](https://user-images.githubusercontent.com/21026209/217930336-be959f9d-97d1-4552-892b-d506c6f6e752.png)

5. Next, click ont eh Q&A Bot node and select the Bot you made earlier:

![image](https://user-images.githubusercontent.com/21026209/217933429-9eb85882-c9e0-47c1-a27e-edf57b62a436.png)

6. Save the flow changes and click make live. Set the Webex Messaging Bot as variable ``Bearer <token>`` and set the Bots name & email and update the support mailer.

![image](https://user-images.githubusercontent.com/21026209/217935728-5c85657a-323f-45c2-85a0-be121fd02485.png)

### Configure Webex Webhooks

1. Create the Webex Webhook to point to the Webex Connect flows Webhook trigger so your Bot gets notified of any new Messages, Actions or Membership changes. More information available here: https://developer.webex.com/docs/webhooks

  
## Demo

*For more demos & PoCs like this, check out our [Webex Labs site](https://collabtoolbox.cisco.com/webex-labs).


## License

All contents are licensed under the MIT license. Please see [license](LICENSE) for details.


## Disclaimer

Everything included is for demo and Proof of Concept purposes only. Use of the site is solely at your own risk. This site may contain links to third party content, which we do not warrant, endorse, or assume liability for. These demos are for Cisco Webex use cases, but are not Official Cisco Webex Branded demos.


## Questions
Please contact the WXSD team at [wxsd@external.cisco.com](mailto:wxsd@external.cisco.com?subject=room-presets-macro) for questions. Or, if you're a Cisco internal employee, reach out to us on the Webex App via our bot (globalexpert@webex.bot). In the "Engagement Type" field, choose the "API/SDK Proof of Concept Integration Development" option to make sure you reach our team. 

