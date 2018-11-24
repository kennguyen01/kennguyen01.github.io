---
title: Make a Chatbot with IBM Watson Part 2
date: 2018-10-23
categories: technology
---

![Chatbot](/images/chatbot.jpg)

Here is the link to part 1: [Part 1](/technology/make-a-chatbot-with-ibm-watson-part-1.html)

Now that we finished with defining the intents for our chatbot, let’s move on to entities and dialogs. In general, entities are specific details about what the user wants. In the previous part, I mentioned that a user who wants to find RPG games is different from a user who wants to get a shooter game. The details about their games are different. This is where entities come in. They allow us to hone in specifically on the details and deliver customized responses to our users.

<!--more-->

## Creating Entities

Using the examples above, let’s create the entity **@game-types**. Note the **@** symbol in front of the entity name. It denotes an entity for Watson. We can click on the **Entities** button right next to the **Intents**. Then you can choose **Add entity** to create our first one.

![Add entity](/images/add-entity.jpg)

After you create the new entity, you can add values that entity. I added some of the well known game genres such as action, adventure, role-playing, etc. to the list of values. To the right of each value that I added, the word Synonyms appear. They are other terms that can be also be used to describe the value.

One cool thing is that you can easily get a list of suggestions from Watson. By clicking on the blue icon to the left of the value, a list of synonym for the word pops up. You can select from any of the suggested synonyms and click Add selected to add them.

![Game types](/images/game-types.jpg)

## More Entities and Values

It’s a convenient feature so make sure to use it. Once you fill out all of the synonyms you can think of. Click on the Try it button and let Watson train on those new entities. As always, when Watson finished, test out our new entities with a few questions to make sure that Watson respond properly to the new entity.

![Game types entity](/images/game-types-entity.jpg)

Great! It looks like Watson is able to understand when the user asks it about different types of games. But a game store is not limited to just selling games. It also sells different game systems such as the PlayStation, XBox, and Nintendo consoles. We will add another entity named **@consoles** to Watson. Feel free to add any console system to the value that you think the user is likely to look for. I’m going to add some of the popular systems available.

![Consoles entity](/images/consoles-entity.jpg)

Take the time to let Watson train on the new entity. Test out what Watson learned after it finished training. Once everything looks good, we can move on the actually creating some dialogs.

## Dialog Flow

Right now our chatbot is capable of recognizing the intents and entities from the user. However, it doesn’t provide any response to the user so it’s not very useful. We are going to improve on that and build a simple dialog flow. Let’s jump into the **Dialog** section of our build and create a new dialog.

![New dialog](/images/new-dialog.jpg)

Every new dialog comes with two default nodes, **Welcome** and **Anything else**. The Welcome node is what our chatbot says when the user first interacts with the chatbot. The Anything else node is just a catch all response when our chatbot cannot match user’s input with any intents or entities.

When you click on the Welcome node, it will open the Welcome dialog panel. Inside, there’s a default condition and response. You do not need to change the default condition. I changed the response to reflect the function of our chat bot. The welcome response is there to direct the user to asks questions that are relevant to our store.

![Welcome node](/images/welcome-node.jpg)

Then we simply set the final condition as **Wait for user input**. We want to know what the user wants to do before we move down the dialog tree. Remember that we had the general intents such as **#greetings**, **#thanks**, and **#goodbyes**. Now is a good time for us to take care of the general dialogs before moving on to something specific.

## General Dialog

Sometimes the user will say hi to our chatbot before asking any question. If that’s the case, then we need to have a dialog node in place for that. You can create a new node by either clicking on the **Add node** button or you can click on the three dots next to the Welcome node and select **Add node below**. After you create the new node, go inside its panel and give it the name of **Greetings**.

Under where it says **If bot recognizes**, type in the intents **#greetings**. This will allow our bot to recognize that intent and respond with a dialog. We can reiterate what we said in the Welcome node or add more responses as we see fit. For the **And finally** condition, we let the user to enters additional inputs before moving on again.

![Greetings node](/images/greetings-node.jpg)

The process is going to be the same for both #thanks and #goodbyes. Create more nodes for those intents under the Greetings node. Then add whatever responses you want the chatbot to answer back to the user. Below are some examples for #thanks:
- You're welcome.
- Anytime.
- Glad I could help
- No problem

Remember to use the proper vocabulary and grammar for the responses. Our chatbot is representing our business so it should respond accordingly. We want to show the user that we care through small details like that. Right below the responses, you can also click on the option to have our chatbot cycles through the responses in **random** order.

The order of the nodes in our dialog flow is important. Our chatbot will start from the top and go through the nodes one by one until it finds the node corresponding the user’s intents and entities.

![General dialogs](/images/general-dialogs.jpg)

I’m going to end the post here. In the next post I’ll go over how to add branching conditionals, multiple responses, and deploying our chatbot.
