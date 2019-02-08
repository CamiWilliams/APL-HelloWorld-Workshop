# Build Your First APL Skill (in 1 hour!)

## Overview

In this workshop, you will create and configure an Alexa Presentation Language skillusing the Alexa Skills Kit SDK in NodeJS and AWS Lambda. When launched, this Alexa skill will have the customer interact with a Hello World skill that features a simple voice interaction and display screen tailored to the device medium.

## Objectives

After completing this workshop, you will be able to:

- Create an Amazon Developer account.
- Create and configure a new skill using the Alexa Skills Kit and AWS Lambda
- Create and configure Intents and Sample Utterances
- Build displays for your skill using the Alexa Presentation Language
- Test a skill using Lambda and an Echo device.

## Prerequisites

This lab requires:

- Access to a notebook computer with Wi-Fi, running Microsoft Windows, Mac OSX, or Linux (Ubuntu, SuSE, or RedHat).
- An Internet browser suchas Chrome, Firefox, or IE9 (previous versions of Internet Explorer are not supported).

## Goal: Completing a Hello World Alexa Skill with APL.

### Overview

Alexa is the voice service that powers Amazon Echo. Alexa provides capabilities, called skills, which enable customers to interact with devices using voice (answer questions, play music, and more).

The Alexa Skills Kit (ASK) is a collection of self-service APIs, tools, documentation, and code samples that make it easy for you to develop your own Alexa skills, which you can then publish. ASK supports simple command-oriented skills, such as &quot;Alexa, ask Greeter to say hello world&quot; as well as sophisticated multi-command dialogs and parameter passing, such as &quot;Alexa, what is this weekend&#39;s weather forecast?&quot; The Alexa Skills Kit is a low-friction way to learn to build for voice.

This task will walk you through creating a simple skill that tells you a &quot;Hello&quot; when you launch it. Through this you will use the Alexa skills kit to learn the fundamentals of building a voice user experience.

### Task 1.1: Create an Account on developer.amazon.com (or Sign In)

1. Navigate to the Amazon Developer Portal at[https://developer.amazon.com/alexa](https://developer.amazon.com/alexa).
2. Click **Sign In** in the upper right to create a free account.

### Task 1.2: Create the Hello World Skill

1. When signed in, click **Your Alexa Dashboards** in the upper right.
2. Choose **Get Started** under Alexa Skills Kit. Alexa Skills Kit will enable you to add new skills to Alexa. (The other option, Alexa Voice Services, is what you use if you want to put Alexa onto other devices such as a Raspberry Pi.)
3. To start the process of creating a skill, click the **Create Skill** button on the right.

### Task 1.3: Skill Information

1. Skill Name:enter **Hello World**.
2. Skill Type: Select **Custom Interaction Model**.
3. Language: Select **English (U.S.).**
4. Invocation Name: **hello world**. This will be the name that you will use to start your skill (eg.,&quot;Alexa, Open _[hello world__]_&quot;.) The invocation name you choose needs to be more than one word and not contain a brand name. Remember the invocation name for future use in this lab.
5. Click **Create Skill**.
6. Select the **Start from scratch** template.
7. Click **Choose**.

### Task 1.4: Interaction Model

1. In the navigation menu on the left, choose **JSON Editor**.
2. Verify that the JSON in the Code Editor matches the JSON below:

```
{
  "interactionModel": {
        "languageModel": {
            "invocationName": "hello world",
            "intents": [
                {
                    "name": "AMAZON.FallbackIntent",
                    "samples": []
                },
                {
                    "name": "AMAZON.CancelIntent",
                    "samples": ["cancel hello world"]
                },
                {
                    "name": "AMAZON.HelpIntent",
                    "samples": []
                },
                {
                    "name": "AMAZON.StopIntent",
                    "samples": []
                },
                {
                    "name": "AMAZON.NavigateHomeIntent",
                    "samples": []
                }
            ],
            "types": []
        }
    }
}
```
**Copy** the above JSON into the Code Editor box. You can type it directly or copy it from [https://s3.amazonaws.com/apl-hello-world-skill/en-US.json](https://s3.amazonaws.com/apl-hello-world-skill/en-US.json)

Each of these JSON fields are **Intents**. Intents represent what your skill can do, they are an action Alexa will take. To prompt Alexa for the action, a user would say an **Utterance**. In the case of the **CancelIntent** , the **Utterance** a user would say to perform the cancel action would be &quot;cancel hello world&quot;.

All of the intents in this model are built-in Amazon intents that have utterances already trained that Alexa understands.

This skill is very basic, so our intent model just uses the default built-in intents for Help and Stop/Cancel.

3. Click the **Save Model** button. This will start the process of creating your interaction (If you did not make changes in the Code Editor the **Save Model** button is gray).
4. Click on the **Interfaces** tab on the left menu.
5. Scroll to the bottom and toggle **Alexa Presentation Language** to on. This will allow you to use APL in your skill.
6. Click on the **Save Interfaces** button at the top.
7. Once the interfaces are saved, click on **Build Model.**
8. We&#39;re now done with the Interaction Model. Choose **Enpoints** in the left menu.

### Task 1.5: Configuration

Your skill needs to be connected to an endpoint that will perform your skill logic. We will be using AWS Lambda for this lab. We will create the Hello World skill Lambda function, copy its ARN (Amazon Resource Name), and paste it into your skill&#39;s configuration page.

1. In a new browser tab, go to [http://aws.amazon.com](http://aws.amazon.com/)
2. **Sign in** to the management console.
3. From the region selector in the upper right, be sure that you&#39;re in the **US East (N. Virginia)** region.
4. From the Services menu on the left of the top menu bar, choose **Services | Compute | Lambda**.
5. Click the orange **Create Function** button in the upper right.
6. Assure that **Author from scratch** is toggled.
7. Name: **helloWorldSkill**
8. Runtime: NodeJS 8.10
9. Role: **Create a new role from one or more template(s)**
10. Role name: **helloWorldSkillRole**
11. Policy templates: **Simple microservice permissions**
12. Click the orange **Create function** in the lower right.

The Lambda function for your skill has now been created. Now you need to attach your skill to it.

14. In the **Designer** view, under **Add Triggers** , select **Alexa Skills Kit**
15. In the upper-right corner of the page, **copy your ARN**. Copy everything except &quot;ARN-&quot;. It will look like this:
`arn:aws:lambda:us-east-1:123456789012:function:helloWorldSkill`
16. Now **switch browser tabs back to your skill** in the developer portal. You should be on the Endpoints tab. (If you closed the browser tab, here&#39;s how to get back: Go to  [http://developer.amazon.com](http://developer.amazon.com/), sign in, click Alexa, click Alexa Skills Kit, click on your skill name, click on Endpoints from the left-hand menu).
17. Select **Endpoint** from the left menu.
18. For the service endpoint type, choose the **AWS Lambda ARN (Amazon Resource Name)** radio button.
19. **Paste your Lambda ARN** into the Default text field.
20. Click **Save Endpoints**.
21. Copy your skill ID.
22. Navigate back to your **Lambda function tab**. **Click** on the **Alexa Skills Kit** trigger that we previously added in the **Designer** view (it should say &quot;Configuration Required&quot; underneath).
23. Scroll down to the **Configure Triggers** view.
24. Skill id verification: **Enabled**
25. **Paste** your skill id.
26. Click **Add.**
27. Click **Save**.

Next, we will upload the Hello World skill code into Lambda. You should now see details of your helloWorldSkill Lambda function that includes your function&#39;s ARN in the upper right and the Configuration view of your function.

28. Click on the **helloWorldSkill** part of the tree in the **Designer** view.
29. Scroll down to see the **Function code** view.
30. Code Entry Type: **Upload a .zip file**
31. Ensure **Node.js 8.10** is selected for **Runtime**
32. Handler: **index.handler**.
33. Function Package: **Upload** the following .zip file: [https://s3.amazonaws.com/apl-hello-world-skill/Archive.zip](https://s3.amazonaws.com/apl-hello-world-skill/Archive.zip)
34. Click the **Save** button in the top of the page. This will upload your function code into the Lambda container.

After the Save is complete, you should see your code editor inline (Note, if your function code becomes large, this view will not be available after uploading, but will still run). 

### Task 1.6: Test your voice interaction

We&#39;ll test your skill two times. First, we&#39;ll test the voice interaction is intact in the simulator. Then, we will add APL and test with a multimodal device in the simulator.

1. Switch browser tabs to **the developer portal** (If you closed the browser tab, here&#39;s how to get back: Go to  [http://developer.amazon.com](http://developer.amazon.com/), sign in, click Alexa, click Alexa Skills Kit, click on your skill name).
2. Scroll to the top of the page and click **Test**.
3. Switch **Test is disabled for this skill** to Development.
4. In **Alexa Simulator** tab, under **Type or click…**, type &quot;open hello world&quot;
5. You should hear and see Alexa respond with &quot;Welcome to the Alexa Skills Kit, you can say hello!&quot;

### Task 1.7: Add displays to your LaunchRequest

We will now add some displays written in the Alexa Presentation Language to your skill&#39;s LaunchRequest. The LaunchRequest is the function that is called when a user invokes your skill without an utterance, just the invocation name (for example, &quot;Alexa open [hello world]&quot;).

1. In the **developer portal** , select the **Build** tab in the top menu.
2. Scroll down and select the **Display** tab on the left menu.
3. This will navigate you to the **APL Authoring Tool**. This is an authoring tool used to create and edit APL documents for your skill. There are currently 7 sample templates you can use. For now, we will start from scratch. Select **Start from scratch**.
4. In the top pane, you can toggle between different devices. Select **Small Hub**.
5. Select the **toggle** in the middle of the authoring tool. This should switch views to the raw code. You should see this APL code in the editor:

```
{
    "type": "APL",
    "version": "1.0",
    "theme": "dark",
    "import": [],
    "resources": [],
    "styles": {},
    "layouts": {},
    "mainTemplate": {
        "items": []
    }
}
```
APL is made up of Components dictated in the mainTemplate. A component is a primitive element that displays on the viewport of the device.

6. Under items, **add** a **Container** component. This component can contain and orient child components.

```
{
    "type": "APL",
    "version": "1.0",
    "theme": "dark",
    "import": [],
    "resources": [],
    "styles": {},
    "layouts": {},
    "mainTemplate": {
        "items": [
            {
                "type": "Container",
                "width": "100vw",
                "height": "100vh",
                "items": []
            }
        ]
    }
}
```
This Container currently has a width 100% of the viewport width (100vw) and 100% of the viewport height (100vh).

7. Add a child component to the Container. **Insert** a **Text** component that reads &quot;Hello, World!&quot;.

```
{
    "type": "APL",
    "version": "1.0",
    "theme": "dark",
    "import": [],
    "resources": [],
    "styles": {},
    "layouts": {},
    "mainTemplate": {
        "items": [
            {
                "type": "Container",
                "width": "100vw",
                "height": "100vh",
                "items": [
                    {
                        "type": "Text",
                        "text": "Hello, World!"
                    }
                ]
            }
        ]
    }
}
```

You will now see a cut-off &quot;Hello, World!&quot; appear on screen. The text is currently cut off on the round hub, because the Container view defaults to a square, versus a circle.

8. **Align** the text to be in the center of the screen. **Set** the **height** of the Text component to 100vh and the **width** of the Text component to 100vw. **Add the properties** _textAlign: center_ and _textAlignVertical: center_ to the Text component.

```
{
    "type": "APL",
    "version": "1.0",
    "theme": "dark",
    "import": [],
    "resources": [],
    "styles": {},
    "layouts": {},
    "mainTemplate": {
        "items": [
            {
                "type": "Container",
                "width": "100vw",
                "height": "100vh",
                "items": [
                    {
                        "type": "Text",
                        "text": "Hello, World!",
                        "height": "100vh",
                        "width": "100vw",
                        "textAlign": "center",
                        "textAlignVertical": "center"
                    }
                ]
            }
        ]
    }
}
```
Now you can see the Text in the center of the screen vertically and horizontally.

9. **Toggle** in between the various devices. If you click on Medium Hub, Large Hub, and Extra-Large TV in the authoring tool, you can see the same experience on every device.

Now that we have a visual experience that fits for every device, lets change the customer experience to be different for any devices that are NOT round. This will be utilizing the built-in **viewport properties** that specifies device characteristics like size, shape, and orientation.

10. Select **Medium Hub**.
11. In the Text component, add a **when** statement. The when statement uses data-binding to show or hide the component it is attached to based upon the condition specified. This condition should be &quot;if the viewport shape is round&quot;.

```
{
    "type": "APL",
    "version": "1.0",
    "theme": "dark",
    "import": [],
    "resources": [],
    "styles": {},
    "layouts": {},
    "mainTemplate": {
        "items": [
            {
                "type": "Container",
                "width": "100vw",
                "height": "100vh",
                "items": [
                    {
                        "when": "${viewport.shape == 'round'}",
                        "type": "Text",
                        "text": "Hello, World!",
                        "height": "100vh",
                        "width": "100vw",
                        "textAlign": "center",
                        "textAlignVertical": "center"
                    }
                ]
            }
        ]
    }
}
```
Now the text component will only show on any hubs that are round. So, if you **toggle** back to the **Small Hub,** you should see the &quot;Hello, World!&quot; text.

12. Under the Text component, **add** a similar **Text** component with the when condition of &quot;if the viewport&#39;s shape is not round&quot;. **Set** the color of this component to **red**.

```
{
    "type": "APL",
    "version": "1.0",
    "theme": "dark",
    "import": [],
    "resources": [],
    "styles": {},
    "layouts": {},
    "mainTemplate": {
        "items": [
            {
                "type": "Container",
                "width": "100vw",
                "height": "100vh",
                "items": [
                    {
                        "when": "${viewport.shape == 'round'}",
                        "type": "Text",
                        "text": "Hello, World!",
                        "height": "100vh",
                        "width": "100vw",
                        "textAlign": "center",
                        "textAlignVertical": "center"
                    },
                    {
                        "when": "${viewport.shape != 'round'}",
                        "type": "Text",
                        "text": "Hello, World!",
                        "height": "100vh",
                        "width": "100vw",
                        "textAlign": "center",
                        "textAlignVertical": "center",
                        "color": "red"
                    }
                ]
            }
        ]
    }
}
```
Now **toggling** between the different devices, you can see a red &quot;Hello, World!&quot; for any landscape devices, and a white &quot;Hello, World!&quot; for round devices.

We have finished authoring our display screen for our skill, we now need to add this APL code to our skill.

13. **Copy** the entire APL code.
14. **Now switch browser tabs** back to your Lambda function code.
15. Assure you have selected the **helloWorldSkill** function under the **Designer** view and scroll down to the **Function code**
16. Select **File -\&gt; New File**
17. **Paste** the APL code.
18. Select **File -\&gt; Save As** and name this file **main.json.** Assure it is being saved under the **helloWorldSkill**
19. Once main.json is saved, you should see it appear in the navigation view on the left. **Select** js.
20. **Navigate** to the **LaunchRequest** (line 6).

We will now add an APL directive to the LaunchRequest response. A directive specifies how a compiler (or other translator) should process its input. In this case, our directive type will be `Alexa.Presentation.APL.RenderDocument`, indicating to interpret the input as a document to render as APL, and our input will be our main.json document.

21. **Add** an if statement to determine if the customer&#39;s device has a display using the **supportsAPL** function. The current return statement should be in the else of that statement (line 13).

```
    if(supportsAPL(handlerInput)) {

    } else {
      return handlerInput.responseBuilder
        .speak(speechText)
        .reprompt(speechText)
        .withSimpleCard('Hello World', speechText)
        .getResponse();
    }

```
22. In the if statement, **paste** the following code:

```
return handlerInput.responseBuilder
      .speak(speechText)
      .reprompt(speechText)
      .withSimpleCard('Hello World', speechText)
      .addDirective({
          type: 'Alexa.Presentation.APL.RenderDocument',
          document: require('./main.json')
        })
      .getResponse();

```
23. Click **Save** at the top of the window **.**

### Task 1.8: Test your voice interaction and display interface.

We&#39;lltest yourskillinwith the new APL displays in the testing simulator.

1. Switch browser tabsto **the developer portal**
2. Scroll to the top of the page and click **Test.**
3. In **Alexa Simulator** tab, under **Type or click…** , type &quot;open hello world&quot;
4. You should hear and see Alexa respond with &quot;Welcome to the Alexa Skills Kit, you can say hello!&quot;
5. Hover your mouse on the right side of the portal. Scroll down to the bottom, you can now see your APL displays. You can toggle between devices and retest by typing &quot;open hello world&quot;

## Congratulations! You have finished your first APL skill!

See more information about APL and Multimodal skill building: [http://alexa.design/multimodal](http://alexa.design/multimodal)

See more APL skill examples:

- Fire TV Vlogs (NodeJS): [https://github.com/alexa-labs/skill-sample-nodejs-firetv-vlogs](https://github.com/alexa-labs/skill-sample-nodejs-firetv-vlogs)
- Pager Karaoke (NodeJS): [https://github.com/alexa-labs/skill-sample-nodejs-pager-karaoke](https://github.com/alexa-labs/skill-sample-nodejs-pager-karaoke)
- Pager Karaoke (Python): [https://github.com/alexa-labs/skill-sample-python-pager-karaoke](https://github.com/alexa-labs/skill-sample-python-pager-karaoke)
- Pager Karaoke (Java): [https://github.com/alexa-labs/skill-sample-java-pager-karaoke](https://github.com/alexa-labs/skill-sample-java-pager-karaoke)
- Space Explorer (NodeJS): [https://github.com/alexa-labs/skill-sample-nodejs-space-explorer](https://github.com/alexa-labs/skill-sample-nodejs-space-explorer)
- Level Up Riddles (NodeJS): [https://github.com/alexa-labs/skill-sample-nodejs-level-up-riddles](https://github.com/alexa-labs/skill-sample-nodejs-level-up-riddles)
- Movie Quotes Quiz (NodeJS): [https://github.com/alexa-labs/skill-sample-nodejs-movie-quotes-quiz](https://github.com/alexa-labs/skill-sample-nodejs-movie-quotes-quiz)
