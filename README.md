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


## Components List
All possible Components for Quickreply, Message and Modal.

### Quickreply Components

     1. Buttons
       - Text
       - URL redirector
       - Send Location
       - Multi Select
       - Radio
       - Share Button
     2. Card
     3. Carousal
     4. List Picker
     5. Calendar
     6. Audio Recorder
     7. Barcode Scanner
     8. Custom Input
     9. Wizard
     10. File Picker
     
### Message Components
     1. Card
     2. Carousal
     3. Flight Info
     4. List Card
     5. Image Card
     6. Video Card
     7. Audio Card

### Modal Components
Components that opens in a modal:

     1. Image Capture
     2. Video Capture
     3. Seat Booking

# Final JSON Doc

```

function abhinandan() {
	let The_Epic_Json_be =   {
    messages: [
      {
      // <!-- The type of message to be sent -->
        type: "text / html / quickreply / component",
        // <!-- Unique Message ID associated with the entire message. -->
        message_id: "alpha numeric string",
        payload: {
          // <!-- To send a text message. Can be paired with quick_replies -->
          text: "This is a simple text",
          // <!-- To send a styled message. Can be paired with quick_replies -->
          html: "<h2>This is html</h2>",
          quick_replies: {
            id: "QR_ID",
            ref: "",
            elements: {
              buttons: [{
                id: "BTN_ID",
                ref: "QRTX_29A1",
                content_type: "text",
                style: "primary",
                title: "Hello this is a text button!",
                icon: "(opt) Icon url to show on the right. 24px x 24px",
              },{
              	// URL
              	id: "",
              	ref: "QRUL_29A2",
              	content_type: "url",
              	style: "primary",
              	title: "This will open a url in new tab!",
              	icon: "open.jpg",
              	url: "phonon.in/?utm_campaign=PHON"          	
              },{
              	// Multi
              	id: "",
              	ref: "QRML_29A1",
              	content_type: "multi",
              	style: "primary",
              	title: "Multi Option 1",
              	icon: "prefix.jpg",
              	is_selected: "true"
              },{
              	// Radio
              	id: "",
              	ref: "QRRD_29A1",
              	content_type: "radio",
              	style: "primary",
              	title: "Radio Option 1",
              	icon: "radio.jpg",
              	is_selected: "true"
              },{
              	// Share
              	id: "",
              	ref: "QRSH_29A1",
              	content_type: "share",
              	style: "secondary",
              	title: "Share now!",
              	options: {
              		title: "This is the Title!",
              		description: "This is the description of the share!",
              		url: "URL to put if any.",
              		show_facebook: "true",
              		show_twitter: "(opt)false",
              		show_email: "true",
              	}
              },{
                // Location
              	id: "",
              	ref: "QRLC_29A1",
              	content_type: "location",
              	style: "primary",
              	title: "Click to share your location.",
              	icon: "location.jpg",
              }],
            },
        },
        properties: {
          tag: "",
          disabled: "True / False / Hidden",
          ip_placeholder: "String to show in placeholder",
          timestamp: 150000,
          // For QR Multi only
          qr_mul_max: "Max selectables",
          qr_mul_min: "Minimum selectables",
          // 
        }
      }
    ]
  }



function quickreply_component() {
	let The_Epic_Json_be =   {
    messages: [
      {
      // <!-- Quickreply Component. -->
        type: "quickreply",
        message_id: "alpha numeric string",
        
        payload: {
          // <!-- To send a text message. Can be paired with quick_replies -->
          text: "This is a QR component called card.",
          quick_replies: {
            id: "",
            ref: "QRCD_29A0",
            content_type: "generic_card",
            elements: {
              title: "This is the title of card",
              subtitle: "This is the title of card",
              image_url: "BluesExplosion.jpg",
              buttons: [{
                id: "BTN001",
                ref: "JNSWD",
                title: "Jain Sandwhich",
                style: "primary",
                icon: "",
              }]
            }
          },
        }
        properties: {
          tag: "",
          disabled: "True / False / Hidden",
          ip_placeholder: "String to show in placeholder",
          timestamp: 150000,
        }
      },
      {
        type: "quickreply",
        message_id: "alpha numeric string",
        
        payload: {
          // Calendar
          text: "Calendar.",
          quick_replies: {
            id: "",
            ref: "QRCD_29A0",
            content_type: "calendar",
            elements: {}
          },
        }
        properties: {
          tag: "",
          disabled: "True / False / Hidden",
          ip_placeholder: "String to show in placeholder",
          timestamp: 150000,
        },
      }
    ]
  }
}

function component() {
  let The_Epic_Json_be = {
    messages = [
    {
      type: "component",
      message_id: "MID",

      payload: { 
        id: "",
        ref: "",
        content_type: "seat_booking",
        elements: {
          map: [
            'fff_fff',
            'fff_fff',
            'ebe_eee',
            'ee___ee',
            'Bee_eee',
            'Bee_eee',
            'Bee_eee',
            'eee_eee',
            'eee_eeB',
            'eee_Bee',
            'eee_eeB',
            'eee_eee',
            'eee_eee',
            'eee_eee',
            'eee_eee',
            'eee_eee',
            'eee_eee',
            ],
            seats: {
              f:  {
                    price   : 300,
                    classes : 'first-class', //your custom CSS class
                    category: 'First Class'
                  },
              e:  {
                    price   : 200,
                    classes : 'economy-class', //your custom CSS class
                    category: 'Economy Class'
                  }
            },
            columns: ['A', 'B', 'C', ' ', 'D', 'E', 'F'],
            legend : [
              [ 'f', 'available',   'First Class (300 Rs)' ],
              [ 'e', 'available',   'Economy Class (200 Rs)'],
              [ 'f', 'unavailable', 'Already Booked']
            ],
            maxseats: 3,
        }
      },
      properties: {
        tag: "",
        disabled: "True / False / Hidden",
        ip_placeholder: "String to show in placeholder",          
      }
    }]
  }
}

```



### To Do:
1. ~List components.~
2. ~General Structure the JSON for component.~
3. Each Component JSON.
4. Paged documentation for each.





***~*** ***Abhinandan Shah*** ***~***
