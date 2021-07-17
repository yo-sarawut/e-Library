Use Google App Script to Create a Line bot Reminder
==

>My new company was looking for a way to remind members to punch in/out everyday. As they mainly use LINE, I thought maybe LINE bot can be helpful if I can trigger it to send messages periodically 🤖

![](https://miro.medium.com/max/1400/1*JCRYpAed_y09cNzolE4hDw.png)

In this post, I’ll show you how to achieve this with Google App Script:

1.  Set up environment
2.  Write our script
3.  Run

## Our Goal

Create a LINE bot to send a message to a list of users at 9 a.m. and 6 p.m. everyday.

## System Requirement

A Google account and Line Messaging API (Yes, that’s all 🙌)

# Set up environment

1️⃣ We need to register ourselves as LINE developers → create a provider → create a Messaging API.  [Here is the official step by step instructions](https://developers.line.biz/en/docs/messaging-api/getting-started/). In the end, we can add the bot by QR code:

![](https://miro.medium.com/max/1400/1*ejcaWyCIP2m3NHM1Hm8Ciw.png)

2️⃣ Go to your Google Drive and create a new folder (💬 Mine is “Linebot”). Next, create:

-   **a Google Sheet:**  This will be our database, storing userIDs of members who need to receive messages.
-   **a Google App Script:**  Write our logic here to store userIDs and send reminders.

![](https://miro.medium.com/max/60/1*bVRig-fBDTA4GXqZZTf0Cg.png?q=20)

![](https://miro.medium.com/max/700/1*bVRig-fBDTA4GXqZZTf0Cg.png)

# Write our script

If you are also new to GAS, these parts will be handy:

![](https://miro.medium.com/max/1400/1*O5hhs27kue8Xqc7VBgJzog.png)

1.  We can create many files here. However, it is important that ⚠  **function names in each files should all be different**! ⚠ Since we do  **NOT**  need to write  `import functionA from "./a.gs"`  in GAS, it will be confused if there are duplicated function names in the same project.
2.  The Save icon will save  **all changes**  in the current project (In the case above, changes in three files will all be saved 💾)
3.  To test a function, click  **Run** and the function on the right (In the example above:  `replyMsg`  ) will be executed separately 👟

Back to work, our script contains 👌 main sections:

-   Handle messages from LINE
-   Add userID into Google sheet
-   Send reminders to all users

## 1. Handle messages from LINE

In the end, we will deploy GAS as the Messaging API’s Webhook URL. In this way, LINE will send an HTTP  `POST`  request whenever it receives any message. Hence, in our Apps Script, we use a  `doPost(e)`  function in  `Code.gs`  to handle events send from Line.

Don’t forget to replace the  `channelToken`  above with your own ones, which can be found in the Developers’ console:



![](https://miro.medium.com/max/700/1*ppn1RruV_teCsrYfoMyH3Q.png)

## 2. Add userID into Google sheet

When user tell our LINE bot: “Remind me to punch”, before replying the message, we have to check if this user is already in our remind list:

Remember the Google Sheet we created for storing users’ ids? We need its sheet id now😉



![](https://miro.medium.com/max/700/1*-h_sI4wZ0XftvKFfJirDZg.png)

Let’s put it in the following code (in  `openSheet.gs`) :

If the userId is not in the Sheet, we use  `appendRow`  to add its id at the last row.

Awesome, now we have a list of userId. We can move on to send them reminder ⏰

## 3. Send reminders to all users

In LINE Messaging API, we will need each user’s id to send them messages:

So let’s get the list of userId from our sheet:

As the reminder should not send messages during the weekend, I added a  `checkDay()`  function.  [You can change the time zone to yours from this list](https://sites.google.com/site/scriptsexamples/available-web-apps/event-manager/documentation/tools/time-zones)  🌏

Last but not least, we need a trigger to execute  `sendReminder()`  on 9 a.m. and 6 p.m. on weekdays.  [This video explains many other functions that can be used in setting up a time-based trigger](https://www.youtube.com/watch?v=5BYhGGPQlyA)  ⏳

# Run

Almost there! last ☝+✌ steps:

1.  Set up the trigger
2.  Deploy the GAS project
3.  Verify the webhook in LINE Messaging API

## 1. Set up the trigger

Before deploying, we have to make sure the trigger is set. So save the project → Run  `trigger.gs`  (the function should be  `setupTrigger()`) → Check the trigger tab



![](https://miro.medium.com/max/700/1*ZMhzlvTxYpLEFoaDih12pQ.png)

In the tab, we should see 2 triggers (`morningReminder` and  `eveningReminder`). We can see more details when choosing  `edit`  (The trigger below is the one we set on 8:55 a.m.) You may discover that yes, setting up the trigger in code gives us more flexibility



![](https://miro.medium.com/max/700/1*X8g_C0Jq2jOeGIRmmtuVKg.png)

🙋‍♀️  **Side Note**: there may be time difference on the time we set and the time GAS was triggered. In the  `LastRun`log above, my 8:55 reminder is executed at 8:57, while the 18:00 reminder is triggered at 18:03 🤷‍♂️ We’ve tried our best 😅

## 2. Deploy the GAS project

Deploy → New deployment → Type:  `Web app`  →  `Anyone`  can access (so users won’t be asked to authorize the script)→ Deploy



![](https://miro.medium.com/max/700/1*3KDegUDD102QCn10G1rnWA.png)

## 3. Verify the webhook in LINE Messaging API

Copy the Web app URL → Set it as Messaging API’s Webhook URL → Verify (Some times there will be weird errors, but just click  `Verify`  again. It should work 😏)



![](https://miro.medium.com/max/700/1*KUxr2aQn04wIg3pjH2JdLg.png)

Hooray! It works 🍕🍕🍕

![](https://miro.medium.com/max/1400/1*Agukh-Lgcag6xsrT9CEWdQ.png)


> Reference : https://medium.com/nerd-for-tech/use-google-app-script-to-create-a-line-bot-reminder-ebf5f8a8a1dc
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjgwNzc5MDQwXX0=
-->