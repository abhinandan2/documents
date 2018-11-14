# The Epic Json
**We are the music-makers and we are the dreamers of dreams.**

## Structure
The JSON has three main part:
 1. System info
 2. Meta Data
 3. Messages Array
 
### System Info
`System_info` shall contain all the data related to the environment of the widget. So information like customer id, session id and other global informantion shall be put here. 
It is highly recommended to create object even of entities with single attribute. For example, instead of `system_info.customer_id` prefer to keep `system_info.customer.id`. This way we can add further attributes of customer, if we need them in future, with ease.
```
{
    system_info : {
        customer: {
            id: "UID",
        },
        session: {
            id: "Session UID",
        }
    }
}
```
### Meta Data
Meta Data field is used to send special information to the widget. 
Meta data field is mutually exclusive with Messages field.
Such as, we can send the special information of `typing_on` or `typing_off` in meta data, viz:
(To be developed further.)
```
{
    meta_data: {
        sender_action: "typing_on",
    }
}
```

### Messages

Messages field will include an array of succesive message object, each defining a single message to be sent. Hence, at once, you may send multiple messages to be displayed in succession. 

Message field shall have 4 attributes:
1. Type
2. Message ID
3. Payload
4. Properties

#### Type
Type will define the *type* fo the message to be displayed. All the types are categorised in four groups:
1. Text: Simple text messages.
2. Styled Text: Text with styled elements such as color and size.
3. Quickreply components: Quickreply include components that *assist to take input from user*. Buttons, Calendar, Checkboxes, Date-Time picker, etc. are included here.
4. Message Components: Message Components include components that *are custom made to display certain information to the user.* Example include components like Flight Info, Generic Card, List Card, Summary Card, etc.

#### Message ID
Message ID is the UID associated with the whole message element. This ID would be used to remove or update the whole message.

#### Payload
Payload will contain the data of the selected type. 

| Type Selected | Payload Options |
| ---- | ---- |
| text | `payload.text` : send a text message.
| | `payload.quick_replies`: send a quickreply along with a text message.|
| html |`payload.html` : send styled message by setting the html here.|
| quickreply | `payload.quick_replies` : Data for the component of quick_reply. |
| |`quick_replies[].id` : Unique button id |
| |`quick_replies[].ref` : A code that can be used to distinguish the selected option. |
| |`quick_replies[].content_type` : Type of QR Component. (text, url, location, calender, etc.) |
| |`quick_replies[].style` : Style to be used for the button. |
| |`quick_replies[].title` : Text to be displayed on the button |
| |`quick_replies[].icon` : Icon url to be placed on the right of the button |
| |`quick_replies[].url` : Url to open on tap of the button.|
| component | `message.payload` will contain all the data. |

#### Properties
Properties to the message.

| Property | Description |
| --- | --- |
| tag | "Ad / New / etc." : Special tag associated with message. |
| disabled | "True / False / Hidden": Wheather to disable or hide the inputbox |
| placeholder | "String to show in placeholder." |
| timestamp | "Unix Time stamp." | 

The whole sturcture is as follows:
```
  {
    messages: [
      {
      <!-- The type of message to be sent -->
        type: "text / html / quickreply / component",
        <!-- Unique Message ID associated with the entire message. -->
        message_id: "alpha numeric string",
        
        payload: {
          <!-- To send a text message. Can be paired with quick_replies -->
          text: "This is a simple text",
          <!-- To send a styled message. Can be paired with quick_replies -->
          html: "<h2>This is html</h2>",
          quick_replies: [{
            id: "unique button id",
            ref: "ref to send back. Could be anything.",
            content_type: "text / url / location",
            style: "primary / secondary",
            title: "(opt) Text to show.",
            icon: "(opt) Icon url to show on the right. 24px x 24px",
            url: "(opt) Url to redirect to."
          }]
        },
        properties: {
          tag: "",
          disabled: "True / False / Hidden",
          ip_placeholder: "String to show in placeholder",
          timestamp: 150000,
        }
      }
    ]
  }
```

### To Do:
1. List components.
2. Structure the JSON for each component.
3. Paged documentation for each.

***~*** ***Abhinandan Shah*** ***~***
