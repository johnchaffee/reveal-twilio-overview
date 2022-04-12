<!-- .slide: data-background="pink" -->
## What's so great about Lani?

* She's sweat <!-- .element: class="fragment" data-fragment-index="1" -->
* She smells good <!-- .element: class="fragment" data-fragment-index="2" -->
* She buys great gifts <!-- .element: class="fragment" data-fragment-index="3" -->
* She's great at planning trips <!-- .element: class="fragment" data-fragment-index="4" -->


## Provisioning

<div class="text60">

* Zipwhip
  * Zipwhip only allows you to provision (text-enable) an existing landline number
  * Zipwhip provides a console and API
  * API provisioning is completed in seconds
* Twilio
  * Twilio typically sells you a new number for voice and text.
  * Twilio has a beta API, Hosted Numbers, that allows you to provision an existing landline number
  * Console or API
  * Line owner must verify ownership via automated phone call (like our self-serve)
  * Owner must sign LOA
  * Turn around: Up to 1-day for 10DLC, 3-days for TF
  * Dan said 10DLC& TF SMS is hard coded to 1MPS
  * MMS not supported

</div>


## 3rd-Party Plugin<br>P latform Evaluation

- [GMail Add-Ons](#/gmail)
- [Slack Apps](#/slack)
- [Outlook Add-Ins](#/outlook)
- [MS Teams](#/teams)


<!-- .slide: id="gmail" -->
## Gmail Add-Ons

- UI Components
  - Sidebar
  - Compose Modal

- Development Environment
  - Apps Script
  - Cards

- Add-ons run on Web & Mobile


<img class="" src="./images/gmail-addons.png">


<!-- .slide: id="gmail-card" -->
<img class="" src="./images/gmail-compose2.png">


## Gmail Cards

<div class="flex-container">
  <div class="col1">
    <img class="" src="./images/gmail-card1.png">
  </div>

  <div class="col1">
    <img class="" src="./images/gmail-card2.png">
  </div>
</div>


## Gmail Manifest

<div class="text70">

  Scopes
  ```json
    "oauthScopes": [
      "https://www.googleapis.com/auth/gmail.addons.current.action.compose",
      "https://www.googleapis.com/auth/gmail.addons.current.message.readonly",
      "https://www.googleapis.com/auth/gmail.addons.execute",
      "https://www.googleapis.com/auth/script.locale"],
  ```

  Triggers
  ```json
      "gmail": {
        "contextualTriggers": [{
          "unconditional": {
          },
          "onTriggerFunction": "onGmailMessage"
        }],
        "composeTrigger": {
          "selectActions": [{
            "text": "Insert payment request",
            "runFunction": "onGmailCompose"
          }],
          "draftAccess": "NONE"
        }
      }
  ```

</div>


## Gmail Apps Script

<div class="text80">

Building the [Compose Modal Card](#/gmail-card)

```js [1|2-3|4-16|17-24|25-29|30-32|33]
function onGmailCompose(e) {
  var header = CardService.newCardHeader()
      .setTitle('Request Payment')
  var sku = CardService.newSelectionInput()
    .setType(CardService.SelectionInputType.RADIO_BUTTON)
    .setTitle("Select a SKU")
    .setFieldName("sku")
    .addItem("Standard Edition ($49.99)", "Standard Edition", true)
    .addItem("Professional Edition ($79.99)", "Professional Edition", false)
    .addItem("Enterprise Edition ($99.99)", "Enterprise Edition", false);
  var quantity = CardService.newTextInput()
      .setFieldName('quantity')
      .setTitle('Quantity')
  var notes = CardService.newTextInput()
      .setFieldName('notes')
      .setTitle('Notes (optional)')
  var action = CardService.newAction()
      .setFunctionName('onGmailInsertTxt2Pay');
  var button = CardService.newTextButton()
      .setText('Insert Payment Request')
      .setOnClickAction(action)
      .setTextButtonStyle(CardService.TextButtonStyle.FILLED);
  var buttonSet = CardService.newButtonSet()
      .addButton(button);
  var section = CardService.newCardSection()
      .addWidget(sku)
      .addWidget(quantity)
      .addWidget(notes)
      .addWidget(buttonSet);
  var card = CardService.newCardBuilder()
      .setHeader(header)
      .addSection(section);
  return [card.build()];
}
```

</div>


## Twilio Send SMS

<div class="text80">

```bash
curl -X POST \
  -d "Body=Hi there, your new phone number is working." \
  -d "From=${TWILIO_NUMBER}" \
  -d "To=${MOBILE_NUMBER}" \
  "https://api.twilio.com/2010-04-01/Accounts/${ACCOUNT_SID}/Messages" \
  -u "${ACCOUNT_SID}:${AUTH_TOKEN}"
```

</div>


## Side by side bulleted lists

<div class="flex-container">
<div class="col1">

* one
* two
* three

</div>

<div class="col1">

* one
* two
* three

</div>
</div>


## iframe test

<iframe src="https://embed.zipwhip.com/" width="300px" height="450px" style="border: solid 1px #aaa;"></iframe>


## The End

[&larr; Back to beginning](#/0)


<!-- .slide: id="priorities" -->
## Priorities
1. Plugin framework /shim
2. Broker
3. Developer dashboard
4. Eventing webhooks
5. APIs

[&larr; Back to beginning](#/0)


## Technologies

<div class="text80">

API | Description 
--- | ---
**Front-end Plugin** | UI components displayed in the Zipwhip app
**Back-end APIs** | External server sends requests to Zipwhip API
**Webhooks** | Zipwhip sends notifications to external server

</div>


## Quote

> Now is the time for all good men to come to the service of their country


## iframe cols

<div class="flex-container">
   <div class="col3">
<pre><code class="html">&lt;iframe 
   src="https://embed.zipwhip.com" 
   width="300px"
   height="450px"&gt;
&lt;/iframe&gt;
</code></pre>
   </div>
   <div class="col2">
      <iframe src="https://embed.zipwhip.com/" width="300px" height="450px" style="border: solid 1px #aaa;"></iframe>
   </div>
</div>


## iframe no cols

<iframe src="https://embed.zipwhip.com/" width="300px" height="450px" style="border: solid 1px #aaa;"></iframe>

<div class="text70">

```html
<iframe src="https://embed.zipwhip.com/" width="300px" height="450px"></iframe>
```

</div>


<section data-background-iframe="https://developers.zipwhip.com/widget/builder/" data-background-interactive></section>


<section data-background-iframe="https://developers.zipwhip.com/api/software/spec/" data-background-interactive></section>


## Slide 1

Form input below

<form action="#">
    <input type="text"></input>
</form>

<button>My button</button>


## 7/10/20 Agenda

<div class="text80">

* AuthVia deep-dive
	- Talk to David about AuthVia
* Plugin platform research
	* Slack
	* Salesforce LWC
	* Google Apps Script
* Sprint planning
* David
	* Calendar events Eddy RCS -> next week?
+ Review MVP with Avery and Snelling
- Schedule Developer Dashboard

</div>


## Slide 3

- What is there is a whole bunch of text, will it automatically make it smaller?
- Bullet 3 
- foo
- Even [links](https://www.google.com)


## Slide 3 Image

![External Image](https://s3.amazonaws.com/static.slid.es/logo/v2/slides-symbol-512x512.png)


## Slide 4 image

- What is there is a whole bunch of text, will it automatically make it smaller?
- Bullet 3 
- foo
- Even [links](https://www.google.com)

![Cat](./images/cat.jpg)


## Slide 4 r-stretch image

- What is there is a whole bunch of text, will it automatically make it smaller?
- Bullet 3 
- Even [links](https://www.google.com)

<img class="r-stretch" src="./images/cat.jpg">


## Slide 5 Flex col1-1

<div class="flex-container">

<div class="col1 text60">

- What is there is a whole bunch of text, will it automatically make it smaller?
- What is there is a whole bunch of text, will it automatically make it smaller?
- What is there is a whole bunch of text, will it automatically make it smaller?
- What is there is a whole bunch of text, will it automatically make it smaller?
- What is there is a whole bunch of text, will it automatically make it smaller?
- Bullet 3 
- Even [links](https://www.google.com)

</div>

<div class="col1">

![Cat](./images/cat.jpg)

</div>

</div>


## Slide 5 Flex col1-1

<div class="flex-container">

<div class="col1 text60">

```html
<iframe 
  src="https://embed.zipwhip.com/" 
  width="400px" 
  height="500px"> 
</iframe>
```

</div>

<div class="col1">

<iframe src="https://embed.zipwhip.com/" width="400px" height="500px"></iframe>

</div>

</div>


## Slide 5 Flex col2-1

<div class="flex-container">

<div class="col2 text60">

- What is there is a whole bunch of text, will it automatically make it smaller?
- What is there is a whole bunch of text, will it automatically make it smaller?
- What is there is a whole bunch of text, will it automatically make it smaller?
- What is there is a whole bunch of text, will it automatically make it smaller?
- What is there is a whole bunch of text, will it automatically make it smaller?
- Bullet 3 
- Even [links](https://www.google.com)

</div>

<div class="col1">

![Cat](./images/cat.jpg)

</div>

</div>


## Slide 5 Flex col1-2

<div class="flex-container">

<div class="col1 text50">

- What is there is a whole bunch of text, will it automatically make it smaller?
- What is there is a whole bunch of text, will it automatically make it smaller?
- What is there is a whole bunch of text, will it automatically make it smaller?
- Bullet 3 
- Even [links](https://www.google.com)

</div>

<div class="col2">

![Cat](./images/cat.jpg)

</div>

</div>


## Slide 5C Flex r-frame

<div class="flex-container">

<div class="col1 r-frame">
<!-- r-frame adds a frame around the element -->

![Cat](./images/cat.jpg)

</div>

<div class="col1">

![Cat](./images/cat.jpg)

</div>

</div>


## Slide 7

Goodbye

[Start Over](#/0)
