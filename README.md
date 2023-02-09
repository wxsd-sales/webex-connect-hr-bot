# Webex Connect HR Bot

This is a Webex Messaging Bot which runs on the Webex Connect CPaaS platform. It leverages the Webex Connect Q&A Bot builder to respond to users queries and also can process Adaptive Card Actions via the flow and communicate with other integration services..

![image](https://user-images.githubusercontent.com/21026209/217918129-07f1cc12-52c4-4008-983d-c9255455557b.png)

## Requirements

1. Webex Connect Sandbox - Available to setup here: https://imimobile.com/products/webex-connect/sandbox
2. Webex Messaging Bot Token - Guide available here: https://developer.webex.com/docs/bots

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

5. Next, click ont eh Q&A Bot node and select the Bot you made ealier:

![image](https://user-images.githubusercontent.com/21026209/217933429-9eb85882-c9e0-47c1-a27e-edf57b62a436.png)

6. Update the receive node and select the Webhook you created ealier and configure the following resume keys and values:

![image](https://user-images.githubusercontent.com/21026209/217934456-0498c7d0-66cc-428e-abd6-951e38c50f87.png)

7. Connect the ``Receive`` node to the ``Data Parser`` to the right

![image](https://user-images.githubusercontent.com/21026209/217934837-69ddf7e0-ccf3-4378-bc75-21b06e39813d.png)

8. Save the flow changes and click make live. Set the Webex Messaging Bot as variable ``Bearer <token>`` and set the Bots name & email and update the support mailer.

![image](https://user-images.githubusercontent.com/21026209/217935728-5c85657a-323f-45c2-85a0-be121fd02485.png)

### Configure Webex Webhooks

1. Create the Webex Webhook to point to the Webex Connect flows Webhook trigger so your Bot gets notified of any new Messages, Actions or Membership changes. More information available here: https://developer.webex.com/docs/webhooks


## Support

Please reach out to the WXSD team at [wxsd@external.cisco.com](mailto:wxsd@external.cisco.com?subject=room-presets-macro)
